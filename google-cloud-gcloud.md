## Google Cloud Auth
```
michaelobrien@mbp8 shared %  gcloud auth application-default login 
michaelobrien@mbp8 gcp-bootstrap % cat ~/.config/gcloud/application_default_credentials.json 
{
  "account": "",
  "client_id": "76...hur.apps.googleusercontent.com",
  "client_secret": "d-F...y",
  "quota_project_id": "lz-...-ot",
  "refresh_token": "1//0...JI",
  "type": "authorized_user",
  "universe_domain": "googleapis.com"
}%                                          
```


## Service Account Impersonation

```
export SA_PROJECT=prj-...
gcloud config set project $SA_PROJECT
export SA_EMAIL=sa-terraform-net@$SA_PROJECT.iam.gserviceaccount.com
# only outside cloud shell
gcloud auth login

gcloud config set auth/impersonate_service_account $SA_EMAIL
gcloud auth application-default login --impersonate-service-account $SA_EMAIL

```
