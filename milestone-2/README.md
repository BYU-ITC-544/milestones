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
| 3  | 220-229 | 17-18 | 1348 | 172.16.40.14-172.16.40.15 | https://172.16.40.14:8006 |
| 4  | 230-239 | 19-20 | 1349 | 172.16.40.16-172.16.40.17 | https://172.16.40.16:8006 |
| 5  | 240-249 | 21-22 | 1350 | 172.16.40.18-172.16.40.19 | https://172.16.40.18:8006 |
| 6  | 250-259 | 23-24 | 1351 | 172.16.40.20-172.16.40.21 | https://172.16.40.20:8006 |
| 7  | 260-269 | 25-26 | 1352 | 172.16.40.22-172.16.40.23 | https://172.16.40.22:8006 |
| 8  | 270-279 | 27-28 | 1353 | 172.16.40.24-172.16.40.25 | https://172.16.40.24:8006 |
| 9  | 280-289 | 29-30 | 1354 | 172.16.40.26-172.16.40.27 | https://172.16.40.26:8006 |
| 10 | 290-299 | 31-32 | 1355 | 172.16.40.28-172.16.40.29 | https://172.16.40.28:8006 |

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


### Step 7: Documentation

Documentation is a crucial part of being a sys admin. For the technical documenation you will create a wiki that contains all the needed technical documenation

- Update Milestone 1 diagrams and tables to reflect changes.
- Record all test results as a baseline for troubleshooting.

### Submission Requirements

**Home / Overview**
- Update **Current Milestone** to “Milestone 2: VM and Network Set Up.”
- Add the date of the latest update.
- Include a short summary of progress (e.g., “All VMs installed, firewall configured, VLANs segmented”).

**Technologies & Software**
- Add OS versions for each VM (Windows Server 2022, Windows 10/11, Linux flavors).
- Include firewall software (OPNsense/PfSense), web server software, and any hypervisor tools (Proxmox version, network plugins).

**Network Design**
- Update **Logical Diagram** to reflect VLAN assignments, switch port bonding, and firewall/router placement.
- Update **Physical Diagram** to show actual VM placement, switch connections, and WAN connectivity.
- Update **VLAN Table** to include IDs, names, and intended usage (servers, workstations, management, guest Wi-Fi).

**Hosts Inventory**
- Add all installed VMs and physical machines with:
  - Hostname
  - IP address (static or DHCP assigned)
  - Assigned VLAN
  - Role (Web server, DB server, workstation, etc.)
  - Backup local admin account created
  - Status (installed / configured / tested)
- Include screenshots where possible to validate VM setup.

**Firewall Rules**
- Include all rules created, following least privilege principle:
    - Source, destination, ports, protocols
    - Rule type (allow/block)
    - Rule ordering and justification
- Include evidence of tested rules (ping, traceroute, service access).
- Mention default deny rule and auto-generated rules.
- Include a backup of the current firewall rules that can be imported if needed.

**Policies**
- Update **Disaster Recovery** section to reflect VM snapshot strategy.
- Include notes on testing procedures for connectivity and firewall verification.
- Ensure local admin account policies and VLAN segregation principles are documented.

**Hardware Planning**
- Update to reflect Proxmox resources used:
    - Storage, RAM, CPU allocated per VM.
    - Physical workstation connections and switch ports used.
    - Cable assignments and LACP bonding info.
- Include VM tagging and pooling strategy in Proxmox.

**Assumptions & Justifications**
- Note any assumptions made about VLAN usage, IP assignments, or service dependencies.
- Justify why certain firewall rules, VLAN segmentation, or port assignments were chosen.
- Include rationale for creating local backup admin accounts on servers/workstations.
