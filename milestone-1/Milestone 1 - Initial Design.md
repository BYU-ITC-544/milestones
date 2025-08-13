# Milestone 1: Initial Design

## Objective:

Given a list of requirements, your team will design a network and choose the software solution(s) that you will use to achieve your objectives. This will not be an all-inclusive design and will mostly outline what you plan to do, and you will add to it as the semester progresses. This milestone focuses on creating a **comprehensive initial design** that balances functionality, security, and scalability.

## Requirements

You are the new IT department for Spicy Cluck Co., a company that has a chain of fried chicken stores across the United States and Europe. Your team has been tasked with setting up a new regional office in Provo, Utah. The office needs to have the following services and systems:

- **DNS Linux Server**:
  - Resolve internal and external requests.
  - Integrate with AD for internal name resolution.

- **Active Directory (AD)**:
  - Manage users, groups, and permissions.
  - Integrate with LDAP-compatible services if needed.

- **Backup Active Directory**:
  - Secondary AD server for redundancy and disaster recovery.
  - Ensure replication and time synchronization with primary AD.

- **Database Server**:
  - Implement the database structure provided for the website.
  - Secure access and backups.

- **Web Server**:
  - Host the official website on the public internet.
  - Implement SSL/TLS and proper firewall rules.

- **File Server**:
  - Central file storage for documents, files, and resources.
  - Implement permissions according to roles.

- **Linux Machine for General Use**:
  - Provide a Linux workstation for administrative tasks and development work.

- **General Workstations**:
  - Workstations for employees to use for daily tasks.
  - Configure based on user type (in-person, hybrid, remote).

- **Onsite Backup Server**:
  - Store backups of critical data and systems locally for quick recovery.
  - Schedule regular backups and test restores.

- **VPN Server(s)**:
  - Provide secure remote access for hybrid and remote workers.
  - Implement multi-factor authentication where possible.

- **Desktop Linux Machine**:
  - Provide additional desktop Linux machines for administrative tasks and development work.

- **DHCP Server**:
  - Manage and assign IP addresses dynamically to devices within the network.
  - Configure reservations for servers and critical devices.

- **SIEM Server**:
  - Implement a Security Information and Event Management system for monitoring and analyzing security events and incidents across the network.
  - Centralize logs from all critical devices.
  - Install endpoint protection on devices.

- **Metric Server**
  - Implement a resource monitoring server in Proxmox and set up usage and availability alerts.
  - Monitor VM resource usage and network statistics.

**Minimum Hardware/VM Allocation:**

* 2x Windows Server 2022
* 5x Windows 10 or 11
* 1x Kali Purple
* 1x Debian Desktop 10.0.0 or later
* 1x Desktop Linux of your choice
* 4x Linux Servers

You will be given a total of 10 VLANs for your network; you may use fewer but no more.

## Instructions:

This will just be an initial design, and you will be expected to amend it throughout the semester as you learn more about these systems. The focus is on creating a **robust foundational plan** that can evolve as the network grows.

You will need to create the needed tables, figures, diagrams, etc. to plan out and explain your design. This is **not a final draft**, and it will most likely change as you implement it over the semester, but it must be complete and include all the items below.

There will be **one deliverable** for this assignment: a written technical document outlining the **design requirements, network design (logical and physical), and software/technologies** you plan to use.

### Step 1: Technologies & Software

Choose the technologies & software that you will use. Several technologies you may want to consider include:

1. **Router** (OPNSense, PfSense, IPFire)
1. **Firewall** (IPFire, OpenWrt, OPNSense, PfSense)
1. **DNS** (BIND, Unbound, dnsmasq, PowerDNS)
1. **IDS/IPS/SIEM** (Security Onion, Gravwell, Splunk, ELK, Wazuh)
1. **Web Server** (Apache, Nginx)
1. **VPN** (OpenVPN, WireGuard, OPNSense)
1. **File Server** (Samba, OpenMediaVault, TrueNAS)
1. **Database** (MySQL, Postgres, MariaDB)
1. **Backup and Restore Solution** (Bacula, Duplicati, UrBackup)
1. **DHCP Server** (OPNSense, Windows Server)
1. **Metric Server** (Graphite, InfluxDB)

**Additional Considerations:**

- You may select alternative technologies if they better meet your objectives.
- For any new software/system added, document the justification and expected benefit.
- Include considerations for **ease of maintenance, security, scalability, and disaster recovery** in your selection rationale.

### Step 2: Network Diagram

1. Create **logical and physical network diagrams** that meet the above requirements (two separate diagrams).
1. Include **IP addresses** (use `10.0.0.0/8`), VLAN IDs (maximum 10), subnets, gateways, and network segments.
1. Include **server and workstation placement**, showing which VLAN each host belongs to.
1. Justify design decisions and state any assumptions clearly. For example:
  - VLAN segmentation for security (servers vs. workstations)
  - Redundant paths for critical systems
  - Choice of private IP ranges for internal communication

### Step 3: Other Design Considerations

#### 1. Disaster Recovery

- Identify critical systems and services.
- Plan backup strategies (onsite/offsite, VM snapshots, file backups).
- Include failover mechanisms for AD, DNS, and core network services.
- Test restore procedures periodically.

#### 2. Firewall Rules (Least Privilege Principle)

- Follow the **principle of least privilege**: allow only traffic necessary for each system/service. This includes IP version, subnet ranges, protocols and ports.
- **Key rule elements**:
  - **Source:** IP, subnet, VLAN, or alias.
  - **Destination:** IP, subnet, VLAN, or alias.
  - **Source Port:** Port(s) on the source machine (often `any`).
  - **Destination Port:** Port(s) on the destination system (e.g., `443`, `3306`).
  - **Protocol:** TCP, UDP, ICMP, or combination.
  - **Direction:** Inbound/outbound relative to the interface.
  - **Gateway (optional):** Policy-based routing.
  - **Schedule (optional):** Time-based access control.
- **Rule Ordering:**
  - Place **specific rules first** (e.g., service-to-service).
  - Place **general deny/catch-all rules last**.
- **Logging:** Enable logging for needed rules
- **Testing:** Use ping, traceroute, telnet, DNS queries, or application clients to confirm functionality.
- Consider creating **default-deny rules** for unclassified VLANs.

#### 3. Policies, Frameworks, and Laws

- Identify all relevant organizational policies and regulatory frameworks to enforce. Examples:
  - Acceptable Use Policy (AUP)
  - Password Policy
  - Access Control Policy
  - Data Retention and Disposal Policy
  - Remote Access Policy
  - GDPR or CCPA compliance (for European and US data handling)
  - Security Incident Response Plan
- These policies should guide firewall rules, user permissions, and network design.

#### 4. Devices – Physical vs VM

- Users will require a mix of **physical workstations** and **VMs** (VDIs would also be suitable) depending on their role:
  - **Remote workers:** VM or VDI only
  - **Hybrid workers:** VM + physical workstation (assume half are onsite at a time)
  - **In-person workers:** Physical workstation only
- Document which devices are physical and which are virtual to assist with resource allocation.

**User List with Access Requirements:**

1. Emily Brown - CTO (Remote)
1. Albert Tay - Director of Fried Chicken (Hybrid)
1. Rachel Nguyen - HR Manager (In-person)
1. Alex Patel - IT Manager (Hybrid)
1. Karen Taylor - Customer Service Manager (In-person)
1. Jessica Rodriguez - Content Writer (In-person)
1. Ryan Lee - Graphic Designer (In-person)
1. Ben Anderson - Sales Representative (In-person)
1. Olivia Davis - Data Analyst (Remote)
1. Eric Nguyen - Network Administrator (Hybrid)

### Step 4: Hardware

- **Physical Workstations & Peripherals:**
  - Include monitors, keyboard/mouse, power, and network cables.
  - Ensure cables are properly terminated and tested.

- **VM Host Resources:**
  - Total RAM, CPU, and storage needed for all VMs.
  - Include overhead for snapshots, backups, and monitoring.
  - Adjust according to available server resources.

- **Networking Hardware:**
  - Switches, routers, access points, and patch cables.
  - Ensure proper VLAN configuration and separation of management traffic.
  - Include labeling for ports and cable runs for maintainability.

- **Backup and Recovery Hardware:**
  - Onsite backup storage capacity and redundancy.
  - Plan for offsite backup if required for compliance or disaster recovery.

### Example Table

Here’s an example **VLAN, Services, and Firewall Rules Table** that demonstrates some of the information you will need to include. It organizes the network by VLAN, lists the services running in each, and gives example firewall rules. You can expand or adjust it as your design evolves.

| VLAN ID | VLAN Name           | IP Subnet     | Hosts/Services                   | Example Firewall Rules (Least Privilege)                                                                 |
| ------- | ------------------- | ------------- | -------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 10      | Management          | 10.0.10.0/24  | AD Primary, AD Backup, DNS, DHCP | Allow Management VLAN → all servers (necessary ports only), Deny all other access                         |
| 20      | Web Servers         | 10.0.20.0/24  | Web Server                       | Allow WAN → Web Server TCP 443/80, Allow Management VLAN → Web Server TCP 22/3389, Deny all else          |
| 30      | Database Servers    | 10.0.30.0/24  | Database Server                  | Allow Web Servers → Database TCP 3306, Allow Management VLAN → Database TCP 3306, Deny all else           |
| 40      | File Servers        | 10.0.40.0/24  | File Server                      | Allow Management VLAN → File Server TCP 445/139, Allow Workstations VLAN → File Server TCP 445/139        |
| 50      | Workstations LAN    | 10.0.50.0/24  | General Workstations             | Allow Workstations → DNS TCP/UDP 53, Allow Workstations → Web TCP 80/443, Deny inter-VLAN traffic         |
| 60      | VPN Clients         | 10.0.60.0/24  | Remote/Hybrid Worker VMs         | Allow VPN → Management VLAN (specific ports), Allow VPN → Web/Database servers (as needed), Deny all else |
| 70      | SIEM / Security     | 10.0.70.0/24  | SIEM Server, Metric Server       | Allow Management VLAN → SIEM TCP 514/443, Allow SIEM → all servers for log collection, Deny all else      |
| 80      | Backup              | 10.0.80.0/24  | Onsite Backup Server             | Allow Management VLAN → Backup TCP 22/873/445, Deny all else                                              |
| 90      | Admin Linux         | 10.0.90.0/24  | Linux Admin/Desktop Machines     | Allow Admin VLAN → all servers (necessary ports only), Allow Admin → VPN TCP 1194, Deny all else          |
| 100     | DMZ / Public Access | 10.0.100.0/24 | Public-facing services if needed | Allow WAN → DMZ TCP 80/443, Allow Management VLAN → DMZ TCP 22/443, Deny all other traffic                |

### Submission Requirements

Combine all design components into a **single detailed technical document**. Include:

1. Title/Cover page
2. Table of contents
3. Project overview, purpose, and objectives
4. Technologies & software selection
5. List of all hosts with hostnames, OS type, and version
6. Devices categorized as physical workstations or VMs
7. Logical and physical network diagrams with IP addresses, VLANs (max 10), and subnets
8. Disaster recovery plan and firewall rules outline
9. Policies, frameworks, and laws to be followed or created
10. Justification of design decisions and any assumptions made at each step
11. Any additional diagrams, tables, or figures needed for clarity

**Format:** PDF, with all text, tables, and images legible and readable.