

# gcloud-gke-vagrant-ubuntu

![enter image description here](https://lh3.googleusercontent.com/l8HRwjd2NZ5j6z4afkOz_LKXtJI2FG1Sd_T8BCmnqmFx1fJvMs5OerCPWk2wzRUQdOEMlGiKMTlGBA)

# About...

This setup is used to install ***prerequisites*** that are required to ***access/create/delete Google Kubernetes Engine***.

# Table of Contents

* [Prerequisites](#prerequisites)
* [Install Vagrant Box](#deploy)
* [Vagrant Box Details](#configuration)
* [Create GKE cluster](#create_cluster)
* [Access GKE cluster](#gke)
* [Delete GKE cluster](#delete_cluster)
* [Add-Ons provided](#addons)
* [Login Vagrant VM](#access)
* [Stop Vagrant VM](#stop)
* [Restart Vagrant VM](#restart)
* [Destroy Vagrant VM](#destroy)




<a id="prerequisites"></a>

# Prerequisites 
* Enable Virtualization(VT) in BIOS for Hyper-V 
* [Git](https://git-scm.com/downloads "Git") command line utility which is used to target an existing repository and create a **clone**, or copy of the target repository
* [Vagrant (Version >= 2.2.0)](https://www.vagrantup.com/downloads.html "Vagrant") is an open-source software product for building and maintaining portable virtual software development environments, e.g. for VirtualBox, Hyper-V, Docker containers, VMware, and AWS
* [Oracle VM VirtualBox (Version >= 6.0)](https://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html "Oracle Virtual Manger") lets you run multiple operating systems on Mac OS, Windows, Linux, or Oracle Solaris.
* Minimum laptop/desktop configuration  - 8GBRAM , 4CPU , support for VT-X



<a id="deploy"></a>

# Install Vagrant Box
 Default settings:`env.yaml`. These settings can be changed as per your requirements and the below are minimum requirements.
```yaml
VM:
  ip: 100.10.10.116
  cpus: 2
  memory: 2048
  vmname: gcloud-gke-ubuntu
  hostname: gcloud-gke-ubuntu.com
```
Open `windows (OR) bash` terminal from your `local windows` machine

* `$ cd gcloud-gke-vagrant-ubuntu/provisioning` 
* `$ git clone https://github.com/SubhakarKotta/gcloud-gke-vagrant-ubuntu.git` 
* `$ vagrant up`


<a id="configuration"></a>

# Vagrant Box Details

Name|IP|OS|RAM|CPU|
|----|----|----|----|----|
gcloud-gke-ubuntu  |100.10.10.116|Ubuntu 18.04|2G|2|


<a id="create_cluster"></a>

# Create GKE Cluster

**Login to vagrant box from your local machine**
* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant ssh gcloud-gke-ubuntu`

**Provide GCLOUD Credentials**
* `$ gcloud auth login`

 **[Create GKE Cluster](https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-cluster) by following the steps given in the link**

* `$ kubectl get nodes` [To verify kubectl is connected to aks cluster]


**[Access Kubernetes Dashboard](#access_dashboard) by following the steps given in the link**


<a id="access_dashboard"></a>

# Access Kubernetes Dashboard

From ***local windows system terminal*** execute the below commands

* `$ ssh -L 8001:localhost:8001 vagrant@100.10.10.116` [***password : vagrant***]

Use the below command to generate ***access token*** to login ***Dashboard***
* `$ kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode`

Start proxy to access kubernetes dashboard
* `$ kubectl proxy`

***Click !***
[http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/login](http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/login)


<a id="gke"></a>

# Access GKE Cluster

**Login to vagrant box from your local machine**
* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant ssh gcloud-gke-ubuntu`

**Provide GCLOUD Credentials**
* `$ gcloud auth login`

**Fetch/Update kubeconfig on your vagrant box**
* `$ gcloud container clusters get-credentials <YOUR_CLUSTER_NAME> --zone <YOUR_ZONE_NAME> --project <YOUR_PROJECT_NAME>`
* `$ kubectl get nodes` [To verify kubectl is connected to aks cluster]

**[Access Kubernetes Dashboard](#access_dashboard) by following the steps given in the link**


<a id="delete_cluster"></a>

# Delete GKE Cluster

**Login to vagrant box from your local machine**
* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant ssh gcloud-gke-ubuntu`

**Provide GCLOUD Credentials**
* `$ gcloud auth login`

**[Delete GKE Cluster](https://cloud.google.com/kubernetes-engine/docs/how-to/deleting-a-cluster) by following the steps given in the link**

<a id="addons"></a>

# Add-Ons provided
* `kubectl`
* `gcloud`
* `helm`

<a id="access"></a>

# Login Vagrant VM

**The Vagrant VM can be accessed in two ways from your local windows machine**

**vagrant ssh**
* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant ssh gcloud-gke-ubuntu`

**putty/mobaxterm**
* `100.10.10.116` [***vagrant/vagrant*** ]
	
          

<a id="stop"></a>

# Stop Vagrant VM

**Run the below command to stop the Vagrant Box from your local windows machine**

* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant halt`


<a id="restart"></a>

# Restart Vagrant VM

**Run the below command to restart the Vagrant Box if the vagrant box is stopped from your local windows machine**
* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant up`


<a id="destroy"></a>

# Destroy Vagrant VM

**Run the below command to delete the Vagrant Box from your local windows machine**
* `$ cd gcloud-gke-vagrant-ubuntu/provisioning`
* `$ vagrant destroy`
