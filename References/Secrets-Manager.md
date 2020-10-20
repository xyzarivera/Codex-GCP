# Secrets Manager

## Sensitive and Secret Data

- Database Password
- API KEy
- Auth Token
- Private Certs/Keys

- Do not store secrets in container images or in git

## Secret Manager

- Generally Avaialble
- Fully managed principle of least privilage
- TLS 
- AES-256
- versionign and lifecyle management
- full audit logging
- access via Cloud IAM

## Retrieval Methods

- Client Libraries
- REST API
- Environment Variables
  - Build-Time 
  - Runtime
    - script to inject secrets

## Multiple Secrets

- for multiple environment variables 
  - consider adding a startup script to your application container
- Cloud Run for Anthos allows direct injection of Kubernetes Secrets either as environment variables or mounted volumes
- Programmatic Access to secrets might be easier
- Make sure your service account has the Secret Manager Secret Accessor IAM role

## Programmatic Access using Python

``` python
import OS
from google.cloud import secretmanager

client = secretmanager.SecretManagerServiceClient()
secret_name = "my-secret"
project_id = os.environ["GCP_PROJECT"]
resource_name = "projecs/{project_id}/secrets/{secret_name}/versions/latest"
response = client.access_secret_version(resource_name)
secret_string = response.payload.data.decode('UTF-8')
```