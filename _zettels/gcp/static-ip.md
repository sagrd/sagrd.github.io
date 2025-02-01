---
date: 2025-01-28
layout: zettel
category: show
tags:
  - gcp
title:
---
- First, reserving static ip causes extra money.
- create two ip address with following cmd
```
gcloud compute addresses create $USED_IP --project=$PROJECT_ID --region=us-west1
gcloud compute addresses create $UNUSED_IP --project=$PROJECT_ID --region=us-west1
```
- Confirm the two address were created
```
gcloud compute addresses list --filter="region:(us-west1)"
```
- Export the ip in variable
```
export USED_IP_ADDRESS=$(gcloud compute addresses describe $USED_IP --region=us-west1 --format=json | jq -r '.address')
```
- To use the ip: Create a compute instance
```
gcloud compute instances create static-ip-instance \
--zone=us-west1-a \
--machine-type=e2-medium \
--subnet=default \
--address=$USED_IP_ADDRESS
```
