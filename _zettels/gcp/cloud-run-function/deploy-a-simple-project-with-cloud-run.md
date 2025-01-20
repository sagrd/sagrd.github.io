---
date: 2025-01-19
layout: zettel
category: show
tags:
  - gcp
  - cloud-run-function
  - article
article-name: Official Docs
link: https://www.cloudskillsboost.google/course_templates/741/labs/499436
---
- Steps
	- Sample Code: `git clone https://github.com/rosera/pet-theory.git`
	- Change Directory `cd pet-theory/lab03` and edit `package.json` file to change `scripts` json
	
```
...

"scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },

...
```
- 
	- Install packages that the script will run:
```
npm install express
npm install body-parser
npm install child_process
npm install @google-cloud/storage
```
- 
	- To build and deploy; use google cloud build `gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/pdf-converter` 
	- This should list the container in `ArtifactRegistry > Repositories`
	- Deploy with the following cmd. It should show a message after completion
```
gcloud run deploy pdf-converter \
  --image gcr.io/$GOOGLE_CLOUD_PROJECT/pdf-converter \
  --platform managed \
  --region us-east1 \
  --no-allow-unauthenticated \
  --max-instances=1
```
- 
	- Set variable `SERVICE_URL` so you can easily access it
```
SERVICE_URL=$(gcloud beta run services describe pdf-converter --platform managed --region us-east1 --format="value(status.url)")
```
- 
	- And finally invoke the service as authorized user
	- ```curl -X POST -H "Authorization: Bearer $(gcloud auth print-identity-token)" $SERVICE_URL```
	- 
- Trigger Cloud Run
	- Create New Bucket with `gsutil mb gs://$GOOGLE_CLOUD_PROJECT-upload` and `gsutil mb gs://$GOOGLE_CLOUD_PROJECT-processed`
	-  Tell Cloud Storage to send a Pub/Sub notification whenever a new file has finished uploading to the docs bucket ```gsutil notification create -t new-doc -f json -e OBJECT_FINALIZE gs://$GOOGLE_CLOUD_PROJECT-upload```
	- Create a new service account which Pub/Sub will use to trigger the Cloud Run services: ```gcloud iam service-accounts create pubsub-cloud-run-invoker --display-name "PubSub Cloud Run Invoker"```
	- Give the new service account permission to invoke the PDF converter service: ```gcloud beta run services add-iam-policy-binding pdf-converter --member=serviceAccount:pubsub-cloud-run-invoker@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com --role=roles/run.invoker --platform managed --region us-east1```
	- Enable your project to create pub/sub authentication token ```gcloud projects add-iam-policy-binding $GOOGLE_CLOUD_PROJECT --member=serviceAccount:service-$PROJECT_NUMBER@gcp-sa-pubsub.iam.gserviceaccount.com --role=roles/iam.serviceAccountTokenCreator```
	- Create a Pub/Sub subscription so that the PDF converter can run whenever a message is published on the topic "new-doc".```gcloud beta pubsub subscriptions create pdf-conv-sub --topic new-doc --push-endpoint=$SERVICE_URL --push-auth-service-account=pubsub-cloud-run-invoker@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com```
	- 
- Can also Update the container. See the source link for this.













