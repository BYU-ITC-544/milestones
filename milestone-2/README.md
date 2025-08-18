# Milestone 2: VM and Network Set Up

## Objective:

At the end of this milestone, your team should have all physical and virtual machines installed and a basic working network that enforces the firewall rules and VLAN segmentation defined in Milestone 1. You will also begin testing connectivity and service access to ensure the network functions as intended.


## Instructions:

- **Do not download pre-built virtual machines.** Install all machines from ISO or disk images. Cloud-init VMs are allowed.
- Configure each VM with sufficient disk space:
    - Windows Server 2022: **100 GB minimum**
    - Other Windows OS: **50 GB minimum**
    - Linux flavors: **20 GB minimum**
- **Save a snapshot** of each VM immediately after installation to allow quick recovery from mistakes.
- Your team is responsible for the integrity of the Proxmox instance; you must troubleshoot issues or rebuild if problems occur.

### Step 1: Connecting to Proxmox

- Each team has a dedicated Proxmox instance. Access credentials and VPN profiles are located in Learning Suite under `Content` > `Proxmox`.
- Access to Proxmox is **only possible via the VPN**. All VMs will be hosted in your Proxmox instance.
- System resources available per instance:
  - **2 TB storage**
  - **253 GB RAM**
  - **50 CPU cores**

### Step 2: Cables

- You must create the majority of network cables yourself.
- The only exceptions are cables connecting the patch panel to your Proxmox server.
- Ensure proper cable termination, bonding, and LACP where required to avoid connectivity issues.


### Step 3: Networking

- Configure **virtual switches** and **VLANs** on both your firewall and hypervisor.
- Each team has **10 VLANs** to use. VLAN IDs, switch ports, and WAN IP ranges are assigned as follows:

| Team Number | VLAN Range| Switch Ports | VPN Port | WAN IP Range | Proxmox URL |
| -- | ------- | ----- | ---- | --------------------------| ------------------------- |
| 1  | 200-209 | 13-14 | 1347 | 172.16.40.10-172.16.40.11 | https://172.16.40.10:8006 |
| 2  | 210-219 | 15-16 | 1348 | 172.16.40.12-172.16.40.13 | https://172.16.40.12:8006 |
| 3  | 220-229 | 17-18 | 1349 | 172.16.40.14-172.16.40.15 | https://172.16.40.14:8006 |
| 4  | 230-239 | 19-20 | 1350 | 172.16.40.16-172.16.40.17 | https://172.16.40.16:8006 |
| 5  | 240-249 | 21-22 | 1351 | 172.16.40.18-172.16.40.19 | https://172.16.40.18:8006 |
| 6  | 250-259 | 23-24 | 1352 | 172.16.40.20-172.16.40.21 | https://172.16.40.20:8006 |
| 7  | 260-269 | 25-26 | 1353 | 172.16.40.22-172.16.40.23 | https://172.16.40.22:8006 |
| 8  | 270-279 | 27-28 | 1354 | 172.16.40.24-172.16.40.25 | https://172.16.40.24:8006 |
| 9  | 280-289 | 29-30 | 1355 | 172.16.40.26-172.16.40.27 | https://172.16.40.26:8006 |
| 10 | 290-299 | 31-32 | 1356 | 172.16.40.28-172.16.40.29 | https://172.16.40.28:8006 |

- Both assigned switch ports **must be used** and properly bonded for LACP.
- The first IP in the WAN IP range is already assigned to Proxmox; the second is used for your router WAN interface.


### Step 4: Firewall & Router

- Recommended firewall/router options: **OPNsense** or **PfSense**. Other solutions are allowed but unsupported by TAs.
- **Install the firewall first** and verify internet connectivity.

#### VLAN Configuration Hint:

- Tagged VLAN traffic must be considered when creating the VM:

  1. Create **separate network interfaces** for each VLAN, or
  2. Create a **single interface** handling multiple VLANs and configure tagging inside the VM.

#### Firewall & VLAN Best Practices:

- **Apply the principle of least privilege:**
    - Allow only the traffic necessary between VLANs.
    - Deny all other inter-VLAN traffic by default.
    - Enable logging on deny rules to monitor unauthorized attempts.

- **Test connectivity:** Install a test VM in each VLAN and validate:
    - Ping, traceroute, DNS resolution, nmap and application-level access.
    - Verify that only intended services can communicate across VLANs.
        - This will not be possible for all services since they have not yet been set up.

#### Firewall Rule Clarifications

- **Default & auto-generated rules:**
    - Firewalls like OPNsense create rules automatically. These may be hidden and/or non-editable.
- **Rule icons:**
    - ❌ Block rule
    - ▶ Allow rule
    - → Traffic relative to interface (inbound)
    - ← Traffic relative to interface (outbound)
- **Network selection in rules:**
    - `<Network Name> net` → Entire subnet
    - `<Network Name> address` → Only gateway IP

### Rule Fields & What They Mean

| Field                | Description                                                                                                                                          | Example                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| **Protocol**         | Traffic type (IPv4, IPv6, TCP, UDP, ICMP, etc.)                                                                                                      | IPV4 and TCP for web traffic                                        |
| **Source**           | Where the traffic originates. Can be: <br>• A single IP <br>• A network range <br>• A named network in OPNsense <br>• An alias (custom group of IPs) | 192.168.10.25/32 (single IP) <br> 192.168.10.0/24 (network) |
| **Source Port**      | The originating port of the traffic (usually random for client traffic). Often left as “any.”                                                        | Any                                                          |
| **Destination**      | Where the traffic is going (same options as source).                                                                                                 | 192.168.20.10 (database server)                            |
| **Destination Port** | The port on the destination system the traffic is targeting.                                                                                         | 443 (HTTPS)                                                |
| **Gateway**          | The gateway traffic uses (for policy-based routing).                                                                                                 | WAN Gateway, VPN Gateway                                     |
| **Schedule**         | Allows the rule to be active only at specific times/days.                                                                                            | Block social media during work hours                         |


#### Example Firewall Rules

| Action | Interface | Direction | Protocol | Source  | Source Port | Destination   | Dest Port | Description                       |
| ------ | --------- | --------- | -------- | ------- | ----------- | ------------- | --------- | --------------------------- |
| Allow  | LAN       | In        |IPV4 TCP      | LAN Net | Any         | 192.168.20.10 | 3306      | Allow Accounting VLAN to DB |
| Allow  | LAN       | In        | IPV4 TCP/UDP  | LAN Net | Any         | Any           | 53        | Allow DNS queries           |
| Block  | LAN       | In        | Any      | Any     | Any         | Any           | Any       | Block all other traffic     |

> Note that most firewalls include a default “deny all” rule at the end of the rule set. This rule is usually auto-generated and cannot be removed or altered.


### Step 5: VM Set Up

**Installation Guidelines:**

- Base OS installation only is sufficient for now; service configuration can follow in later milestones.
- Assign VMs to the correct VLAN.
- **Use static IPs** for servers/infrastructure; DHCP (with reservations) for workstations.
- **Create a local backup admin account** not tied to Active Directory on every server/workstation:
    - Example: `Username: localadmin`
    - Store passwords securely in a vault.
- Apply **basic OS hardening:**
    - Change default credentials
    - Disable unnecessary services
    - Enable OS-level firewall

**VLAN & Resource Verification:**
- Confirm VLAN assignments.
- Ensure firewall rules enforce **least privilege**:
    - Servers accessible only by necessary VLANs
    - Inter-VLAN communication restricted unless explicitly allowed

**Web Server & Port Forwarding:**
- Install selected web server software (Apache, Nginx, etc.).
- Configure firewall port forwarding to allow external HTTP/HTTPS traffic from WAN → Web Server VLAN.
- Test access from an external network.


### Step 6: Proxmox Organization Best Practices

- **Tags:** Assign descriptive tags for each VM.
    - Role-based: `web-server`, `db-server`, `dns`, `workstation`
    - Environment: `production`, `testing`, `development`
    - Project: `spicy-cluck`, `milestone-3`

- **Pools:** Organize VMs into logical groups for easier management:
    - `Infrastructure`: AD, DNS, DHCP, firewall
    - `Applications`: Web, DB servers
    - `Workstations`: User desktops, test machines

- **Best practices:**
    - Consistent naming for tags and pools
    - Document VLAN assignments, IPs, and service dependencies in Proxmox notes
    - Update tags/pools as systems change


### Step 7: Documentation for the Wiki

Documentation is a crucial part of being a sysadmin. For Milestone 2, your team must create and update Wiki pages that fully document your VM installations, firewall rules, VLAN configurations, and Proxmox organization. All documentation must include **proof of operation** (screenshots, logs, test results) and must stay consistent with the actual configuration.

Additionally, **all physical cables must pass testing and be built to a professional standard**. Improperly terminated or untested cables will result in lost points.

### Milestone 2 Wiki Sections

1. **Updates Only (Technologies & Software)**
    - Document **only updates or changes** to OS versions, firewall software, web server software, and hypervisor tools.
    - Include verification screenshots or command outputs where changes are made.

1. **Network Design**
   - Updated **Logical Diagram** (VLAN assignments, switch port bonding, firewall/router placement).
   - Updated **Physical Diagram** (VM placement, switch connections, WAN connectivity).
   - **VLAN Table** with IDs, names, and usage.
   - Confirmation that physical cables are correctly terminated, tested, and bonded with LACP where required.

1. **Hosts Inventory**
    - Complete table for all VMs and physical machines including:
        - Hostname
        - IP address (static or DHCP)
        - Assigned VLAN
        - Role (Web server, DB server, workstation, etc.)
        - Local backup admin account created
        - Status (installed/configured/tested)
    - Screenshots verifying installation/configuration.

1. **Router**
    - Document router role (edge routing, DHCP relay, static routes).
    - WAN interface configuration (IP, gateway, DNS).
    - Internal interface configurations (VLAN interfaces, routing tables).
    - Routing protocol setup (if applicable: static, OSPF, etc.).
    - NAT configuration.
    - Connectivity test evidence (ping/traceroute to external sites, routing table screenshots).

1. **Firewall Rules**
    - Document all rules created:
        - Source, destination, ports, protocols
        - Rule type (allow/block)
        - Rule ordering and justification
    - Include evidence of tested rules (ping, traceroute, DNS resolution, service access).
    - Backup/export of firewall configuration included.
    
7. **Hardware Planning**
    - Document Proxmox allocations:
        - Storage, RAM, CPU per VM
        - Physical workstation connections and switch ports
        - Cable assignments and LACP bonding configuration
    - Document VM tagging and pooling strategy.

8. **Assumptions & Justifications**
    - Note assumptions about VLAN usage, IP assignments, service dependencies.
    - Justify firewall rules, VLAN segmentation, and port assignments.
    - Rationale for creating local backup admin accounts.


### Checklist for Wiki Update
 
- Update the for **Technologies & Software** with (10 Points):
    - Changes to OS/software documented
    - Firewall/web/hypervisor updates included
    - Verification screenshots provided

- Update the page for **Network Design** with (20 Points):
    - Updated logical and physical diagrams
    - VLAN table completed and accurate
    - Physical cable testing results and bonding configuration documented

- Update the page for **Hosts Inventory** with (10 Points):
    - Hostnames, IPs, VLANs, roles, statuses documented
    - Local backup admin accounts listed
    - Screenshots of installation/configuration included

- Update the page for **Firewall Rules** with (20 Points):
    - All rules listed with details
    - Evidence of tested rules provided
    - Backup/export attached

- Create a page for the **Router** (20 pts) with:
    - WAN + internal interface configs documented
    - Static/dynamic routes listed
    - NAT configuration included
    - Routing table screenshots included
    - Connectivity test results provided
    - Config backup included

- Update the page for **Hardware Planning** with (20 Points):
    - Proxmox resource allocations detailed
    - Switch/cable assignments documented
    - VM tagging/pooling explained


### Important Note on Scoring

Points are awarded only if the **documentation matches the implemented system**:

* **Documentation Accuracy** – Must reflect the actual network/VM setup.
* **Functional Verification** – Every documented feature must be installed, configured, and tested.
* **Consistency** – All system changes must be updated in the Wiki.
* **Evidence of Operation** – Screenshots, logs, or test results must be included.
* **Cable Verification** – All physical cables must be tested and documented as passing to standard.

If documentation exists but the feature (or cable build) is not functional, **no points will be awarded**.