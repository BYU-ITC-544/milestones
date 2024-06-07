# Milestone 1: Initial Design

## Objective:

Given a list of requirements, your team will design a network and choose the software solution(s) that you will use to achieve your objectives. This will not be an all-inclusive design and will mostly outline what you plan to do and you will add to it as the semester progresses.

## Requirements

You are the new IT department for Spicy Cluck Co. which is a company that has a chain of fried chicken stores across the United States and Europe. Your team has been tasked with setting up a new regional office in Provo, Utah. The office needs to have the following services and systems:

- **DNS Linux Server**:
   - Resolve internal and external requests.
- **Active Directory (AD)**:
   - Manage users, groups, and permissions.
- **Backup Active Directory**:
   - Secondary or backup AD server for redundancy and disaster recovery.
- **Database Server**:
   - Implement the database structure provided for the website.
- **Web Server**:
   - Host the official website on the public internet.
- **File Server**:
   - Central file storage for documents, files, and resources.
- **Linux Machine for General Use**:
   - Provide a Linux workstation for administrative tasks and development work.
- **General Workstations**:
    - Workstations for employees to use for their daily tasks.
- **Onsite Backup Server**:
    - Store backups of critical data and systems locally for quick recovery.
- **VPN Server(s)**:
    - Set up VPN servers to allow remote and hybrid workers secure access to the network.
- **Desktop Linux Machine**:
    - Provide additional desktop Linux machines for administrative tasks and development work.
- **DHCP Server**:
   - Manage and assign IP addresses dynamically to devices within the network.
- **SIEM Server**:
   - Implement a Security Information and Event Management system for monitoring and analyzing security events and incidents across the network.

As a minimum, you should use:

- 2x Windows servers 2022
- 18x Windows 10 or 11
- 1x Kali Purple
- 1x Debian Desktop 10.0.0 or later
- 1x Desktop Linux of your choice
- 4x Linux Servers

You will be given a total of 10 VLANs for your network, you may use less than 10 but no more.

## Instructions:

This will just be an initial design and you will be expected to make changes to it throughout the semester as you learn more about these systems.

You will need to create the needed tables, figures, diagrams, etc. to plan out and explain your design. This will not be your final draft and it will most likely change as you implement it over the semester but it still must be complete and include all the items below. 

There will be 1 deliverable for this assignment, a written technical document that will outline the design requirements, network design, and software/technologies that you plan to use.

Please review the grading rubric for the level of detail that is expected.

### Step 1: Technologies & Software

Choose the technologies & software that you will use. Some you will want to consider are:

1. Router (OPNSense, PfSense, IPFire)
1. Firewall (IPFire, OpenWrt, OPNSense, PfSense)
1. DNS (BIND, Unbound, dnsmasq, PowerDNS)
1. IDS/IPS/SIEM (Security Onion, Gravwell, Splunk, ELK)
1. Web Server (Apache, Nginx)
1. VPN (OpenVPN, WireGaurd, OPNSense)
1. File Server (Samba, OpenMediaVault, TrueNAS)
1. Database (MYSQL, Postgres, MariaDB)
1. Backup and restore solution (Bacula, Duplicati, UrBackup)
1. DHCP Server (OPNSense, Windows Server)

You don't have to use the above suggestions if you want to try something else out. You can also change which one you use if you find it will not work for your solution. If there is a technology or system you want to work with but is not in the requirements you can add it and we can look at swapping it out for a different requirement. 

### Step 2: Network Diagram 

1. Create a network diagram that meets the above requirements
1. Include what IP addresses (use 10.0.0.0/8 addresses), VLANs (max 10), Subnets, etc. you will use (These should be in the diagram and a separate table)
1. Justify your design decisions and state any assumptions that you have made

### Step 3: Other Design Considerations 

1. Disaster Recovery
1. Policies, frameworks, and laws that need to be followed
1. Devices that should be a physical workstation vs a VM

This is a list of the users that will be using the system. Users will be a mix of in-person, hybrid, and remote. Hybrid and remote workers will require a VM but hybrid workers will also need a physical machine. In-person workers will only need physical workstations. You can assume that only half of the hybrid workers will be physically present at any one time.

1. Jane Smith - CEO (Remote)
1. John Doe - COO (Remote)
1. Sarah Lee - CMO (Remote)
1. Michael Chen - CFO (Remote)
1. Emily Brown - CTO (Remote)
1. Albert Tay - Director of Fried Chicken (Hybrid)
1. David Kim - Director of Operations (Hybrid)
1. Lisa Jackson - Director of Marketing (Remote)
1. Tom Johnson - Director of Sales (Remote)
1. Rachel Nguyen - HR Manager (In-person)
1. Alex Patel - IT Manager (Hybrid)
1. Karen Taylor - Customer Service Manager (In-person)
1. Kevin Wong - Product Manager (In-person)
1. Jessica Rodriguez - Content Writer (In-person)
1. Ryan Lee - Graphic Designer (In-person)
1. Taylor Adams - Social Media Manager (Hybrid)
1. Ben Anderson - Sales Representative (In-person)
1. Grace Kim - Software Developer (Remote)
1. Olivia Davis - Data Analyst (Remote)
1. Eric Nguyen - Network Administrator (Hybrid)
1. Megan Thompson - Administrative Assistant (Hybrid)

### Step 4: Hardware

You will need to work out how much of the following your design will need. We will be getting most of these from surplus so make sure you have a detailed shopping list!

1. Physical workstations and any peripherals or cables (power, mouse, keyboard, monitors, monitor cables)
1. Total RAM, CPU, and storage needed for all VMs (We may have to adjust this depending on available resources, we will provide server resources  to host your VMs)
1. Networking hardware (switches, cables, AP, etc.) - You will be making your own ethernet cables and they must be correctly made to a good standard. Simply passing the cable test will not be sufficient.

### Submission Requirements

Combine all of your design components into a single detailed technical document. Make sure to include a contents project overview, scope and purpose, and summary at the end. It should also contain documentation for all the above steps. Please refer to the grading rubric to see everything that must be included.

Submit the written technical report a PDF format, the presentation should also be submitted as a PDF.