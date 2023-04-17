# EKS-bastion-modules
## Deploy `Vault` For `EKS` Cluster Using Vault Image From `Elastic Container Registry ECR`
# DOCUMENTATION `Steps` and `Commands`:
_______________________________________________________________________________
##### This Terraform project creates a custom VPC with public and private subnets, an EC2 bastion host with a security group in the public subnet, an EKS cluster with a network interface in the public subnet, and two EKS node groups in the public and private subnets. IAM roles are created for the EKS cluster and node groups, and the necessary policies are attached to them. Additionally, a null resource with remote-exec is used to copy the pem key to the bastion host so that the admin can access the node group from the bastion host. An Elastic IP is also allocated to the bastion host to provide a static public IP address.
note:
You must also have AWS credentials set up on your local machine. <br>
creat a key-value pair named "eks-terraform-key" and copy the pem file to `private-key/eks-terraform-key.pem`
and This command creates a parameter named `eks-terraform-key` with the value `your_value_here` and data type `String`.
```
aws ssm put-parameter --name "eks-terraform-key" --value "your_value_here" --type "String"
```
then to get the value of a key-value pair, you can use the aws ssm get-parameter command
```
aws ssm get-parameter --name "eks-terraform-key"
```
#This command retrieves the value of the parameter named `eks-terraform-key`
# Details

## VPC

The VPC is created using the `vpc` Terraform module, which sets up a custom VPC with two public subnets and two private subnets. the subnets are associated with a routing table that routes traffic to the Internet Gateway for the public subnets and the NAT Gateway for the private subnets.

## EC2 Bastion Host

The EC2 bastion host is created using the bastion Terraform module, which uses the `ec2_instance` module to create the instance. The bastion host is placed in a security group that allows incoming SSH traffic from the user's IP address. An Elastic IP is allocated to the bastion host to provide a static public IP address.

Additionally, a `null resource` is used with `remote-exec` to copy the pem key to the bastion host so that the admin can access the node group from the bastion host.

## EKS Cluster

The EKS cluster is created using the `aws_eks_cluster` Terraform resource and includes a network interface in the public subnet. The IAM role for the EKS cluster is created using the iam Terraform module, and the necessary policies are attached to the role using the iam_policy_attachment resource.

## EKS Node Groups

Two EKS node groups are created, one in the public subnet and one in the private subnet. The node groups are created using the `eks_node_group` Terraform resource, and the necessary IAM roles are created using the `aws_iam_role` role  and attached to the node groups using the `aws_iam_role_policy_attachment` resource.

## 1-Configure mypc with aws account
```
brew install awscli
cat .aws/credentials
vim .aws/credentials #then put awsaccount iam user credentials accses and secret keys
brew install terraform
brew install helm
brew install kubectl
terraform init
terraform plan 
terraform apply
```
## 2-Creating or updating a kubeconfig file for an Amazon EKS cluster (configure mypc with eks cluster)
```
aws eks update-kubeconfig --region <region code> --name <cluster name>
kubectl get svc
```
## 3-Deploy Vault for EKS cluster 
  
