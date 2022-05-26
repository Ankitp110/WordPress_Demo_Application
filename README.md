# WordPress_Demo_Application
This Repo is Prepared to present a demo of Wordpress Application to the the representatives of Allianz Technology.

Step-01: Create EKS Cluster using eksctl in AWS environment
         
Prerequisite is to have the AWS CLI installed in your local to configure in which acccount the EKS cluster will be created. Once you have an IAM user and AWS CLI installed in your local, we have to fire a command -:
         
         aws configure
         AWS Access Key ID [None]: (Replace your creds when prompted)
         AWS Secret Access Key [None]: (Replace your creds when prompted)
         Default region name [None]: us-east-1
         Default output format [None]: json

Please note we have to use our own AWS credentials here for the IAM user that you just created. DO NOT USE ROOT CREDENTIALS FOR THE ROOT AWS ACCOUNT.
Another Prerequisite is to have the EKSCTL and KUBECTL binary installed in your local desktop. Kindly run the below commands to have the EKSCTL and KUBECTL binary installed in your machine.

          mkdir kubectlbinary
          cd kubectlbinary
          curl -o kubectl.exe https://amazon-eks.s3.us-west-2.amazonaws.com/1.16.8/2020-04-16/bin/windows/amd64/kubectl.exe

Update the system Path environment variable 
   
           C:\Users\ANKIT\Documents\kubectlbinary

Verify the kubectl client version by firing the command 
 
           kubectl version --client

To Install EKSCTL on windows or linux, Please follow the documentation below -

           https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html#installing-eksctl

Final step here is to have a complete EKS cluster in AWS with preoper master and worker nodegroups. Please fire the command from your local.

           eksctl create cluster --name=eksdemo1 \
                      --region=us-east-1 \
                      --zones=us-east-1a,us-east-1b \
                      --without-nodegroup

In next step, we are adding the worker node group to our "eksdemo1" cluster

           eksctl create nodegroup --cluster=eksdemo1 \
                       --region=us-east-1 \
                       --name=eksdemo1-ng-public1 \
                       --node-type=t3.medium \
                       --nodes=2 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=kube-demo \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --alb-ingress-access 

Here we are creating a EKS cluster with name "eksdemo1" with 2 desired worker noddes. The Cluster is confired in "us-east-1" region and within two AZ's which are us-east-1a,us-east-1b. We also have a EC2 key pairs to work with worker nodes in case we need to SSH into our worker nodes.

Verify from your local terminal if everything is working as expected.

                     # List EKS clusters
                     eksctl get cluster

                     # List NodeGroups in a cluster
                     eksctl get nodegroup --cluster=<clusterName>

                     # List Nodes in current kubernetes cluster
                     kubectl get nodes -o wide

Step-02: Creating the Kubernetes Manifests files for our WordPress application.

The structure of our application is we are running a backend with mysql server and our frontend wordpress application will talk to the mysql backend and the data will be stored in the mysql DB in case we create any data from frontend.

I have written all the kube manifests files for mysql server and wordpress application. You can see all the manifests files by navigating to path WordPress_Demo_Application/Kubemanifests_files/ in master branch.
The structure of my application is something like -:

                   ![image](https://user-images.githubusercontent.com/26731929/170404378-a01c7b72-2658-45e6-8340-8b895483efe2.png)

The explanation for each of the files will be given when I am attending my interview. For now, our frontend is communicating to the backend and our application is exposed to the outer world using LoadBalancer service. 
