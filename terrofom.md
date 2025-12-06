#!/usr/bin/env bash
set -euo pipefail

echo "=== Installing helper packages ==="
sudo yum install -y yum-utils gnupg2 wget unzip

echo "=== Downloading HashiCorp repo file ==="
TMP_REPO="/tmp/hashicorp.repo"
wget -q -O "$TMP_REPO" "https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo"

if [ ! -s "$TMP_REPO" ]; then
  echo "ERROR: failed to download repo file. Exiting."
  exit 1
fi

echo "=== Fixing repo for RHEL 10 (pointing to RHEL/9 path) ==="
# Replace occurrences of RHEL/$releasever (or $releasever) with the static 'RHEL/9' path
# This avoids $releasever expanding to '10' (which currently lacks repo metadata)
sudo sed -e 's|\$release/RHEL/\$releasever|RHEL/9|g' \
         -e 's|RHEL/\$releasever|RHEL/9|g' \
         -e 's|\$releasever|9|g' \
         "$TMP_REPO" | sudo tee /etc/yum.repos.d/hashicorp.repo > /dev/null

echo "=== Showing the resulting repo file (first 40 lines) ==="
sudo sed -n '1,40p' /etc/yum.repos.d/hashicorp.repo || true

echo "=== Cleaning metadata & refreshing repos ==="
sudo yum clean all || true
sudo yum makecache -y || true

echo "=== Installing Terraform ==="
sudo yum -y install terraform

echo "=== Terraform Version Installed ==="
terraform -v || true

echo "=== Done ==="
