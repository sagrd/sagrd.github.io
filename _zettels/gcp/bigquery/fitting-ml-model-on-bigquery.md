---
date: 2025-01-03
layout: zettel
category: show
tags:
  - bigquery
  - machine-learning
  - gcp
article-name: from bigquery labs
---
#### Baseline Model: Logistic Regression

- The SELECT statement generates the isGoal outcome variable and extracts relevant features from event data, such as shot distance and angle. Joins are utilized to identify the competition of each shot, allowing for the exclusion of World Cup data from the current modeling, which will be used later after the model has been fitted.
```
CREATE MODEL `soccer.xg_logistic_reg_model`
OPTIONS(
 model_type = 'LOGISTIC_REG',
 input_label_cols = ['isGoal']
 ) AS

SELECT
 Events.subEventName AS shotType,

 /* 101 is known Tag for 'goals' from goals table */
 (101 IN UNNEST(Events.tags.id)) AS isGoal,

  `soccer.GetShotDistanceToGoal`(Events.positions[ORDINAL(1)].x,
   Events.positions[ORDINAL(1)].y) AS shotDistance,

 `soccer.GetShotAngleToGoal`(Events.positions[ORDINAL(1)].x,
   Events.positions[ORDINAL(1)].y) AS shotAngle

FROM
 `soccer.events` Events

LEFT JOIN
 `soccer.matches` Matches ON
   Events.matchId = Matches.wyId

LEFT JOIN
 `soccer.competitions` Competitions ON
   Matches.competitionId = Competitions.wyId

WHERE
 /* Filter out World Cup matches for model fitting purposes */
 Competitions.name != 'World Cup' AND
 /* Includes both "open play" & free kick shots (including penalties) */
 (
   eventName = 'Shot' OR
   (eventName = 'Free Kick' AND subEventName IN ('Free kick shot', 'Penalty'))
 )
;
```
- There is also evaluation (so cool)

![[Pasted image 20250111230710.png]]
- Understanding the model fit (via bigquery [ML weight function](https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights))

![[Pasted image 20250111231141.png]]
	- Each input in the logistic regression model has associated weights: a single numerical weight for continuous features and one for each category in categorical features. Interpreting these coefficients directly can be misleading due to potential correlations among predictors. However, based on general soccer knowledge, the following trends appear reasonable: 
		- penalty kicks have a higher success rate, 
		- shots taken from greater distances tend to have lower success, 
		- and shots taken at steeper angles to the goal are more likely to succeed.
- 
#### XGBOOST
- using BigQuery ML's XGBoost to the data and compare its performance with the earlier fitted logistic regression model. 
- Boosted trees theoretically offer enhanced accuracy due to their capability to capture nonlinear relationships and interactions among features, which logistic regression may not adequately address
```
CREATE MODEL `soccer.xg_boosted_tree_model`
OPTIONS(
 model_type = 'BOOSTED_TREE_CLASSIFIER',
 input_label_cols = ['isGoal']
 ) AS

SELECT
 Events.subEventName AS shotType,

 /* 101 is known Tag for 'goals' from goals table */
 (101 IN UNNEST(Events.tags.id)) AS isGoal,
  `soccer.GetShotDistanceToGoal`(Events.positions[ORDINAL(1)].x,
   Events.positions[ORDINAL(1)].y) AS shotDistance,

 `soccer.GetShotAngleToGoal`(Events.positions[ORDINAL(1)].x,
   Events.positions[ORDINAL(1)].y) AS shotAngle

FROM
 `soccer.events` Events

LEFT JOIN
 `soccer.matches` Matches ON
   Events.matchId = Matches.wyId

LEFT JOIN
 `soccer.competitions` Competitions ON
   Matches.competitionId = Competitions.wyId

WHERE
 /* Filter out World Cup matches for model fitting purposes */
 Competitions.name != 'World Cup' AND
 /* Includes both "open play" & free kick shots (including penalties) */
 (
   eventName = 'Shot' OR
   (eventName = 'Free Kick' AND subEventName IN ('Free kick shot', 'Penalty'))
 )
;
```
- Evaluating results: The log loss and ROC AUC of the boosted tree model is pretty similar to that from the logistic regression model, but slightly worse (higher log loss and lower ROC AUC).
#### Prediction on new data 
- Can use [BigQuery ML's prediction functionality](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-predict)
```
SELECT
 *

FROM
 ML.PREDICT(
   MODEL `soccer.xg_logistic_reg_model`,
   (
     SELECT
       Events.subEventName AS shotType,

       /* 101 is known Tag for 'goals' from goals table */
       (101 IN UNNEST(Events.tags.id)) AS isGoal,

       `soccer.GetShotDistanceToGoal`(Events.positions[ORDINAL(1)].x,
           Events.positions[ORDINAL(1)].y) AS shotDistance,

       `soccer.GetShotAngleToGoal`(Events.positions[ORDINAL(1)].x,
           Events.positions[ORDINAL(1)].y) AS shotAngle

     FROM
       `soccer.events` Events

     LEFT JOIN
       `soccer.matches` Matches ON
           Events.matchId = Matches.wyId

     LEFT JOIN
       `soccer.competitions` Competitions ON
           Matches.competitionId = Competitions.wyId

     WHERE
       /* Look only at World Cup matches for model predictions */
       Competitions.name = 'World Cup' AND
       /* Includes both "open play" & free kick shots (including penalties) */
       (
           eventName = 'Shot' OR
           (eventName = 'Free Kick' AND subEventName IN ('Free kick shot', 'Penalty'))
       )
   )
 )
```
![[Pasted image 20250111234801.png]]