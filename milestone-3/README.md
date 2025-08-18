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

- Create a page for **AD & LDAP Setup** with (10 Points):
   - Domain creation and configuration steps
   - LDAP schema and integration details
   - Replication settings and verification steps
   - Troubleshooting and common errors

- Create a page for **User Accounts & Groups** with (10 Points):
   -  List of created users and groups
   -  Role-based permission assignments
   -  Account policies (passwords, lockouts, expirations)
   -  Documentation of administrative vs. standard accounts

- Create a page for **Group Policies** with (10 Points):
   - Policies applied to user groups
   - Policies applied to device groups
   - Security baselines and compliance settings
   - Testing and verification of GPO effectiveness

- Create a page for **DNS Configuration** with (20 Points):
   - Forward and reverse lookup zones
   - Host (A/AAAA), CNAME, MX, PTR, and SRV records
   - Zone transfer and replication configuration
   - Troubleshooting common DNS resolution issues

- Create a page for **DHCP Setup** with (20 Points):
   - Defined scopes and address ranges
   - Reservations for specific devices
   - Static IP assignments and justifications
   - Failover configuration and troubleshooting

- Create a page for **Firewall Rules** with (20 Points):
   - Current inbound and outbound rules
   - Changes and updates made to rules
   - Backup of rule sets and export procedure
   - Rule justification and security considerations

- Create a page for **Network Diagrams** with (10 Points):
   - Updated topology maps (logical and physical)
   - Device roles and interconnections
   - VLANs and subnet documentation

**Important Note on Scoring**
Points will only be awarded if both the documentation **and** the corresponding system features are fully implemented and operational. This means:

- **Documentation Accuracy** – All pages must provide clear, complete, and up-to-date information reflecting the current configuration and setup.
- **Functional Verification** – Each documented feature (e.g., VPN server, SIEM alerts, file server permissions) must be installed, configured, and tested to confirm it works as described.
- **Consistency** – Any changes made to the system during implementation must be reflected in the documentation to avoid mismatches.
- **Evidence of Operation** – Screenshots, test results, or verification steps must be included in the documentation where applicable to prove that the feature is functioning.

If the documentation is present but the feature is not functional (or vice versa), **no points will be awarded** for that section.


