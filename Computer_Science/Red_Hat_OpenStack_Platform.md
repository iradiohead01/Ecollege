# Red Hat OpenStack Platform

>The Red Hat OpenStack Platform director is a toolset for installing and managing a complete OpenStack
environment.

[Basic Architecher](./arch.png)

## Undercloud

### Introduction

* Environment Planning
* Bare Metal System Control
* Orchestration (YAML templates)
* Command Line Tools and a Web UI
* Undercloud Components
  * OpenStack Identity (keystone) - Provides authentication and authorization for the director’s components.
  * OpenStack Bare Metal (ironic) and OpenStack Compute (nova) - Manages bare metal nodes.
  * OpenStack Networking (neutron) and Open vSwitch - Controls networking for bare metal nodes.
  * OpenStack Image Service (glance) - Stores images that are written to bare metal machines.
  * OpenStack Orchestration (heat) and Puppet - Provides orchestration of nodes and configuration of nodes after the director writes the overcloud image to disk.
  * OpenStack Telemetry (ceilometer) - Performs monitoring and data collection. This also includes:
    * OpenStack Telemetry Metrics (gnocchi) - Provides a time series database for metrics.
    * OpenStack Telemetry Alarming (aodh) - Provides a an alarming component for monitoring.
  * OpenStack Workflow Service (mistral) - Provides a set of workflows for certain directorspecific actions, such as importing and deploying plans.
  * OpenStack Messaging Service (zaqar) - Provides a messaging service for the OpenStack Workflow Service.
  * OpenStack Object Storage (swift) - Provides object storage for various OpenStack Platform components, including:
    * Image storage for OpenStack Image Service
    * Introspection data for OpenStack Bare Metal
    * Deployment plans for OpenStack Workflow Service

### Installation

1. Creating a director installation user  

Use the following commands to create the user named stack and set a password:
> d[root@director ~]# useradd stack  
> [root@director ~]# passwd stack # specify a password

Disable password requirements for this user when using sudo:
> [root@director ~]# echo "stack ALL=(root) NOPASSWD:ALL" | tee -a
/etc/sudoers.d/stack  
> d[root@director ~]# chmod 0440 /etc/sudoers.d/stack

Switch to the new stack user:
> [root@director ~]# su - stack  
> [stack@director ~]$

Continue the director installation as the stack user.

2. CREATING DIRECTORIES FOR TEMPLATES AND IMAGES

> $ mkdir ~/images  
> $ mkdir ~/templates

3. SETTING THE HOSTNAME FOR THE SYSTEM

use hostnamectl to set a hostname:
> $ sudo hostnamectl set-hostname manager.example.com  
> $ sudo hostnamectl set-hostname --transient manager.example.com

Then /etc/hosts requires an entry like:

> 127.0.0.1 manager.example.com manager localhost localhost.localdomain
localhost4 localhost4.localdomain4

4. REGISTERING YOUR SYSTEM

Register your system with the Content Delivery Network, entering your Customer Portal user name and
password when prompted:

> $ sudo subscription-manager register

Find the entitlement pool ID for Red Hat OpenStack Platform director.

>$ sudo subscription-manager list --available --all --matches="*OpenStack*"
Subscription Name: Name of SKU
Provides: Red Hat Single Sign-On
Red Hat Enterprise Linux Workstation
Red Hat CloudForms
Red Hat OpenStack
Red Hat Software Collections (for RHEL Workstation)
Red Hat Virtualization
SKU: SKU-Number
Contract: Contract-Number
**Pool ID: Valid-Pool-Number-123456**
Provides Management: Yes
Available: 1
Suggested: 1
Service Level: Support-level
Service Type: Service-Type
Subscription Type: Sub-type
Ends: End-date
System Type: Physical

>$ sudo subscription-manager attach --pool=Valid-Pool-Number-123456


## Overcloud

**3 types overcloud node roles**

* Controller
> A default Controller node contains the following components:
> * OpenStack Dashboard (horizon)
> * OpenStack Identity (keystone)
> * OpenStack Compute (nova) API
> * OpenStack Networking (neutron)
> * OpenStack Image Service (glance)
> * OpenStack Block Storage (cinder)
> * OpenStack Object Storage (swift)
> * OpenStack Orchestration (heat)
> * OpenStack Telemetry (ceilometer)
> * OpenStack Telemetry Metrics (gnocchi)
> * OpenStack Telemetry Alarming (aodh)
> * OpenStack Clustering (sahara)
> * OpenStack Shared File Systems (manila)
> * OpenStack Bare Metal (ironic)
> * MariaDB
> * Open vSwitch
> * Pacemaker and Galera for high availability services.

* Compute
> A default Compute node contains the following components:
> * OpenStack Compute (nova)
> * KVM/QEMU
> * OpenStack Telemetry (ceilometer) agent
> * Open vSwitch

* Storage
> Nodes that provide storage for the OpenStack environment. This includes nodes for:
> * Ceph Storage nodes
> * Block storage (cinder)
> * Object storage (swift)
