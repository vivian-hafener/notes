# OCHAMI
Open Composable Heterogeneous Adaptable Management Infrastructure

#### Software Architecture Overview
OpenCHAMI uses a microservices-based approach where each of these components are independent, but able to communicate via an API. 

* Boot Script Service (BSS) - Handles custom boot parameters for compute nodes
* State Management Daemon (SMD) - Maintains inventory and node health status
* Magellan - discovers and manages server hardware using Redfish APIs
* OPAAL - OIDC-based authorization and authentication
* Configurator - dynamically generates config files from templates

## Components
---
#### Boot Script Service - https://github.com/OpenCHAMI/bss
* Purpose: BSS delivers boot arguments, initrd, and kernel arguments to HPE Shasta systems and supports Level 2 boot services for static images.
* API Specification: A swagger.yaml file in this repo defines the REST API endpoints for BSS.
* Architecture: Designed to be a minimal, stateless service that focuses solely on providing the necessary boot metadata to nodes in a Shasta environment.

#### OpenCHAMI Cloud-Init Server - https://github.com/OpenCHAMI/cloud-init
* Generates cloud-init configurations for nodes
* Takes in configuration data from:
	* SMD
	* User-supplied JSON
	* Cluster defaults and group overrides
* On nodes, cloud-init retrieves data in a specific order:
	1. `/meta-data` - YAML doc with system configuration
	2. `/user-data` - a document from [one of the specified formats ](https://cloudinit.readthedocs.io/en/latest/explanation/format.html#cloud-config-data)
	3. `/vendor-data` - vendor-supplied configuration via include-file mechanisms
	4. `/network-config` - Optional document in [one of the formats](https://cloudinit.readthedocs.io/en/latest/reference/network-config.html#network-config). This is only retrieved from if specifically requested and is not supported via the OpenCHAMI cloud-init server today. 

#### State Management Daemon - https://github.com/OpenCHAMI/smd
SMD is responsible for:
* Discovering hardware inventory.
* Tracking hardware state, logical roles, and enabled/disabled status.
* Creating and managing component groups and partitions.
* Storing and retrieving Redfish endpoint and component data.
* Monitoring hardware state transitions via Redfish events.

#### ochami - https://github.com/OpenCHAMI/ochami
* ochami is the OpenCHAMI Command-line interface, which allows use of the OpenCHAMI API while not needing to rely on lots of `curl` commands
* Configuration is done via two config files, or via compiled defaults if neither are defined. 
	* System-level configuration resides in `/etc/ochami/config.yaml`
	* User-level configuration resides in `${HOME}/.config/ochami/config.yaml`
You can generate a user-level configuration by running:
```
mkdir -p ~/.config/ochami/
ochami config show > ~/.config/ochami/config.yaml
```

References:
---
OpenCHAMI Docs - https://openchami.org/
OpenCHAMI Repos - https://github.com/OpenCHAMI
