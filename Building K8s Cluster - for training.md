Building K8s Cluster - for learning 


Assuming Ubuntu image (Other distributions change 'apt' to 'yum', etc.)

First things first
	We need to get images and tools from Docker and Google[Kubernetes]. So it is prudent to add the their public key, and include their API repository to the system. 

	Let us import gpg key and add to API repository for Docker
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"
```

Let us do the same for Kubernetes/Google 

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

Now it is time to install Docker and Kubernetes packages. Here are the four packages to be installed:
	1. docker 
	2. kubelet 
	3. kubeadm 
	4. kubectl 

### Note: Version of kube* should all be the same 

trick: to avoid accidentally upgrading these packages as part of a regular maintenance apt-get update, mark them as <code>hold<code>

```
sudo apt-get update
# K8s 1.14 versions
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu kubelet=1.14.5-00 kubeadm=1.14.5-00 kubectl=1.14.5-00

# K8s 1.18.12 versions 
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu kubelet=1.18.12-00  kubeadm=1.18.12-00 \ 
kubectl=1.18.12-00

sudo apt-mark hold docker-ce kubelet kubeadm kubectl
```