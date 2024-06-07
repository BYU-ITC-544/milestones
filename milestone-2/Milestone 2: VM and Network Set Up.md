# Milestone 2: VM and Network Set Up

## Objective:

At the end of this milestone, you should have your physical and virtual machines installed and a basic working network that uses the firewall rules you established in the previous milestone.

## Instructions:

You must not download pre-built virtual machines. You should install all machines from an ISO image into the virtual environment.

You should ensure you configure with sufficient disk space (100GB for Windows server 2022, 50GB min for other Windows, and 20GB for the Linux flavors). Expanding disks is fine (using LVM on Linux will make this much easier). We will not be responsible for lost machines - this is part of being a sysadmin!

Save a snapshot of each VM. If you don't do this, you might have to rebuild if you break something later on.

This is the basic topology of the network. You will be responsible for setting up the `Team Router` and `Team LAN` the rest will be set up for you.

![Network Topology](./topology.png)

### Step 1: Connecting to Proxmox

Each team has been given a Proxmox instance to run the required VMs. A TA will give the VPN profile and credentials to access your instance. Your team will be responsible for managing the Proxmox instance throughout the entire semester, if you brick it you will have to start over with a fresh instance or figure out how to fix it yourself.

You will only be able to access your Proxmox and public access machine while connected to the VPN. All of the machines that need to be VMs will be hosted on the Proxmox instance.

### Step 2: Cables

You will have to make the majority of the network cables yourselves, the only exception will be any cables between the patch panel and your Proxmox server.

### Step 3: Networking

You'll need to configure the virtual switches and VLANs on your firewall and in your hypervisor. We'll have a discussion in class about how you might want to set it up for your network and what the physical and logical topologies will look like.

Each team has 10 vlans assigned to it. The VLANs assigned to your team can be found below.

| Team Number | VLAN Range|
| - | -- |
| 1  |   200-209 |
| 2  |   210-219 |
| 3  |   220-229 |
| 4  |   230-239 |
| 5  |   240-249 |
| 6  |   250-259 |
| 7  |   260-269 |
| 8  |   270-279 |
| 9  |   280-289 |
| 10 |	 290-299 |

### Step 4: Firewall & Router

You can use PfSense or Opnsense as the firewall and router for this class and must have specific firewall rules implemented to avoid disrupting the IT&C network. You can use another solution if your team wants to but don't expect TA help to get it set up.

1. Install your firewall as your first VM and make sure that your connection to the internet is working correctly
1. Set up all of your VLANs and firewall rules, you may want to install one machine in each VLAN to test if they are working as expected.

### Step 5: VM set up

1. Install all of the VMs. Just do a basic install, all the setup will be done in a later milestone or you can do it now if you choose to do so.
1. After you've finished the setup up check all the VMs are in the correct VLAN and have access to the correct resources using the firewall rules.

You just need to do the initial setup for each of the VMs, configuring them will come in later labs. This is the minimum list but if your design may require more. 

1. 2x Windows Server 2022
1. 4x Windows 10
1. 1x CentOS-7 or CentOS 8 
1. 1x Debian 10.0.0 or later 
1. 2x Desktop Linux of your choice, at least two different flavors and not Ubuntu
1. 4x Linux Servers

You will need to install a web server on your chosen web server VM to test the port forwarding. Once your VPN is set up you can use your public access machine to test the connection and access your internal network.

These machines will be used for your labs throughout this semester.

### Step 6 Documentation:

Update the documentation and diagrams your team made in milestone 1 to reflect any changes that you have made

### Submission Requirements

Create 1 report for your team and submit the link to Learning Suite as a PDF, any other format will not be accepted.

[ ] 50 Points - Screenshot of each running VM with the following information shown:
- Hostname
- IP address
- Internet access  

[ ] 10 Points - Table showing the name and description of each host (use the above descriptions)  
[ ] 10 Points - Screenshot(s) showing your network configurations on the hypervisor  
[ ] 15 Points - Screenshot(s) showing the VLANs set up  
[ ] 10 Points - List of all implemented firewall rules and why it is a rule  
[ ] 5 Points - The port forwarding for the webserver is working correctly 
