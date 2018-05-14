# Lab 0: Install Service Catalog and svcat

Before we begin, we need to install Service Catalog and its associated CLI utility, svcat.
Towards that end, this lab contains instructions to install:

* The Helm CLI, version 2.7.0 or later
* The Helm tiller pod inside your cluster
* Service Catalog, version 0.1.18 or later
* svcat, the Service Catalog CLI tool

# Install Helm

1. Download and install [the Helm CLI](https://github.com/kubernetes/helm#install).
2. Run `helm init` to install the tiller pod into your kube cluster. This pod is Helm's entry point
for creating additional infrastructure inside your cluster.
3. To allow the tiller pod permissions to perform changes inside your cluster, run
`kubectl create clusterrolebinding tiller-cluster-admin \
    --clusterrole=cluster-admin \
    --serviceaccount=kube-system:default
`

# Install Service Catalog

Service Catalog is installed via a Helm chart, a manifest that describes what to install and how to run it.

1. First, add the Service Catalog repo to your helm by running `helm repo add svc-cat https://svc-catalog-charts.storage.googleapis.com`
It should show up when you run `helm search service-catalog`.
2. Install Service Catalog by running 
`helm install svc-cat/catalog \
    --name catalog --namespace catalog`
It should show up when you run `kubectl get pods --all-namespaces`

# Install svcat

svcat is a command line tool for interacting with Service Catalog. It can be run as a kubectl plugin, or as a standalone binary.
Download the version that corresponds to your operating system:

* [Linux](https://download.svcat.sh/cli/latest/linux/amd64/svcat)
* [OS X](https://download.svcat.sh/cli/latest/darwin/amd64/svcat)
* [Windows](https://download.svcat.sh/cli/latest/windows/amd64/svcat.exe)

Make the binary executable:

* (Linux/OS X) `chmod +x svcat`
* (Windows) Make sure the filename ends in .exe

Move the file somewhere on your PATH:

* (Linux/OS X) `mv svcat /usr/local/bin/`
* (Windows) `mkdir -f ~\bin
$env:PATH += ";${pwd}\bin"`
