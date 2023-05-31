# CICD-Node.js
 CI/CD pipeline using AWS services like Amazon EKS (Elastic Kubernetes Service) and Amazon ECR (Elastic Container Registry) to build and deploy a Docker image. I have used AWS Code Pipeline and Codebuild for this Project
 Here's a breakdown of the different phases and commands in this configuration:
 
 install: This phase installs the necessary dependencies for the pipeline. It downloads kubectl (Kubernetes command-line tool) and adds it to the PATH. Then, it checks the version of kubectl using the kubectl version command.

pre_build: In this phase, the pipeline logs into Amazon EKS by updating the kubeconfig with the specified cluster name and region. It then checks the Kubernetes configuration and access by running kubectl config view --minify and kubectl get svc commands. Next, it logs into Amazon ECR using the AWS CLI command aws ecr get-login-password and pulls the latest Docker image from the specified repository URI.

build: This phase builds the Docker image. It runs the docker build command to build the image, using --cache-from option to leverage any existing layers from a previous build if available. The resulting image is tagged with the specified repository name and tag.

post_build: In the final phase, the pipeline pushes the Docker image to Amazon ECR using the docker push command. It then applies a Kubernetes deployment configuration from cicd/deployment.yaml file using kubectl apply. Finally, it restarts the deployment to deploy the latest image using kubectl rollout restart.
