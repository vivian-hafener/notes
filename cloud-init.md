# Introduction to clout-init

## What is cloud-init
* An initialization tool to automate the initialization and configuration of machines
* Applies settings from a configuration to a machine (to-do list)
	* Can do things like setting hostname, configuring network interfaces, setting up user accounts, etc. 
* Config settings are re-usable across configurations

## How does cloud-init work?
* Early boot phase
	1. Identify the datasource
	2. Fetch config data from the datasource. 
		* Meta-data - instance platform data, like the hostname, network config, etc. 
		* Vendor-data / User-data - post-networking data, like ssh keys, custom scripts, hardware optimizations
	3. Write network configuration and configure DNS

* Late boot phase
	* Can interact with config management to apply more complex configs
	* Install software / run updates
	* Modify accounts
	* Execute user scripts

## Using cloud-init

#### The cloud-config
The cloud-config file is a file that is commonly used for early-boot configuration. It is defined in YAML and can do most things. However, it can't define the network because that is generally done separately.

References:
---
https://cloudinit.readthedocs.io/en/latest/index.html 
