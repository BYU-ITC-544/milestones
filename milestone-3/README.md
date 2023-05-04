# Milestone 3: VM and Network Set Up

## Objective:

At the end of this milestone, you should have your physical and virtual machines installed and a basic working network that uses the firewall rules you established in the previous milestone.

## Instructions:

You must not download pre-built virtual machines. You should install all machines from an ISO/USB/NetInstall image into the virtual environment.

You should ensure you configure with sufficient disk space (100GB for Windows server 2022, 50GB min for other Windows, and 20GB for the Linux flavors). Expanding disks is fine (using LVM on Linux will make this much easier).  (If you run these on your hardware, you should ensure you can run 2-3 of these VMs at any one time, and you must also ensure you have a copy on an external drive or your machine.) We will not be responsible for lost machines - this is part of being a sysadmin!

Save a snapshot of each VM. If you don't do this, you will have to repeat this lab later down the line in your own time, with no extra grade!

### Step 1: Installation

You will be given 2 physical servers that your team will use for the entire semester. 1 server will host your type 1 hypervisor and the other will act as a NAS for all your VM storage.

1. Download the TrueNAS core ISO
1. Prepare a USB drive to install the ISO
1. Install the NAS
    - Make sure to set a secure password that you will not forget

1. Download the ISO for your chosen hypervisor
1. Prepare a USB drive to install the ISO
1. Install the hypervisor
    - Make sure to set a secure password that you will not forget

### Step 2: Configuring TrueNAS

1. Create an appropriate folder structure within TrueNAS and give the needed folder(s) the correct permissions to be accessible from the hypervisor
1. Add the TrueNAS folder to your hypervisor as storage

<br>
<br>

### Step 3: Networking

1. You'll need to configure the virtual switches and VLANs on your firewall and in your hypervisor. We'll have a discussion in class about how you might want to set it up for your network.

### Step 4: Firewall & Router

You can PfSense or Opnsense as the firewall and router for this class and must have specific firewall rules implemented to avoid disrupting the IT&C network. You can use another solution if your team wants to but don't expect TA help to get it set up.

1. Install your firewall as your first VM and make sure that your connection to the internet is working correctly
1. Set up all of your VLANs and firewall rules, you may want to install one machine in each VLAN to test if they are working as expected

### Step 5: VM set up

1. Install all of the VMs. Just do a basic install, all the setup will be done in a later milestone or you can do it now if you choose to do so.
1. After you've finished the set up check all the VMs are in the correct VLAN and have access to the correct resources using the firewall rules.

You just need to do the initial setup for each of the VMs, configuring them will come in later labs. This is the minimum list but if your design requires more 

1. 2x Windows Server 2022
1. 4x Windows 10
1. 1x CentOS-7 or CentOS 8 
1. 1x Debian 10.0.0 or later 
1. 2x Desktop Linux of your choice, at least two different flavors and not Ubuntu
1. 4x Linux Servers

You will need to install a web server on your chosen web server VM to test the port forwarding

These machines will be used for your labs throughout this semester.

### Step 6 Documentation:

Update the documentation and diagrams your team made in milestone 1 to reflect any changes that you have made

<br>
<br>
<br>
<br>
<br>
<br>
<br>

### Pass-Off Requirements

Create 1 report for your team and submit the link to Learning Suite as a PDF, any other format will not be accepted.

- [ ] 70 Points - Screenshot of each running VM with the following information shown:
    - Hostname
    - IP address
    - Internet access

- [ ] 15 Points - Table showing the name and description of each host (use the above descriptions)
- [ ] 10 Points - Screenshot(s) showing your network configurations on the hypervisor
- [ ] 10 Points - Screenshot showing the VLANs set up
- [ ] 10 Points - List of all implemented firewall rules and why it is a rule
- [ ] 5 Points - The port forwarding for the webserver is working correctly