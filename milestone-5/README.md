# Milestone 5: Backup and Disaster Recovery Policy


## Objective


The purpose of Milestone 5 is to establish a comprehensive framework for protecting organizational data and ensuring business continuity in the event of hardware failures, human error, cyberattacks, or natural disasters. This milestone combines both **backup procedures** and **disaster recovery planning**, ensuring that all critical systems, data, and services can be restored promptly and securely.


A well-designed Backup and Disaster Recovery (DR) Policy ensures:


- Protection of data integrity, confidentiality, and availability
- Rapid recovery of systems and data after incidents
- Compliance with regulatory and industry standards
- Continuity of business operations with minimal downtime


## Part 1: Backup Policy


### 1. Purpose


A backup policy defines how organizational data is regularly copied, stored, and maintained to protect against accidental loss, corruption, or unauthorized access.


### 2. Key Elements


- **Data Retention**
   - Define retention periods for different data types (e.g., configurations, financial, marketing, sales, etc.)
   - Ensure retention meets legal, compliance, and operational requirements


- **Frequency of Backups**
   - Critical servers and databases
   - Workstations and less critical systems


- **Backup Types**
   - Full backups, incremental backups, and differential backups
   - Choose type based on recovery objectives and storage efficiency


- **Storage Media**
   - Local disks, NAS, SAN, or cloud storage
   - Ensure redundancy across multiple storage locations


- **Off-Site Backups**
   - Maintain off-site copies for disaster recovery
   - Include cloud backups or geographically separated physical storage


- **Encryption and Security**
   - Encrypt all backup files in transit and at rest
   - Restrict access using role-based access controls


- **Testing and Verification**
   - Periodically restore backups to verify integrity and functionality
   - Document the success/failure of test restores


- **Backup Automation**
   - Automate backup tasks using scripts or management tools
   - Ensure logs are maintained and reviewed regularly


- **Monitoring and Alerts**
   - Generate notifications for backup completion, failures, or errors
   - Maintain audit trails for compliance


- **Documentation and Review**
   - Record backup schedules, storage locations, encryption methods, and retention policies
   - Update documentation regularly


- **Scalability and Growth**
   - Ensure backup infrastructure can scale with increasing data volume
   - Regularly review storage capacity and upgrade as needed


- **Compliance and Regulatory Requirements**
   - Align backups with industry-specific standards (e.g., HIPAA, GDPR, SOX)


- **Disaster Recovery Planning**
   - Integrate backups with disaster recovery procedures
   - Define recovery point objectives (RPO) and recovery time objectives (RTO)


- **Regular Review and Testing**
   - Schedule periodic reviews of the backup policy
   - Conduct simulation tests to validate procedures


### 3. Recommended Backup Strategy: 3-2-1-1-0 Rule


To maximize resilience against data loss and ransomware, the organization will follow the **3-2-1-1-0 backup rule**:


- **3** — Maintain **three copies** of all important data
- **2** — Store the copies on **two different types of media**
- **1** — Keep **one backup copy offsite**
- **1** — Keep **one backup copy offline or air-gapped**
- **0** — Ensure **zero backup errors**


### 4. Difference Between 3-2-1 and 3-2-1-1-0


| Feature                 | 3-2-1 Rule | 3-2-1-1-0 Rule |
| ----------------------- | ---------- | -------------- |
| Total Copies            | 3          | 3              |
| Different Media Types   | 2          | 2              |
| Offsite Copy            | 1          | 1              |
| Offline/Air-Gapped Copy | ❌         | ✅            |
| Zero Backup Errors      | ❌         | ✅            |
| Ransomware Protection   | Limited    | Strong         |
| Data Integrity Checks   | Optional   | Mandatory      |




The **3-2-1 rule** is a foundational best practice, but the **3-2-1-1-0 rule** strengthens security by adding an offline/air-gapped backup (protecting against ransomware and malicious deletions) and requiring error-free verification through regular testing.


## Part 2: Disaster Recovery (DR) Policy


### 1. Purpose


The Disaster Recovery Policy provides a structured approach to restoring systems, networks, and applications after a disruption. DR focuses on minimizing downtime and preventing loss of critical data or services.


### 2. Key Elements


- **Risk Assessment and Business Impact Analysis (BIA)**
   - Identify threats and vulnerabilities to IT systems
   - Determine which systems are critical for operations


- **Recovery Objectives and Priorities**
   - Define Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) for each system


- **Roles and Responsibilities**
   - Assign a DR team with clear responsibilities for executing recovery procedures


- **Contact Information**
   - Maintain up-to-date contact info for internal staff, vendors, and emergency services


- **Data Backup and Restoration Procedures**
   - Reference backup policy for data restoration methods
   - Define step-by-step procedures for restoring critical systems


- **Disaster Recovery Site**
   - Identify a secondary site for operations if the primary site is unavailable
   - Include network, hardware, and software resources


- **Hardware and Software Inventory**
   - Maintain an inventory of servers, networking devices, workstations, and applications
   - Ensure compatible replacement equipment is available


- **Network Infrastructure**
   - Document network topology, VPN access, firewall rules, and routing
   - Include procedures to restore connectivity after an outage


- **Application Recovery Procedures**
   - List critical applications and dependencies
   - Provide instructions for reinstalling or restoring application data


- **Testing and Maintenance**
   - Conduct scheduled DR drills and tabletop exercises
   - Update DR plans based on test results


- **Training and Awareness**
   - Educate staff on their roles during a disaster
   - Conduct periodic refresher training


- **Vendor and Supplier Contingency Plans**
   - Ensure third-party vendors have recovery capabilities
   - Include service-level agreements (SLAs) for critical services


- **Financial and Legal Considerations**
   - Include insurance, compliance obligations, and potential financial impact


- **Emergency Response Procedures**
   - Define immediate actions to take during incidents (power failure, cyberattack, natural disaster)


- **Incident Reporting and Escalation**
   - Establish reporting channels and escalation steps for serious incidents


- **Communication Plan**
   - Outline internal and external communication strategies
   - Ensure stakeholders are informed throughout recovery


- **Post-Recovery Evaluation**
   - Conduct a review after disaster events or drills
   - Identify lessons learned and update policies accordingly


## Part 3: Integration and Documentation


- Create a new **“Backup and Disaster Recovery”** section in your project wiki.


- Include separate sections for:
   - **Backup Policy** (with all sections above)
   - **Disaster Recovery Policy** (with all sections above)
   - **Testing and Verification Logs** (How you would do this)
   - **Recovery Procedures and Checklists**


- Link any relevant network diagrams, VM inventories, and firewall rules that support recovery procedures.


- Include references to off-site backup locations, disaster recovery sites, and contact lists for responsible personnel.


### Submission Requirements


- The completed Milestone 5 documentation must be **uploaded to the project wiki**.
- Ensure that all sections are complete, clearly formatted, and accessible to other system administrators.
- Include references to any diagrams, policies, scripts, or configuration files that support the backup and DR plan.


### Grading


- **50 Points** — Backup Policy
- **50 Points** — DR Policy



