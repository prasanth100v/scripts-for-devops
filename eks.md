✅ Final Script: AWS CLI + kubectl + eksctl (with unzip included)
#!/bin/bash

echo "==== Installing unzip package ===="
sudo yum install -y unzip 2>/dev/null || sudo apt-get install -y unzip

echo "==== Installing AWS CLI v2 ===="
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version

echo "==== Installing kubectl ===="
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.26.4/2023-05-11/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/kubectl
kubectl version --client

echo "==== Installing eksctl ===="
curl --silent --location \
"https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" \
| tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin/eksctl
eksctl version

echo "==== Installation Completed Successfully! ===="

🚀 How to Use
nano setup_eks_tools.sh
chmod +x setup_eks_tools.sh
./setup_eks_tools.sh
