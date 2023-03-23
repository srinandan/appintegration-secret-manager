# Access Secret Manager 

This sample repository demonstrates how to a secret in secret manager from [Application Integration](https://cloud.google.com/application-integration/docs/overview).

# Prerequisites

* The integration version JSON is downloaded [here](./src/executeworkflows.json)
* This repo uses a custom cloud builder called `integrationcli-builder`. , based on [integrationcli](https://github.com/GoogleCloudPlatform/application-integration-management-toolkit) and gcloud

# Configuring Cloud Build

In the setting page of Cloud Build enable the following service account permissions:
* Secret Manager (Secret Manager Accessor)
* Service Accounts (Service Account User)
* Cloud Build (Cloud Build WorkerPool User)

Grant the Application Integration Admin role to the Cloud Build Service Agent

```
    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-cloudbuild.iam.gserviceaccount.com" \
        --role="roles/integrations.integrationAdmin"
```

## Steps

1. Modify  the [overrides file](./overrides/overrides.json) to set the appropriate details for project id and secret name.

2. Modify the [authconfig file](./authconfig/executeworkflows-authconfig.json) to set the appropriate Service Account with permissions to execute a Workflow. Replace the following string

```
"serviceAccount": "<sa-name>@<project-id>.iam.gserviceaccount.com",
```

3. Trigger the build manually

```sh

gcloud builds submit --config=cloudbuild.yaml --region=<region-name> --project=<project-name>
```

The integration is labeled with the `SHORT_SHA`, the first seven characters of the commit id
___

## Support

This is not an officially supported Google product
