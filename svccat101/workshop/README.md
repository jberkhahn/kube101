# An introduction to Kubernetes Service Catalog

[Service Catalog](https://github.com/kubernetes-incubator/service-catalog) lets you provision cloud services and attach them to running Kubernetes deployments 
without having to manage those resources directly. This is done through the use of a broker, a web
server that implements the [Open Service Broker API](https://www.openservicebrokerapi.org/).

# Objectives
These labs are a introduction to the installation and use of Service Catalog using an installation of IBM Cloud Private. By the end of this course, you'll know:
* Understand the core concepts of the Open Service Broker API
* Deploy a service broker, attach it to your Kubernetes deployment, and use it to provision services
* Consume those services in your applications running on Kubernetes

# Prerequesites
* Have completed [Kube101](https://github.com/IBM/kube101/tree/master/workshop).
* Have a running Kubernetes cluster as per Kube101
* A Pay-As-You-Go or Subscription [IBM Cloud account](https://console.bluemix.net/registration/)
