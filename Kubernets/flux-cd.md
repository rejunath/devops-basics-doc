# Flux CD:

### what is Flux-CD
1. Flux Cd is also a continuous deployment tool which automates deployments in kubernetes cluster as part of GITOPS
2. It is a simple and an easy tool for integration with kubernetes cluster.
3. As part flux CD we don't have any dashboard to display continuous deployment process
4. It main source is GITHUB where as you will commit new images in the kubernetes manifest files → flux will pickup the updated image and deploy the new pods.
5. In addition to github, Flux integrates with popular Git providers to simplify the initial setup of deploy keys and other authentication mechanisms:GitHub
GitLab
Bitbucket
AWS CodeCommit
Azure DevOps
Google Cloud Source
Oracle Cloud Git Repositories
