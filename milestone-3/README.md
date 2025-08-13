# Milestone 3: Active Directory, LDAP, DNS, DHCP, Group Policies

## Technologies Overview:

Active Directory, LDAP, DNS, DHCP, and Group Policies are key technologies for managing Windows-based networks. They allow centralized administration, user authentication, and configuration management across devices.

**Objectives of Each Technology:**

1. Active Directory (AD):
   - Provides centralized authentication and authorization.
   - Allows administrators to manage users, groups, devices, and security policies.
   - Supports software deployment, access control, and network resource management.

1. **LDAP (Lightweight Directory Access Protocol):**
   - Standard protocol for accessing and maintaining directory services.
   - Used by AD for querying and managing network directory data.

1. **DNS (Domain Name System):**
   - Translates human-readable domain names into IP addresses.
   - Ensures that internal services and websites are reachable using friendly names.

1. **DHCP (Dynamic Host Configuration Protocol):**
   - Automatically assigns IP addresses and network configuration to devices.
   - Simplifies network management and prevents IP conflicts.

1. **Group Policies:**
   - Apply consistent configuration and security settings across multiple devices.
   - Control software installation, security policies, network access, and user permissions.

## Instructions:

### Step 1: Active Directory & LDAP

- Configure your **primary Windows Server 2022** as the **Domain Controller**.
- Configure your **secondary Windows Server 2022** as a **backup Domain Controller** for redundancy.
- Join all machines to the domain and ensure login is possible using AD credentials.
- Document steps for:
   - Creating users and groups
   - Assigning permissions
   - Modifying and disabling accounts
   - Backup and restoration of AD


### Step 2: DNS

- Designate a Linux or Windows VM as the **internal DNS server**.
- Configure your router/firewall to forward DNS queries to this server.
- DNS should resolve internal hostnames for all services, e.g.:
   - `website.sysadmin.local` → Web Server
   - `db.sysadmin.local` → Database Server
   - `files.sysadmin.local` → File Server
   - `ad1.sysadmin.local` → Primary AD
   - `ad2.sysadmin.local` → Backup AD\
   - All windows hostnames to their IPs 
- Document:
   - DNS zones and records
   - How to add, modify, and remove records

### Step 3: DHCP

- Assign IP addresses dynamically for **general-use machines** using DHCP (either router or Windows Server).
- Assign **static IPs** for all critical infrastructure services (servers, firewall, routers).
- Document:
  - DHCP scope(s)
  - Reservations for critical devices
  - Current leases


### Step 4: Group Policies

- Organize the **10 employees** into groups based on role and access requirements.
- Define **device groups** for servers, workstations, and administrative machines.
- Policies that should be set include:
   - Password & Security Policy
      - Enforce minimum password length: 12 characters
      - Require complex passwords
      - Set account lockout after 5 failed login attempts
   - Software Deployment
      - Install approved business apps based on user group (e.g., CRM for Sales, Office Suite for Content)
      - Restrict installation of unauthorized software
   - Access Control
      - Map network drives based on department (e.g., HR_Shared, Sales_Shared)
      - Limit access to servers and admin consoles according to user group
      - Multi-factor authentication enforced for all logins
   - Administrative Rights
      - IT Managers and Network Admins: Full admin on servers and devices relevant to IT operations
      - Executives: Limited delegation for business-critical apps
      - All other users: Standard user privileges; no local admin rights
   - Device Configuration
      - Enforce company-standard desktop configuration
      - Restrict USB and removable media access for sensitive groups
- Document
   - Record all user accounts, group memberships, and assigned permissions.
   - Document GPOs applied to each group, including enforcement settings.
   - Include instructions for creating, modifying, disabling, or removing users and policies.


### Step 5: Firewall Review

- Review and update firewall rules to ensure the **principle of least privilege** is enforced.
- Confirm:
   - Only required inter-VLAN communication is allowed
   - Services like DNS, DHCP, AD, and web access are permitted
- Include a **backup of current firewall rules** that can be imported if needed.
- Document all firewall changes and justifications.


### Step 6: Testing

- Verify that:
   - Users can log in to the domain
   - DNS resolves all internal services
   - DHCP assigns addresses correctly
   - Group Policies are applied
   - Firewall rules allow required traffic and block unauthorized access
- Log all testing results in the wiki for reference and troubleshooting.

### Step 7: Documentation for the Wiki

Update your GitHub wiki with the following Milestone 3 sections:

1. **Active Directory & LDAP**
   - Primary and backup domain controllers
   - User and group management procedures
   - Backup and recovery procedures

1. **DNS**
   - DNS server configuration
   - Zone and record setup
   - Forwarding and resolution examples

1. **DHCP**
   - DHCP scope and reservation table
   - List of statically assigned IPs

1. **Group Policies**
   - Policies applied to each user and device group
   - Step-by-step procedures for creating/modifying policies

1. **Firewall**
   - Updated rules and rationale
   - Backup of rules for re-import

1. **Network Diagram Updates**
   - Update logical and physical diagrams with any changes

1. **Testing Results**
   - Evidence of correct login, DNS resolution, DHCP assignment, policy application, and firewall enforcement


### Checklist for Wiki Update

- **Update the GitHub wiki** with all relevant Milestone 3 items
- Ensure all sections are **clear, detailed, and organized** for future sysadmins.

Sections that should be updated or created include:
- [ ] AD & LDAP setup documented
- [ ] User accounts and groups created, with permissions assigned
- [ ] DNS setup, zones, and records documented
- [ ] DHCP scopes, reservations, and static IPs listed
- [ ] Group Policies documented per user/device group
- [ ] Firewall rules reviewed, updated, and backup included
- [ ] Network diagrams updated
- [ ] Test results recorded and summarized
