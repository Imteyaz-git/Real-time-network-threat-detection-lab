# Real-Time Network Threat Detection Lab

**Project Overview:**  
This project demonstrates a complete lab environment for real-time network threat detection. The lab integrates Suricata as an IDS/IPS with the Elastic SIEM (Elasticsearch, Logstash, Kibana) for log collection, visualization, and analysis. The ultimate goal is to build a robust, automated system to detect and respond to network threats in real time.

## Current State

### Lab Environment Setup
- **Virtual Machines Created Using Vagrant & VirtualBox:**
  - **Attacker Machine:**  
    - **OS:** Kali Linux  
    - **Purpose:** Simulate network attacks (e.g., port scans, SQL injection, brute-force)
  - **Target Machine:**  
    - **OS:** Metasploitable2  
    - **Purpose:** Provide a vulnerable environment for testing attacks.
  - **Firewall/IPS Machine:**  
    - **OS:** Ubuntu  
    - **Installed Tool:** Suricata IDS/IPS  
    - **Purpose:** Monitor and log network traffic, generating alerts based on custom rules.

### Suricata Configuration
- **Customized `suricata.yaml`:**  
  - Defined network variables (e.g., **HOME_NET:** `[192.168.56.0/24]`).
- **Custom Alert Rule Added:**  
  - **Rule:** `"ICMP Ping Detected"` (in `/etc/suricata/rules/local.rules`)  
  - **SID:** `1000003`  
- **Verification:**  
  - Suricata logs (`eve.json`) are actively updated, and test alerts are generated when traffic (such as pings) is simulated.

### Elastic SIEM Integration (Using Docker)
- **Elastic Stack Setup:**  
  - **Elasticsearch, Logstash, and Kibana** installed on the host using Docker Compose.
  - **Docker Compose File:** Configured to launch the Elastic Stack containers.
- **Logstash Pipeline:**  
  - Custom pipeline (`suricata.conf`) set up to process Suricata logs from Filebeat.
- **Filebeat Configuration on Firewall VM:**  
  - Installed Filebeat to monitor `/var/log/suricata/eve.json`.
  - Configured to forward logs to Logstash at the host's IP.
- **Kibana Index Pattern:**  
  - Created index pattern `suricata-*` to visualize the incoming logs.

## Screenshots
*(Include screenshots of the following to enhance your GitHub repository presentation)*
- Vagrant status showing all VMs running.
- Terminal outputs from Suricata logs (e.g., alerts and stats).
- Docker Compose file snippet for the Elastic Stack.
- Kibana Discover view or Dashboard showing indexed Suricata logs.

## Next Steps
- **Enhance Detection:**  
  - Develop additional custom rules to detect more attack vectors (e.g., port scanning, SQL injection).
- **Simulate Advanced Attacks:**  
  - Use tools like **Nmap**, **Hydra**, and **sqlmap** to generate diverse traffic and validate alerts.
- **Refine Visualizations & Alerts:**  
  - Build more detailed Kibana dashboards.
  - Configure Kibana alerts for automated notifications on critical events.

## How to Reproduce
1. **Clone this Repository:**
   ```bash
   git clone <repository-url>
   cd <repository-directory>
