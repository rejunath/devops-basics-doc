# Flux CD:

### what is Flux-CD
- Flux Cd is also a continuous deployment tool which automates deployments in kubernetes cluster as part of GITOPS
- It is a simple and an easy tool for integration with kubernetes cluster.
- As part flux CD we don't have any dashboard to display continuous deployment process
- It main source is GITHUB where as you will commit new images in the kubernetes manifest files → flux will pickup the updated image and deploy the new pods.
- In addition to github, Flux integrates with popular Git providers to simplify the initial setup of deploy keys and other authentication mechanisms:GitHub
   - GitLab
   - Bitbucket
   - AWS CodeCommit
   - Azure DevOps
   - Google Cloud Source
   - Oracle Cloud Git Repositories

### How Flux-CD works
- Fluc Cd monitors your repo for any change and then sync the changes with kube cluster
- There by implementing Continuous Deployment process where as the user commits in the repo, the application is deployed.
- Flux can connect to any github repo any branch and reconcile the changes and deploy new application

### Components
- 3 Main components of flux which has to be installed and integrated with GITHUb repo
   - *Kubernetes API*: Responsible to complete the bootstrap process of connecting with github, creating a new repo and creating the YAML files of all the components of Flux.
   - *Source Controller*: Responsible for monitoring changes in the source repository   whenever there is a commit
   - *Kustomize controller*: It is responsible to connect to custom repositories and custom branches on the github account for your manifest files

### Commands
- flux bootstrap github --owner=*github_user* --repository=*repo_name* --path=*path_in_repo* --personal=true --private=false

  - --owner	
     - GitHub username or organization name that owns the repository.	
     - eg: --owner=john-doe
  - --repository	
     - Name of the GitHub repository to store Flux configurations. Created if it doesn’t exist.	
     - eg: --repository=prod-cluster
  - --path	
     - Directory in the repo where Flux configurations are stored (e.g., Kustomize files).	
     - eg: --path=clusters/production
  - --personal	
     - Set to true if the repository belongs to a personal GitHub account (default: false).	
     - eg: --personal=true
  - --private	
     - Set to false to make the repository public (default: true for private repos).	--private=false
  
  #### Workflow Overview
      1. Prerequisites
        - Flux CLI installed.
        - kubectl configured to access your Kubernetes cluster.
        - GitHub Personal Access Token (PAT) with: repo scope *(full control of repositories)*, *admin:public_key* scope (to add deploy keys).

  #### Command Execution
       1. Cluster Setup:
         - Installs Flux components (source-controller, kustomize-controller, etc.) in the flux-system namespace.
         - Creates a GitRepository and Kustomization resource to sync the specified --path.

  #### GitHub Interaction:
        - Creates the repository if it doesn’t exist (public/private based on --private).
        - Adds a deploy key to the repository for read/write access.
        - Commits initial Flux manifests (e.g., flux-system configs) to the --path directory.

  #### Post-Bootstrap
        - Flux continuously monitors the repository and syncs changes to the cluster.
        - Add Kubernetes manifests (YAML/Helm/Kustomize) to the --path directory to manage workloads.

  #### Example Command
        - flux bootstrap github \
          --owner=john-doe \
          --repository=prod-cluster \
          --path=clusters/production \
          --personal=true \
          --private=false
  #### Next Steps
        - Add Kubernetes manifests (e.g., deployments, services) to the --path directory.
        - Monitor sync status:
            - flux get kustomizations

### Difference between ArgoCd and Flux CD
- Both are working to provide continuous delivery by integrating with GIT
- Both are providing deploying of application on kubernetes cluster each time there is commit to your repo
- Both are dependent on manifests files/YAML files in github
- In both the cases the YAML files are present in the github
- ARGO CD comes with a versatile UI which allows you to visualize your app deployments.
- Flux CD does not have any UI-> everything is managed via kubernetes master node
- ArgoCD all components are present on kubernetes cluster
- Flux CD is tightly integrated with one specific github repository where flux-system YAML field are present
- FLux CD directly works with kubernetes API to connect to its components.

