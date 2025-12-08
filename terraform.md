## Terraform Install
- https://github.com/ObrienlabsDev/blog/issues/149
- https://github.com/ObrienlabsDev/gcp-infrastructure-as-code
### Terraform Install Mac
- https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
- versions on https://releases.hashicorp.com/terraform/ - https://releases.hashicorp.com/terraform/1.14.1/terraform_1.14.1_darwin_arm64.zip
### Use tfswitch
```
michaelobrien@mbp8 gcp-bootstrap % tfswitch
Use the arrow keys to navigate: ↓ ↑ → ← 
Select Terraform version
  ▸ 1.5.7 *recent
    1.13.3 *recent
    1.14.1
    1.14.0
↓   1.13.5`
michaelobrien@mbp8 gcp-bootstrap % tfswitch
✔ 1.14.1
10:48:10.825 INFO Selected Terraform version: 1.14.1  
10:48:10.854 INFO Installing Terraform version "1.14.1" for "darwin_arm64"  
10:48:10.854 INFO Downloading "https://releases.hashicorp.com/terraform/1.14.1/terraform_1.14.1_darwin_arm64.zip"  
10:48:10.854 INFO Downloading to "/Users/michaelobrien/.terraform.versions/terraform_1.14.1_darwin_arm64.zip"  
10:48:11.297 INFO 28705733 bytes downloaded  
10:48:11.299 INFO Downloading "https://releases.hashicorp.com/terraform/1.14.1/terraform_1.14.1_SHA256SUMS"  
10:48:11.299 INFO Downloading to "/Users/michaelobrien/.terraform.versions/terraform_1.14.1_SHA256SUMS"  
10:48:11.358 INFO 1392 bytes downloaded  
10:48:11.358 INFO Downloading "https://releases.hashicorp.com/terraform/1.14.1/terraform_1.14.1_SHA256SUMS.72D7468F.sig"  
10:48:11.358 INFO Downloading to "/Users/michaelobrien/.terraform.versions/terraform_1.14.1_SHA256SUMS.72D7468F.sig"  
10:48:11.404 INFO 566 bytes downloaded  
10:48:11.404 INFO Verifying PGP signature of checksum file: "/Users/michaelobrien/.terraform.versions/terraform_1.14.1_SHA256SUMS"  
10:48:11.408 INFO Checksum file PGP signature verification successful  
10:48:11.431 INFO Deleting "/Users/michaelobrien/.terraform.versions/terraform_1.14.1_SHA256SUMS"  
10:48:11.431 INFO Deleting "/Users/michaelobrien/.terraform.versions/terraform_1.14.1_SHA256SUMS.72D7468F.sig"  
10:48:11.727 WARNING Falling back to install to "/Users/michaelobrien/bin" directory  
10:48:11.728 WARNING Run `export PATH="$PATH:/Users/michaelobrien/bin"` to append "/Users/michaelobrien/bin/terraform" to $PATH  
10:48:11.728 INFO Switched Terraform to version "1.14.1"  
10:48:11.728 WARNING Run `export PATH="$PATH:/Users/michaelobrien/bin"` to append "/Users/michaelobrien/bin/terraform" to $PATH  
10:48:11.728 INFO Switched Terraform to version "1.14.1"  
michaelobrien@mbp8 gcp-bootstrap % terraform --version
zsh: command not found: terraform
michaelobrien@mbp8 gcp-bootstrap % vi ~/.bash_profile 
michaelobrien@mbp8 gcp-bootstrap % source ~/.bash_profile 
michaelobrien@mbp8 gcp-bootstrap % terraform --version   
Terraform v1.14.1
on darwin_arm64
```

## Gcloud Auth
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

## Terraform init
```
michaelobrien@mbp8 shared % terraform init                                     
Initializing the backend...

Successfully configured the backend "gcs"! Terraform will automatically
use this backend unless the backend configuration changes.
Initializing modules...
Initializing provider plugins...
- Finding hashicorp/time versions matching ">= 0.5.0"...
- Finding hashicorp/null versions matching ">= 2.1.0"...
- Finding hashicorp/google versions matching ">= 3.43.0, >= 3.50.0, >= 3.53.0, >= 3.64.0, >= 3.67.0, >= 3.77.0, >= 4.28.0, < 6.0.0, < 7.0.0, < 8.0.0"...
- Finding hashicorp/random versions matching ">= 2.2.0, >= 3.1.0"...
- Finding hashicorp/google-beta versions matching ">= 3.43.0, >= 3.64.0, >= 3.67.0, >= 3.77.0, >= 4.11.0, >= 4.28.0, < 6.0.0, < 8.0.0"...
- Installing hashicorp/random v3.7.2...
- Installed hashicorp/random v3.7.2 (signed by HashiCorp)
- Installing hashicorp/google-beta v5.45.2...
- Installed hashicorp/google-beta v5.45.2 (signed by HashiCorp)
- Installing hashicorp/time v0.13.1...
- Installed hashicorp/time v0.13.1 (signed by HashiCorp)
- Installing hashicorp/null v3.2.4...
- Installed hashicorp/null v3.2.4 (signed by HashiCorp)
- Installing hashicorp/google v5.45.2...
- Installed hashicorp/google v5.45.2 (signed by HashiCorp)
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```
