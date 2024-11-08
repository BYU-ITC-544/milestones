# Milestone 4: Systems Set Up

## Objective:

Configure the:
- Web server
- Database server
- File server
- Vulnerability Scanner
- VPN server
- SIEM (Extra Credit)

## Instructions:

### Step 1: Database Server

Run these commands to set up your database server.

1. To begin update your machine and install the SQL server. We will use MariaDB for our SQL server.
    ```bash
    sudo apt update -y && sudo apt install mariadb-server -y
    ```

1. MariaDB comes with a script that helps you improve the security of your MariaDB installation. Run this script to set a root password, remove anonymous users, disallow root login remotely, and remove test databases.

    ```bash
    sudo mariadb_secure_installation
    ```

    You will be prompted with several questions. It's generally recommended to answer `Y` (yes) to all questions to improve the security of your MariaDB installation.

1. Ensure that the MariaDB service is started and will start automatically at boot.

    ```bash
    sudo systemctl start mariadb && sudo systemctl enable mariadb
    ```

1. Check the status of the MariaDB service to ensure it's running correctly.

    ```bash
    sudo systemctl status mariadb
    ```

    You should see an output indicating that the service is active (running).

1. Log in to the MariaDB server as the root user to verify the installation.

    ```bash
    sudo mariadb
    ```

    You should see the MariaDB prompt (`MariaDB [(none)]>`), indicating that you have successfully logged in.

    <div style="page-break-after: always"></div>    

1. Create a new database and a user with permission to access it, follow these steps:

    1. Create a new database:
        ```sql
        CREATE DATABASE betterblog;
        ```

    1. Create a new user and grant it permissions on the database:
        ```sql
        CREATE USER 'betterblog'@'%' IDENTIFIED BY 'Fraying3-Bring-Rebuff';
        GRANT ALL PRIVILEGES ON betterblog.* TO 'betterblog'@'%';
        FLUSH PRIVILEGES;
        ```

    1. Exit the MariaDB prompt:
        ```sql
        EXIT;
        ```

1. Using a flash drive, import the database from the `database.sql` file
    ```bash
        mariadb -u root -p betterblog < /path/to/file.sql
    ```

<div style="page-break-after: always"></div>

1. To allow remote connections, you may need to edit the MySQL configuration file.

    1. Open the MariaDB configuration file:
        ```bash
        sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
        ```

    1. Find the line containing `bind-address` and change its value from `127.0.0.1` or whatever value is there to `0.0.0.0`:
        ```bash
        bind-address = 0.0.0.0
        ```

    1. Save the file and exit the editor.

    1. Restart MariaDB to apply the changes:
    ```bash
    sudo systemctl restart mariadb
    ```

1. From your database machine, test the remote connection to ensure it works.

    ```bash
    mariadb -u betterblog -p -h <IP ADDRESS>
    ```

You should be prompted for the password of `betterblog`. If everything is set up correctly, you will be connected to the MariaDB server.

<div style="page-break-after: always"></div>

### Step 2: Web Server 

Run these commands to set up your web server. Since this is not a web class the TAs will assist if needed in getting your website setup. 

1. Start by installing the web server software
    ```bash
    sudo apt install apache2 -y
    ```
1. Install PHP and the necessary PHP modules.

    ```bash
    sudo apt install php libapache2-mod-php php-mysql -y
    ```
1. Create a directory for your website in the `/var/www` directory.

    ```bash
    sudo mkdir /var/www/betterblog
    ```
1. Set the ownership of the directory to the Apache user.

    ```bash
    sudo chown -R www-data:www-data /var/www/betterblog
    ```
1. Copy over the betterblog files that you were given on the USB drive and place them in `/var/www/betterblog`

1. Create a new virtual host configuration file for your website.

    ```bash
    sudo nano /etc/apache2/sites-available/betterblog.conf
    ```

1. Add the following configuration to the file:

    ```apache
    <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        ServerName betterblog.com
        DocumentRoot /var/www/betterblog

        <Directory /var/www/betterblog>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```
1. Save the file and exit the editor.
1. Enable the new virtual host configuration.

    ```bash
    sudo a2ensite betterblog
    ```
1. Disable the default site if you no longer need it.

    ```bash
    sudo a2dissite 000-default
    ```
1. Reload Apache to apply the changes.

    ```bash
    sudo systemctl reload apache2
    ```
1. Within the `/var/www/betterblog` files, edit the config.json to have the following values
    ```json
    "database_host": "<db ip address>",
    "database_user": "betterblog",
    "database_password": "Fraying3-Bring-Rebuff",
    ```

### Step 3: File server

1. **Set Up the Central File Server**  
   - Install and configure a file server (e.g., NFS or Samba).

1. **Set Access Rights**  
   - Define and assign appropriate access rights (read, write, execute) to different directories and files based on user roles.

1. **Connect Workstation Computers**  
   - Connect all the workstation computers to the central file server, ensuring proper authentication and network configuration.

1. **Test CRUD Operations**  
   - From each workstation, test **Create, Read, Update, and Delete** (CRUD) operations on the file server to verify that access rights and functionality are working as expected.

### Step 4: Vulnerability Scanning

1. **Install a Vulnerability Scanning Tool**  
   - Install **OpenVAS** or another vulnerability scanning tool of your choice.

1. **Scan All Virtual Machines (VMs)**  
   - Run vulnerability scans on all your VMs.
   - Document the results, including any identified vulnerabilities that may need to be addressed.

1. **Set Scan Schedules**  
   - Configure regular, automated scans to continuously monitor for new vulnerabilities.
   - Configure automated updates to your CVE database(s)

1. **Update Your Risk Assessment**  
   - Update your risk assessment by incorporating any newly discovered risks and corresponding mitigations.
   - Optionally, use one team member's Homework 2 as a base for your updated assessment and include it in your documentation for this milestone.

### Step 5: VPN Server

- Set up a VPN server to allow remote and hybrid workers access to necessary resources.
- Authentication: Use both username/password and multi-factor authentication (MFA).
- Public IP address for remote access: **128.187.49.253**.
- Port forwarding for VPN traffic: Your team's port can be found in Learning Suite under `Content > Proxmox`.
- Ensure DNS resolution for internal resources.
- Use strong encryption (AES-256 or higher).
- Apply SSL/TLS certificates for secure connections.
- Enable logs for connection auditing and troubleshooting.

### Step 6: SIEM set up - Extra Credit

- Select a SIEM solution that best suits your network. Some possibilities are (Splunk, ELK Stack (Elasticsearch, Logstash, Kibana), and Security Onion)
- Consider which devices you need to and can collect logs from. Possibilities include:
   - Workstations
   - Wervers
   - Eouters
   - Hypervisor
- Set up your chosen SIEM solution and collect logs from the necessary devices
- Use preset default or set up some of your own alerts and then trigger them to test they are working as intended but you will need at least 5 working and useful alerts.

### Extra Credit

- 100 Points - Fully functioning SIEM solution that collects live logs from servers, network devices, and workstations and has at least 5 alerts that are functioning. Documentation on the setup configuration and alerts must also be written.

### Requirements

- 5 Points - Webserver  
    - The web server has been set up and is accessible from the CSRL network  
    - Users can use the website without any errors 
- 5 Points – Database  
    - Database has been setup   
    - The database has a secure config  
    - The database has the correct tables for the website  
- 20 Points - File Server  
    - The file server has been setup   
    - The file server has a secure config  
    - The file server can be accessed from the workstations  
    - Users can perform CRUD operations on the folders and files within their permission group  
- 20 Points - VPN Server
    - The VPN server has been set up to meet all of the specified criteria  
- 10 Points - A vulnerability scanning tool has been installed  
- 20 Points - Vulnerability Scanning of all VMs and workstations has been completed and schedules are set to scan the network at regular intervals   
- 20 Points - Document all the config files and explain and security principles and practices used  

The lab pass-off will be done with a TA and the documentation should be uploaded to Learning Suite. Documentation must be submitted as a PDF.
