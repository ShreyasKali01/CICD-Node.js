# CICD-Node.js
 CI/CD pipeline using AWS services like Amazon EKS (Elastic Kubernetes Service) and Amazon ECR (Elastic Container Registry) to build and deploy a Docker image. I have used AWS Code Pipeline and Codebuild for this Project
 Here's a breakdown of the different phases and commands in this configuration:
 
 install: This phase installs the necessary dependencies for the pipeline. It downloads kubectl (Kubernetes command-line tool) and adds it to the PATH. Then, it checks the version of kubectl using the kubectl version command.

pre_build: In this phase, the pipeline logs into Amazon EKS by updating the kubeconfig with the specified cluster name and region. It then checks the Kubernetes configuration and access by running kubectl config view --minify and kubectl get svc commands. Next, it logs into Amazon ECR using the AWS CLI command aws ecr get-login-password and pulls the latest Docker image from the specified repository URI.

build: This phase builds the Docker image. It runs the docker build command to build the image, using --cache-from option to leverage any existing layers from a previous build if available. The resulting image is tagged with the specified repository name and tag.

post_build: In the final phase, the pipeline pushes the Docker image to Amazon ECR using the docker push command. It then applies a Kubernetes deployment configuration from cicd/deployment.yaml file using kubectl apply. Finally, it restarts the deployment to deploy the latest image using kubectl rollout restart.

AWS EKS
Amazon Elastic Kubernetes Service (Amazon EKS)
makes it easy to deploy, manage, and scale containerized
applications using Kubernetes on AWS.
Amazon EKS runs the Kubernetes management
infrastructure for you across multiple AWS availability
zones to eliminate a single point of failure. Amazon EKS
is certified Kubernetes conformant so you can use
existing tooling and plugins from partners and the
Kubernetes community. Applications running on any
standard Kubernetes environment are fully compatible
and can be easily migrated to Amazon EKS.
Amazon EKS is generally available for all AWS

Benefits
Let’s discuss in short what features it
provides
➔ No Control plane to manage
➔ Secure by default
➔ Comformant and Compatible
➔ Optimized for cost
➔ Build with the community

Cost
Let’s discuss about the cost
➔ Each EKS Cluster Cost
$0.10/hour i.e. $73/month
You can use a single Amazon EKS cluster to
run multiple applications by taking advantage
of Kubernetes namespaces and IAM security
policies.
➔ EC2 Instances & EBS volumes
used in AS Worker Nodes
You pay for AWS resources , you create to run
your Kubernetes worker nodes. You only pay
for what you use, as you use it; there are no
minimum fees and no upfront commitments

![image](https://github.com/ShreyasKali01/CICD-Node.js/assets/90476042/9deb8ea6-adaf-4412-bc6a-b48d88ee1759)

Install Essential Tools
We will need below tools to be installed
➔ Install aws cli
https://docs.aws.amazon.com/cli/latest/userg
uide/cli-chap-install.html (install cli v2)
➔ Install kubectl
https://docs.aws.amazon.com/eks/latest/user
guide/install-kubectl.html
➔ Install aws-iam-authenticator
https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html
➔ Install eksctl
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html  or
https://eksctl.io/introduction/installation/

