## SSH Connection Command For GitBash Terminal:
```
ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
```
## ✅ scripts-for-devops (🚀 How to Use)
```
vi eks tools setup.sh
chmod +x eks tools setup.sh
./eks tools setup.sh
```

## ✅ Delete EKS Cluster using eksctl (Most Common)
```
eksctl delete cluster --name eks-cluster --region ap-south-1
```
## ✅ Create EKS Cluster using eksctl command
```
eksctl create cluster -f ekscluster.yml
```
#✅ Create an IAM OIDC provider in your AWS account
#✅ Associate it with  (eks-cluster) = Enable IRSA (IAM Roles for Service Accounts)
```
eksctl utils associate-iam-oidc-provider \
  --cluster eks-cluster \
  --region ap-south-1 \
  --approve
```
a
```
AKIA5327P5HQMKY26DOB
```
s
```
MXLPC6vnVTSfe3tk8FeSlsLRXChG2x7+sivVfxb/---
```
