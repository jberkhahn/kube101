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

# Open Service Broker API
Cloud native applications are ephemeral and have often have no local stable storage, while still requiring access to the host
of databases, caches, email systems, billing systems, etc. in order to function. OSBAPI is an open API that allows the concerns
of provisioning and maintaining these services to be abstracted away from the application developer and the cloud platform provider.
While the archetypal example is a relational databse, anything that can be decomposed into the five OSB actions can be provided as an
OSB service.

# Open Service Broker Objects
OSBAPI defines five object types - Brokers, Services, Plans, Instances, and Bindings.
* Broker - A server that implements OSB API. Offers a catalog of services via the endpoints outlined in the OSB API specification, e.g. MySQL Broker.
* Service - A category of services offered by a broker, e.g. MySQL databases.
* Plan - A specific type of an offered service, e.g. 100 MB MySQL databases.
* Instance - A specific instantiation of a plan, e.g. Jonathan's 100 MB MySQL database.
* Binding - A unique set of credentials to access a specific instance , e.g. username/password/hostname/port to access Jonathan's 100 MB MySQL database.

# Open Service Broker Endpoints
The [OSBAPI specification](https://github.com/openservicebrokerapi/servicebroker) details the endpoints that must be implemented by a broker.
* GET /v2/catalog
Returns the catalog of services and plans offered by the broker. The platform is expected to maintain this list locally, but the catalog may
be refetched to get updates.
* PUT /v2/service_instances/:instance_id
Provision an instance of some service. Instance ID is some unique identifier that the platform provides. As brokers are intended to be stateless,
the platform must maintain a record of the instance IDs for provisioned services.
* PUT /v2/service_instances/:instance_id/service_bindings/:binding_id
Create a binding for some service instance. Binding ID is some unique identifier that the platform provides and must keep track of internally.
The response to this call contains a credentials JSON that contains the information on how to access the service instance that must be stored locally
by the platform.
* DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id
Delete the binding associated with binding ID. Depending on how the broker is implemented, this might cause subsequent requests to the instance
using the credentials contained in the binding to fail.
* DELETE /v2/service_instances/:instance_id
Unprovision the service instance associated with instance ID.

# Open Service Broker Lifecycle

XXXXX put in pictures here
