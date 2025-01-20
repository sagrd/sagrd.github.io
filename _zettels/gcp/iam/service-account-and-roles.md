---
date: 2025-01-14
layout: zettel
category: show
tags:
  - gcp
  - iam
link: 
article-name: GCP Docs
---
- Service account 
	- belongs to application or a virtual machine instead of individual end user
	- application uses the service account to call google api of a service so that the users aren't directly involved
	- example: compute vm may run as a service account, and that account can be given permission to access the resources it needs.
	- Types of service account:
		- User managed service account:
			- when a new project is created and compute engine api is enabled for the project, a compute engine service account is created for you by default.
			- Its identifiable using this email `project-no-compute@developer.gserviceaccount.com`
			- If the project contains an app engine application; the email becomes something like `project_id@appsoft.gserviceaccount.com`
		- Google managed service account:
			- these service accounts are created and owned by Google mainly for running internal processes
			- represent different Google services and each account is automatically granted IAM roles to access your Google Cloud project.
			- looks something like `PROJECT_NUMBER@cloudservices.gserviceaccount.com`
- IAM Roles:
	- When an identity calls a Google Cloud API, it should have the appropriate permissions to use the resource. 
	- Permission is granted by: by granting roles to a user, a group, or a service account.
	- Three types of roles: 
		- **Primitive roles**, which include the Owner, Editor, and Viewer roles that existed prior to the introduction of Cloud IAM
		- **Predefined roles**, which provide granular access for a specific service and are managed by Google Cloud.
		- **Custom roles**, which provide granular access according to a user-specified list of permissions.
- Creating and managing service account:
	- Creating a service account: `gcloud iam service-accounts create my-sa-123 --display-name "my service account"`
	- Granting roles to service account: 
		- When granting IAM roles, you can treat a service account either as a [resource](https://cloud.google.com/iam/docs/overview#resource) or as an [identity](https://cloud.google.com/iam/docs/overview#concepts_related_to_identity).
		- ```gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
		    --member serviceAccount:my-sa-123@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/editor```















