# OpenCHAMI: bridging the worlds of cloud and HPC
Presenter: Chris Harris w/ NERSC

### Summary & Introduction
- Why open source system management tools?
    - Less is being delivered by vendors
    - Overhead of long term testing, training, and support
    - Convergence of HPC, cloud, and ML
    - Stalled innovation --> rigid tools, repetitive tasks, lack of niche expertise
    - Avoid the retooling cycle every few years --> need something vendor agnostic
- OpenCHAMI --> Open Composable Heterogenous Adaptable Management Interface (whew..)
    - Open source cloud-like ops (modular, cloud-native)
    - What does it do? System management:
        - Inventory management
        - Securely boot images
        - Customize options for each node
        - Enable other teams to manage other aspects of the system
- Guiding principles:
    - Community-development and maintinence
    - Do one thing well --> microservices, useful inputs and outputs. Helps manage & reduce complexity
    - Reduce unplanned maintinence & improve reliability 
    - Memory-safe languages & HTTP REST APIs
    - Does not authenticate --> authorizes
    - Agnostic to OS, deployment tech, workflow manager, and image build process 

### Architecture
- ***State Management Database (SMD)*** --> manage inventory information and expose that info via a REST API
- ***Magellan*** --> BMC, cli, discovery tool. Uses redfish to get info on BMC nodes & populate/validate inventory
- ***Boot Script Service (BSS)*** --> Custom boot parameters for nodes (taken from inventory)
- ***cloud-init*** --> The de facto standard for customizing cloud instances at boot time. Generates configs for nodes, merges config from SMD, user-supplied JSON, and cluster/group defaults
- ***Power Control Service (PCS)*** --> Performs power-related operations on system components (power on, off, reboot, power capping). Uses redfish to communicate with BMC's
- ***Ochami*** - CLI for the API of OpenCHAMI w/ subcommands for each component

### Ochami and DevSecOps
- HPC poses many security challenges
- "Security is the shared responsiblity across development, operations, and security teams"
- Automation of a escure software development lifecycle using CI/CD, rapid testing, IaC, and continuous security checks
- Machine-based authentication - uses WireGuard to perform node identity verification. Nodes generate KeyPair when powered on & configures a tunnel. Search for good blog post on this. Working towards TMP-based machine attestation w/ Keylime. Moving towards workload identity and secure chain of custody.
- Artifact security - secure supply chain for artifacts - https://slsa.dev/ Provides an attestation step within CI pielines to attest to how and when a build was run
- Infrastructure as Code (IaC) - Manage cluster through code instead of manual processes. OpenCHAMI shifts modality from HPC admins being sysadmins to filling more of a DevOps role.
 
