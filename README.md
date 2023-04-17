# EKS-bastion-modules
## Deploy `Vault` For `EKS` Cluster Using Vault Image From `Elastic Container Registry ECR`
# DOCUMENTATION `Steps` and `Commands`:
_______________________________________________________________________________
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
  
