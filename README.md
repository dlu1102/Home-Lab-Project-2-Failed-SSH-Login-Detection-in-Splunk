# Lab #2 – Failed SSH Login Detection in Splunk

## 📌 Objective
Simulate a brute-force login detection workflow in Splunk by ingesting SSH log data, writing SPL queries, and building dashboards.

## 🛠 Skills Practiced
- Splunk data ingestion (custom file indexing)
- SPL (Search Processing Language) for failed login detection
- Dashboard creation for SOC visibility
- Troubleshooting & problem-solving when working with log sources
- Mapping detections to MITRE ATT&CK T1110 (Brute Force)

## 🔍 Workflow
1. **Log Simulation**

   Created a log file with entries such as:

   Jan 14 10:15:32 kali sshd[12345]: Failed password for invalid user wronguser from 192.168.0.5 port 53422 ssh2

   Jan 14 10:15:35 kali sshd[12345]: Failed password for invalid user admin from 192.168.0.8 port 53425 ssh2

3. **Ingestion**
- Splunk → Settings → Add Data → Upload
- Index: `ssh_failures`
- Sourcetype: `linux_secure`

3. **Query**

   index=ssh_failures ("Failed password" OR "Invalid user")
   | stats count by src_ip, user, _time

##   Sample Output

   src_ip                    |user                    |count
   
   192.168.0.5               |wronguser               |12

   192.168.0.8               |admin                   |8

🚀 Lessons Learned

   - Even simulated logs can teach SOC detection skills
   - SPL queries can be written to be source-agnostic
   - Troubleshooting failed attempts builds real problem-solving ability
