# Running Jenkins in Kubernetes (AWS)
Installing Jenkins CI in Kubernests and building containers with Kaniko
## Prerequsites 
- Virtual Machine running Ubuntu 22.04 or newer
### Update Package Repository and Upgrade Packages
``` shell title="Run from shell prompt" linenums="1"
sudo apt update
sudo apt upgrade
```
## Create Kubernetes Cluster
``` shell title="Run from shell prompt" linenums="1"
sudo bash
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="server" sh -s - --disable traefik
exit 
mkdir .kube
sudo cp /etc/rancher/k3s/k3s.yaml ./config
sudo chown dmistry:dmistry config
chmod 400 config
export KUBECONFIG=~/.kube/config
```

## Installs Jenkins
Install helm chart and update repo
``` shell title="Run from shell prompt" linenums="1"
helm repo add jenkinsci https://charts.jenkins.io
helm repo update
```

### Create Namespace
``` shell title="Run from shell prompt"
kubectl create ns jenkins
```

### Download YAML files
``` shell title="Run from shell prompt"
wget https://raw.githubusercontent.com/dmancloud/jenkins-kubernetes-kaniko/main/jenkins-sa.yaml
wget https://raw.githubusercontent.com/dmancloud/jenkins-kubernetes-kaniko/main/jenkins-volume.yaml
wget https://raw.githubusercontent.com/dmancloud/jenkins-kubernetes-kaniko/main/values.yaml
```

### Create a secret for Dockerhub
``` shell title="Run from shell prompt"
kubectl create secret docker-registry docker-credentials --docker-username=[userid] --docker-password=[Docker Hub access token] --docker-email=[user email address] --namespace jenkins
```
### Finally install Jenkins CI

``` shell title="Run from shell prompt"
helm upgrade --install jenkins jenkinsci/jenkins -n jenkins --create-namespace -f values.yaml
```

