# Configuration Management

## Server Configuration/Orchestration

- Common tools include Puppet, Ansible, Chef
- Allows for quick provisioning of new servers
- Allows for quick recovery, able to deploy replacement server while inspection is done on affected server
- No snowflake servers: manual hotfixes, config tweaks can create unique snowflakes
- Once server setup done with provisioning scripts, config mgmt can apply tools and workflows
- Replicated environments, can set up on local VMs for testing

### Automation Framework
- Each tool provides set of syntax and features to write provisioning scripts
- Similar to conventional programming languages, but in simplified form

### Idempotent Behavior
- Keeps track of state of resources to avoid repeating tasks
- Won't try to install packages multiple times
- Aim is that after each provisioning run, system will reach desired state, even if run again

### System Facts
- Provides detailed information about the systems being provisioned
- Includes information such as network interfaces, IP addresses, OS, distribution
- Used in provisioning scripts

### Templating System
- Templating system to facilitate setting up configuration files and services
- Templates support variables, loops, conditionals used to maximize versatility

## Tools

### Ansible
- Decentralized structure
- Doesn't require installation of additional software on nodes
- Relies on SSH for provisioning tasks
- YAML scripts
- Any node can be a controller
- Scripts called playbook/roles
- Sequential execution

### Puppet
- Requires a controller machine and a node to be managed
- Requires an agent application to be installed on node, and a master application for the controller
- Uses custom DSL based on Ruby
- Centralized around a puppet master
- Puppet master synchronizes configuration on nodes
- Scripts called Manifests/Modules
- Non-sequential execution

### Chef
- Uses Ruby
- Chef workstations push configuration to Chef Server, which updates Chef Nodes
- Requires software on nodes
- Chef Server is the central point
- Scripts called Recies/Cookbooks
- Sequential execution
