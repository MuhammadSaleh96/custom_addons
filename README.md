# Project Extension Module

### Summary
This custom module that enhances Odoo's Project Management capabilities by adding custom fields, improving project forms, and providing dynamic behavior for project attributes. It also extends the Project List View with additional details and introduces custom filters for more efficient data retrieval. The module aims to streamline project management for different industries and improve visibility of key project metrics.

## Overview

- **Server:** AWS Ubuntu instance
- **Odoo Version:** Odoo 18 Community Edition
- **Module:** `project_extension` (Enhancements for Project Management)

## Prerequisites

Ensure you have the following before proceeding:

- A working server or instance with minimum 10 GB (for a basic installation without large data storage).
- SSH access the server or instance.
- `project_extension.zip` file (or GitHub repository link https://github.com/MuhammadSaleh96/custom_addons.git) module.
- Visual Studio Code or PyCharm for your development workspace.

## Features Overview

### **Project Form View Enhancements**
- New fields added:
  - `project_type`
  - `industry_type`
  - `client_priority`
  - `expected_revenue`
  - `contract_signed`
- Dynamic behavior using Python to update fields based on user input.

### **Project List View Modifications**
- Displays additional fields for better visibility:
  - `project_type`
  - `industry_type`
  - `client_priority`
  - `expected_revenue`
  - `contract_signed`

### **Custom Filters for Data Retrieval**
- **High-Priority Projects:** Filters projects where `client_priority = High`.
- **Active Contracts:** Filters projects where `contract_signed = True`.
- **Government Projects:** Filters projects where `project_type = Government`.
- **Revenue Above 100,000:** Filters projects where `expected_revenue > 100,000`.

## Installation Guide

### Step 1: Logging in to Your Server

If your server requires a PEM key for authentication, use the following command:

```bash
ssh -i /path/to/your/key.pem username@server_ip_address
```

- `/path/to/your/key.pem`: Replace with the full path to your PEM key file.
- `username`: Replace with your server's username.
- `server_ip_address`: Replace with your server’s IP address.

### Step 2: Update the Server

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Step 3: Secure the Server

```bash
sudo apt-get install -y openssh-server fail2ban
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
sudo systemctl status fail2ban
```

### Step 4: Install Packages and Libraries

```bash
sudo apt-get install -y python3-pip python3-dev libxml2-dev libxslt1-dev zlib1g-dev \
    libsasl2-dev libldap2-dev build-essential libssl-dev libffi-dev libmysqlclient-dev \
    libjpeg-dev libpq-dev libjpeg8-dev liblcms2-dev libblas-dev libatlas-base-dev npm
```

Create a symlink for Node.js:
```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

Install required Node.js packages:
```bash
sudo npm install -g less less-plugin-clean-css
sudo apt-get install -y node-less
```

### Step 5: Set Up PostgreSQL

```bash
sudo apt-get install -y postgresql
sudo su - postgres -c "createuser --createdb --username postgres --no-createrole --superuser --pwprompt odoo"
exit
```

### Step 6: Create Odoo System User

```bash
sudo adduser --system --home=/opt/odoo --group odoo
```

### Step 7: Get Odoo 18 Community Edition

```bash
sudo apt-get install -y git
sudo su - odoo -s /bin/bash
cd /opt/odoo
git clone https://www.github.com/odoo/odoo --depth 1 --branch 18.0 --single-branch .
exit
```

### Step 8: Install Python Dependencies

```bash
sudo apt install -y python3-venv
sudo python3 -m venv /opt/odoo/venv
source /opt/odoo/venv/bin/activate
pip install -r /opt/odoo/requirements.txt
```

Install wkhtmltopdf:
```bash
sudo wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
sudo dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb
sudo apt install -f
```

### Step 9: Configure Odoo 18

```bash
sudo cp /opt/odoo/debian/odoo.conf /etc/odoo.conf
sudo nano /etc/odoo.conf
```

Modify the file with the following settings:

```ini
[options]
admin_passwd = admin
db_host = localhost
db_port = 5432
db_user = odoo18
db_password = 123456
addons_path = /opt/odoo/addons
logfile = /var/log/odoo/odoo.log
```

Set permissions (optional):
```bash
sudo chown odoo: /etc/odoo.conf
sudo chmod 640 /etc/odoo.conf
```

### Step 10: Create Odoo Service

```bash
sudo nano /etc/systemd/system/odoo.service
```

Add the following content:

```ini
[Unit]
Description=Odoo18
Documentation=http://www.odoo.com

[Service]
Type=simple
User=odoo
ExecStart=/opt/odoo/venv/bin/python3 /opt/odoo/odoo-bin -c /etc/odoo.conf

[Install]
WantedBy=default.target
```

Set permissions and start the service:
```bash
sudo chmod 755 /etc/systemd/system/odoo.service
sudo chown root: /etc/systemd/system/odoo.service
sudo systemctl start odoo.service
sudo systemctl enable odoo.service
```

Access Odoo in your browser:
```bash
http://<your_domain_or_IP_address>:8069
```

### Step 11: Add Project Extention Module

Connect to your server or instance:
```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```
Navigate to your Odoo addons directory:
```bash
cd /opt/odoo/custom_addons
```
Clone the repository:
```bash
git clone https://github.com/MuhammadSaleh96/custom_addons.git
```
restart odoo service:
```bash
sudo service odoo18 restart
```

---


### Testing Module Instructions
1. **Use an Existing Custom Module or This Repository**:
   - You can either use your own custom module or clone this repository and proceed with the setup.
2. **Start Odoo**: Ensure Odoo is running:
   ```sh
   sudo systemctl start odoo.service
   ```
3. **Log in to Odoo**:
   - Open a browser and navigate to `http://<your_domain_or_IP_address>:8069`
   - Use the configured admin username and password.

4. **Activate Developer Mode & Activate/Install Modules**:
   - Navigate to `Settings > General Settings`
   - Scroll down to the bottom under `Developer Tools > Enable Developer Mode`
   - Go to `Home Menu` on the Top-left corner Icon then click on `Apps > Update List Apps`
   - Click the `Update` button (note: this will let you see the custom project extention module in modules list panel)
   - Go to `Home Menu` on the Top-left corner Icon
   - Select `Apps` then type `Project` or `project` in the search bar (note: the module has a tic symbol icon)
   - Click on the `Activate` button to install and load project management module in odoo 
   - Now search for `Project Extension` or `project extension` in search bar, make sure to clear the filter 
   - Click on the `Activate` button to install and load the custom project extension module 

5. **New Project Extension Form**
   - Go to `Home Menu` on the Top-left corner Icon
   - Select `Project` from the drop-down menu
   - Click on `New` button to create a new project
   - Fill in the custom fields
   - Check the dynamic fields behavior  
     ![Dynamic Fields](images/Screenshot%202.png)
   - Click on `Create Project`
   - Click on `Projects` on the top menu bar
   - Verify that the project list view displays the new fields under two icon buttons in the image below  
     ![Project List View](images/Screenshot%203.png)

6. **Editing Existing Project Extension Form**  
   - Go to `Project` under `Home Menu` on the Top-left corner Icon  
   - Click on the `List View` Icon and choose any of the existing projects  
     ![List View Icon](images/Screenshot%204.png)  
   - Edit in the custom fields  
   - Check the dynamic fields behavior  
     ![Dynamic Fields](images/Screenshot%205.png)  
   - Save the project after editing the required fields by clicking on the icon shown in the image below  
     ![Save Project](images/Screenshot%206.png)

7. **Custom Filters Project Extension**
   - Go to `Project` under `Home Menu` on the Top-left corner Icon
   - Click on the arrow icon in the search bar and verify custom filters are retriving projects accordantly
    ![Custom Filters](images/Screenshot%207.png)

8. **Troubleshooting**  
   - Check the Odoo logs using the terminal:  
     
     ```bash
     tail -f /var/log/odoo/odoo.log
     ```

### Conclusion
 The project_extension module enhances Odoo’s Project Management capabilities by adding necessary fields, improving the user interface, and enabling advanced filtering options