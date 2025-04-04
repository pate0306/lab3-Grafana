# Lab 3 – Grafana Installation and Dashboard Creation for Ubuntu Server Performance

**Course**: CST 8919 – DevOps Security and Compliance  
**Lab**: 3  
**Topic**: Grafana Setup, Azure Monitor Integration, and Dashboard Creation  
**Author**: [Your Name]  
**Date**: [Submission Date]  

---

## 🔧 Objective

This lab focuses on installing Grafana on an Ubuntu server, connecting it to Azure Monitor via Managed Identity, and visualizing system performance metrics on a Grafana dashboard.

---

## 🧱 Prerequisites

- Ubuntu Server 18.04 or later
- Azure account with permissions to manage resources
- Basic Linux command-line knowledge

---

## ✅ Steps Performed

### 🖥️ Task 1: Prepare Ubuntu Server

```bash
sudo apt-get update && sudo apt-get upgrade
```

---

### 📥 Task 2: Install Grafana

1. **Install dependencies and add Grafana APT repo**:

```bash
sudo apt-get install -y apt-transport-https software-properties-common wget
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get install grafana
```

2. **Start and enable the Grafana server**:

```bash
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

3. **Verify service status**:

```bash
sudo systemctl status grafana-server
```

---

### 🌐 Task 3: Connect Grafana to Azure Monitor

1. Enabled **Managed Identity** on the Azure VM.

2. Assigned the following roles:
   - **Monitoring Reader** on Azure Monitor
   - **Reader** on the subscription

3. Edited `/etc/grafana/grafana.ini` to allow managed identity authentication.

4. Restarted Grafana:

```bash
sudo systemctl stop grafana-server
sudo systemctl start grafana-server
```

5. Accessed Grafana at: `http://<vm-ip>:3000`

6. Logged in with default credentials: `admin/admin`

7. Navigated to:
   - **Configuration > Data Sources**
   - Added **Azure Monitor**
   - Chose **Managed Identity** authentication
   - Saved and tested connection

---

### 📊 Task 4: Create Grafana Dashboard

1. Created a new dashboard and added a panel.
2. Selected **Azure Monitor** as the data source.
3. Chose relevant metrics like:
   - CPU Usage
   - Memory Usage
   - Network I/O
4. Customized visualization (colors, labels, thresholds).
5. Saved the dashboard.

---

## 🖼️ Screenshots

> 📷 **Note**: Replace the placeholders below with actual screenshots before submitting.

- 📸 Grafana Installation: `./screenshots/grafana-installation.png`
- 📸 Azure Monitor Connection: `./screenshots/azure-monitor-setup.png`
- 📸 Final Dashboard: `./screenshots/grafana-dashboard.png`

---

## 📝 Issues Encountered

- Initially faced a permission error assigning roles to the VM's Managed Identity. Resolved it by using a user with appropriate access rights.
- Required reboot after enabling Managed Identity for Azure permissions to take effect properly.
- Needed to restart Grafana service after updating `grafana.ini`—forgot initially, resulting in failed data source connection.

---

## ✅ Final Output

- Successfully installed and configured Grafana.
- Connected Grafana to Azure Monitor using Managed Identity.
- Created a dashboard displaying real-time system performance metrics from Ubuntu server.

---

## 📂 Submission

This markdown file, along with screenshots, is pushed to GitHub at:  
🔗 [GitHub Repository Link](https://github.com/your-username/lab3-grafana)
