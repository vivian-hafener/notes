# Slinky
---------

## Overview
-----
Slinky brings slurm functionality into Kubernetes - allowing simultaneous management of traditional HPC workloads alongside container-based workloads on the same infrastructure. This is intended to eliminate the need to manage separate clusters by combining workloads onto the same hardware. 

### Core Concepts
- Slurm was designed for traditional HPC workloads, while Kubernetes was designed for smaller, more ephemeral cloud workflows. This project combines the benefits of each approach into a cohesive compute solution. 
- This project is designed primarily to run Slurm within Kubernetes clusters, but [Slurm clusters run within Kubernetes can still interface with slurmd on baremetal nodes](https://github.com/SlinkyProject/slurm-operator/blob/main/docs/architecture.md#hybrid). This leaves the door open for "hybrid" configurations that can take advantage of the positives of running a control plane under K8s, while still allowing for nodes that are not under k8s. 
- ***Slinky enables HPC administrators to move towards an IaC model for cluster management, which is a very powerful capability***

### Terminology
***Kubernetes Operator:*** operators are software extensions that make use of custom resources to manage applications and their components by following a control loop. The operator aims to emulate the behavior of a human operator managing a service. On top of the automation offered by a vanilla k8s instance, operators could automate the deployment of applications, taking and restoring backups, upgrades, or simulating failure and conducting resilience testing.

### What is Slinky?
Slinky is a set of projects that enable interoperability between Slurm and K8s. 

The major components are:
- ***slurm-operator*** - a Kubernetes operator that manages and auto-scales Slurm clusters running as K8s pods. 
- ***slurm-exporter***  provides a Prometheus collector and exporter for Slurm cluster metrics for clusters operating within K8s clusters
- ***slurm-client***  provides a client library for the Slurm REST API that is used by slurm-operator to manage and reconcile state. 
- ***containers*** provides the OCI container images used by Slinky

## [slurm-operator](https://github.com/SlinkyProject/slurm-operator/)
The slurm-operator uses a number of controllers and Custom Resource Definitions that it manages, using data from both the K8s API and from the Slurm API. 


## [slurm-exporter](https://github.com/SlinkyProject/slurm-exporter)
This is a Prometheus collector and exporter for metrics generated within a cluster running on Slinky. It uses the Slurm REST API to ingest data, and outputs it as Prometheus types. 

## [slurm-client](https://github.com/SlinkyProject/slurm-client)
The slurm-client provides slurmrestd endpoints which are used by the controller portion of the slurm-operator. The currently implemented endpoints are focused on Create, Read, Update, and Delete operations for nodes and jobs. These endpoints appear to be generated using [openapi generators](https://openapi-generator.tech/). 

## [containers](https://github.com/SlinkyProject/containers)
SchedMD provides OCI container images to support Slinky. These images are built using [bake](https://docs.docker.com/build/bake/), a feature for Docker buildx which allows for build configuration to be defined declaratively. These images are published to [the SlinkyProject package repo.](https://github.com/orgs/SlinkyProject/packages)

The individual containers are defined by Dockerfile at the path containers/schedmd/slurm/$SLURM_VERSION/$OS_VERSION/Dockerfile. As Slurm is built on container build, patches can be applied at the path containers/schedmd/slurm/$SLURM_VERSION/$OS_VERSION/patches, and will be included in the build. 

# Slurm Bridge
----
Slurm Bridge is a future Slunky project that will allow for co-location of Slurm and Kubernetes workloads. This is intended to bring some more of the advantages of Slurm scheduling and node-packing into Kubernetes, and improve the allocation of resources on clusters with shared workloads. 
