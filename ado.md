# ADO

### ADO
- create stub gcp-bootstrap build 
- create build from repo
- check billing - currently 2 non-stakeholder users - https://learn.microsoft.com/en-us/azure/devops/organizations/billing/buy-basic-access-add-users?view=azure-devops
- purchase credits
- purchase parallelism https://aka.ms/azpipelines-parallelism-request

Alternate - revisit my work in
https://github.com/GoogleCloudPlatform/pbmm-on-gcp-onboarding/issues/399

- 6 repos
- branches per repo
- pipelines

#### ADO upstream sync to Github
https://learn.microsoft.com/en-us/azure/devops/repos/git/pushing?view=azure-devops&tabs=visual-studio-2022
```
michaelobrien@mbp8 olxyz % git clone git@ssh.dev.azure.com:v3/obrienlabsxyz/tef-gcp-pbmm-lz/gcp-bootstrap
michaelobrien@mbp8 olxyz % cd gcp-bootstrap 
michaelobrien@mbp8 gcp-bootstrap % git remote add github https://github.com/GoogleCloudZone/gcp-bootstrap
michaelobrien@mbp8 gcp-bootstrap % git pull github
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (5/5), 5.24 KiB | 1.31 MiB/s, done.
From https://github.com/GoogleCloudZone/gcp-bootstrap
 * [new branch]      main       -> github/main
 * [new branch]      plan       -> github/plan
 * [new branch]      production -> github/production
 * [new branch]      shared     -> github/shared
You asked to pull from the remote 'github', but did not specify a branch. 
michaelobrien@mbp8 gcp-bootstrap % git pull github main
From https://github.com/GoogleCloudZone/gcp-bootstrap
 * branch            main       -> FETCH_HEAD
michaelobrien@mbp8 gcp-bootstrap % git config pull.rebase true 
michaelobrien@mbp8 gcp-bootstrap % git pull github main        
From https://github.com/GoogleCloudZone/gcp-bootstrap
 * branch            main       -> FETCH_HEAD
Auto-merging .gitignore
CONFLICT (add/add): Merge conflict in .gitignore
Auto-merging README.md
CONFLICT (add/add): Merge conflict in README.md
michaelobrien@mbp8 gcp-bootstrap % vi README.md 
michaelobrien@mbp8 gcp-bootstrap % git add README.md          
michaelobrien@mbp8 gcp-bootstrap % git add .gitignore 
michaelobrien@mbp8 gcp-bootstrap % git remote -v
github	https://github.com/GoogleCloudZone/gcp-bootstrap (fetch)
github	https://github.com/GoogleCloudZone/gcp-bootstrap (push)
origin	git@ssh.dev.azure.com:v3/obrienlabsxyz/tef-gcp-pbmm-lz/gcp-bootstrap (fetch)
origin	git@ssh.dev.azure.com:v3/obrienlabsxyz/tef-gcp-pbmm-lz/gcp-bootstrap (push)
michaelobrien@mbp8 gcp-bootstrap % git rebase --continue
michaelobrien@mbp8 gcp-bootstrap % git push -u github main
To https://github.com/GoogleCloudZone/gcp-bootstrap
   222b2b8..f9cdc97  main -> main
branch 'main' set up to track 'github/main'.
```

## First ADO Pipeline build permissions


<img width="1957" height="680" alt="Screenshot 2025-12-08 at 18 16 24" src="https://github.com/user-attachments/assets/1d1da8ce-fc22-4f3a-a82d-3a5160e72160" />
