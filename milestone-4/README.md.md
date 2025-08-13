# Milestone 4: Systems Set Up

## Objective

In this milestone, you will configure the following systems:

* File server
* Vulnerability Scanner
* VPN server
* SIEM with Endpoint Protection
* Metric Server (Extra Credit)

The focus is on securing services, ensuring proper access controls, monitoring, and documenting all configurations.


## Instructions

### Step 1: File Server

**Purpose:** Centralize file storage for the company and enforce access controls based on employee roles and groups.

**Setup Tasks:**

1. Install File Server
   - This can be done on a Windows server or Linux device.
   - Ensure the server has sufficient storage and is backed up regularly.

1. Define Access Rights
   - Apply permissions based on AD groups or local user groups.
   - Example:
      - HR folder: read/write access for HR Manager, read-only for Director.
      - IT folder: read/write for IT team, restricted for others.

1. Connect Workstations
   - Map network drives for Windows users.
   - Mount directories for Linux users.
   - This should be done through group policy

4. Test CRUD Operations
   - Verify that users can **Create, Read, Update, Delete** files only where allowed.
   - Document any permissions issues.

**Wiki Updates:**

- Create a page for **File Server Configuration** with:
   - Folder structure and mapping to groups
   - Access rights per folder
   - Backup schedules and locations
   - Troubleshooting tips
- Document any changes you made to Group Policies

### Step 2: Vulnerability Scanning

**Purpose:** Identify vulnerabilities in your environment before attackers can exploit them.

**Setup Tasks:**

1. Install Vulnerability Scanner
   - Use OpenVAS, Nessus, or another solution.

1. Scan All Systems
   - Include all VMs, workstations, and critical network devices.
   - Document the results.
   - Perform a credentialed scan on at least one Windows device and one Linux device.

1. Set Automated Scan Schedule
   - Weekly scans recommended.
   - Ensure CVE database updates automatically.

1. Create Risk Assessment
   - Incorporate vulnerabilities into a risk matrix.
   - Include remediation plans for critical findings.

**Wiki Updates:**

- Create a **Vulnerability Scanning** page with:
   - Tool setup and configuration
   - Scan results and screenshots
   - Risk assessment updates
   - Mitigation strategies
- Document any changes you made to Group Policies


### Step 3: VPN Server

**Purpose:** Provide secure remote access for hybrid and remote employees.

**Setup Tasks:**

1. Install VPN Software
   - Use OpenVPN, WireGuard, or compatible solutions.

1. Authentication
   - Enforce username/password plus multi-factor authentication (MFA).

1. Network Configuration
   - Assign a static public IP: `128.187.49.253`.
   - Configure port forwarding for VPN traffic.
   - Ensure internal DNS resolution for all internal resources.
   - Use the table from Milestone 2 for the port you will need to use

1. Security Settings
   - Use strong encryption (AES-256 or higher).
   - Enable logging and auditing.
   - Restrict VPN access to only remote and hybrid users, ensuring that in-person users cannot connect.

**Wiki Updates:**

- Create a **VPN Server** page with:
   - Installation steps and configuration
   - Authentication methods
   - Connection instructions for remote users
   - Firewall and port forwarding configuration
   - Test results and troubleshooting steps
- Document any changes you made to Group Policies


### Step 4: SIEM & Endpoint Protection

**Purpose:** Collect logs and detect malicious activity. Endpoint protection ensures that devices are continuously monitored for threats.

**Setup Tasks:**

1. Install SIEM
   - Examples: Splunk, ELK Stack, Security Onion.

1. Configure Endpoint Protection
   - Install antivirus/EDR agents on 1 server and 1 workstations.
   - Enable real-time protection, scheduled scans, and reporting.

1. Log Collection
   - Collect logs from:
     - Servers (AD, DNS, File, VPN)
     - Workstations
     - Routers

1. Alert Configuration
   - Configure alerts for suspicious logins, malware detections, and configuration changes.
   - Test alerts to ensure they trigger as expected.

**Wiki Updates:**

- Create a **SIEM & Endpoint Protection** page with:
   - Deployment steps for SIEM and endpoint tools
   - Devices monitored and log sources
   - Alert rules and examples
   - Screenshots of SIEM dashboards and alerts
- Document any changes you made to Group Policies


### Step 5: Metric Server (Extra Credit)

**Purpose:** Monitor system and network performance for capacity planning and alerts.

**Setup Tasks:**

1. Install Metric Server
   - Deploy in Proxmox or as a dedicated VM.

2. Monitor Resources
   - Track CPU, memory, disk, and network usage for all VMs and servers.

3. Configure Alerts
   - Set thresholds for resource utilization.
   - Create alerts for downtime, overload, or unusual traffic patterns.

**Wiki Updates:**

- Create a **Metric Server** page with:
   - Configuration and setup steps
   - Screenshots of monitoring dashboards
   - Alert rules and thresholds
   - How to respond to alerts
- Document any changes you made to Group Policies

### Additional Documentation / Wiki Pages

- **Configuration Files Repository**: Include configuration files for VPN, File Server, SIEM, Endpoint Protection, and Metric Server.
- **Security Policies**: Update documentation to reflect changes in policies from this milestone:
   - Password & access control
   - VPN access restrictions
   - Endpoint protection enforcement
   - File server permissions
- **Network Diagrams**: Update to show connections to VPN, SIEM, and File Server.
- **Backup & Recovery Procedures**: Include instructions for restoring file server and metric server configurations.
- **Change Log**: Track all updates to Group Policies, firewall rules, and system configurations.


## Checklist for Wiki Update

- Create a page for **File Server Configuration** with:
   - Folder structure and mapping to groups
   - Access rights per folder
   - Backup schedules and locations
   - Troubleshooting tips
- Create a **Vulnerability Scanning** page with:
   - Tool setup and configuration
   - Scan results and screenshots
   - Risk assessment updates
   - Mitigation strategies
- Create a **VPN Server** page with:
   - Installation steps and configuration
   - Authentication methods
   - Connection instructions for remote users
   - Firewall and port forwarding configuration
   - Test results and troubleshooting steps
- Create a **SIEM & Endpoint Protection** page with:
   - Deployment steps for SIEM and endpoint tools
   - Devices monitored and log sources
   - Alert rules and examples
   - Screenshots of SIEM dashboards and alerts
- **Configuration Files Repository**: Include configuration files for VPN, File Server, SIEM, Endpoint Protection, and Metric Server.
- **Security Policies**: Update documentation to reflect changes in policies from this milestone:
   - Password & access control
   - VPN access restrictions
   - Endpoint protection enforcement
   - File server permissions
- **Network Diagrams**: Update to show connections to VPN, SIEM, and File Server.
- **Backup & Recovery Procedures**: Include instructions for restoring file server and metric server configurations.
- **Change Log**: Track all updates to Group Policies, firewall rules, and system configurations.

### Extra Credit (50 Points)
- Create a **Metric Server** page with:
   - Configuration and setup steps
   - Screenshots of monitoring dashboards
   - Alert rules and thresholds
   - How to respond to alerts