# Retrieving from Secrets Manager during Build

must be checked first for multiple environment variables

## Saving Secrets to Secret Manager

1. Navigate to Security > Secret Manager.
2. Click Create Secret.
3. Enter Secrets Name
4. In the Secret value box, paste in the API key.
5. Click Create Secret.

## Enabling Cloud Build to access Secrets Manager

1. Click IAM & Admin.
2. Find the row with Cloud Build Service Account in the Role column.
3. Click the pencil icon on the far right of the Cloud Build Service Account row.
4. Click Add Another Role.
5. In the dropdown, select **Secret Manager Secret Accessor**.
6. Click Save.

## Update cloudbuild.yaml

``` yaml
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'gcr.io/$PROJECT_ID/image-gallery', '.']
- name: 'gcr.io/cloud-builders/docker'
  args: ['push', 'gcr.io/$PROJECT_ID/image-gallery']
- name: 'gcr.io/cloud-builders/gcloud'
  entrypoint: 'bash'
  args: [ '-c', 'gcloud secrets versions access latest --secret=gallery-apikey > decrypted.txt' ]
- name: 'gcr.io/cloud-builders/gcloud'
  args:
  - 'run'
  - 'deploy'
  - 'image-gallery'
  - '--image'
  - 'gcr.io/$PROJECT_ID/image-gallery'
  - '--region'
  - 'us-east1'
  - '--platform'
  - 'managed'
  - '--allow-unauthenticated'
- name: 'gcr.io/cloud-builders/gcloud'
  entrypoint: 'bash'
  args: [ '-c', 'gcloud run services update image-gallery --platform managed --region us-east1 --set-env-vars=API_KEY=$(cat decrypted.txt)' ]
images:
- 'gcr.io/$PROJECT_ID/image-gallery'
```


## Resources

[acloudguru](https://acloudguru.com/)
