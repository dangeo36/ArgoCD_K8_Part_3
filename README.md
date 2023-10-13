# ArgoCD_K8

The goal of this project is to automate Kubernetes manifest files with ArgoCD and Jenkins. The CI portion of the pipeline will build Docker images of a Java application and push them to Amazon ECR. Images are pushed with a build number (or tag) that can be referenced later in the CD portion. The CD portion will pull the latest tag and update the Kube manifest files. Once everything is properly updated, ArgoCD will monitor the latest changes in the pipeline and update accordingly.

## Part 3 

For this part of the project, we will be using Jenkins to build out a CD pipeline. The repository contains Kubernetes manifest files. We have an app-deploy file that is responsible for deploying our container image (updated in ECR). There are also files for secrets, persistent volumes, services, databases, and config maps. Using kubectl we can apply these files in our EKS cluster. 

This pipeline is triggered by the CI one mentioned in part 2. Once triggered, the Jenkinsfile includes steps to fetch and update the app-deploy.yml file with the current image's build number. The pipeline updates the deployment file and then pushes the code to Github. After the code is pushed, ArgoCD (already installed and ready to go) monitors and makes adjustments. 

## Tools / Dependencies
For this part, I have an Amazon EC2 instance (Ubuntu 20.04, t2.medium) that has Java 17, Jenkins, Terraform, awcli (configured with proper credentials), kubectl, and Docker. Jenkins needs proper plugins and credentials to access AWS and the Github repository. 
