# 🔐 SSH Log Analysis using Splunk

## 📌 Overview
This project focuses on analyzing SSH authentication logs using Splunk to detect suspicious activities such as failed login attempts, brute-force attacks, and abnormal login behavior. The analysis simulates real-world SOC (Security Operations Center) monitoring.

---

## 🎯 Objectives
- Analyze SSH authentication logs  
- Detect failed login attempts  
- Identify brute-force attacks  
- Track successful logins after failures  
- Visualize SSH activity trends  

---

## 🛠 Tools Used
- Splunk Cloud  
- SPL (Search Processing Language)  

---

## 📂 Dataset
- Type: SSH authentication logs  
- Format: `.json`  
- Contains fields such as:
  - source IP  
  - username  
  - authentication status  
  - timestamp  

---

## 🔎 SPL Queries

### 1. Failed Login Attempts
```spl
index=* auth_success=false
| stats count by src_ip user
| sort - count
```

---

### 2. Brute Force Detection
```spl
index=* auth_success=false
| stats count by src_ip
| where count > 10
```

---

### 3. Successful Logins
```spl
index=* auth_success=true
| stats count by user src_ip
```

---

### 4. Login Activity Over Time
```spl
index=* 
| timechart count by auth_success
```

---

## 🚨 Detection Logic

- Multiple failed login attempts from a single IP → possible brute-force attack  
- Successful login after many failures → potential compromise  
- High login frequency → suspicious behavior  

---

## 📊 Observations
- Certain IP addresses generated repeated failed login attempts  
- Some accounts were targeted more frequently  
- Patterns indicate automated brute-force attempts  

---

## 📊 Dashboard Visualization

### 🔐 SSH Logs Security Dashboard

#### 🖥️ Dashboard Overview
This dashboard provides a comprehensive visualization of SSH log activity, focusing on authentication behavior and potential security threats. It is designed to help identify suspicious patterns such as brute-force attacks and unauthorized access attempts.

---

### 📸 Dashboard 1 – Security Insights

![SSH Dashboard 1](./dashboard1.png)

#### 🔍 Key Metrics:
- **Total SSH Events (1200):** Total number of SSH log entries analyzed.
- **Successful Logins (306):** Count of successful authentication attempts.
- **Failed SSH Logins (305):** Indicates failed login attempts, often linked to brute-force attacks.
- **Connections Without Authentication (286):** Suspicious connection attempts without proper login.

#### 📊 Visual Analysis:
- **Failed Login Distribution:**  
  Displays usernames with the highest failed login attempts (e.g., root, admin), helping identify targeted accounts.

- **Brute Force IP Detection:**  
  A table listing IP addresses with repeated failed attempts along with their frequency and percentage contribution.

#### 🧠 Insights:
- High failed login attempts suggest possible brute-force attacks.
- Certain usernames are more frequently targeted.
- Repeated IP addresses indicate potential attackers.

---

### 📸 Dashboard 2 – Event Summary

![SSH Dashboard 2](./dashboard2.png)

#### 🔍 Key Metric:
- **Total SSH Events (1200):**  
  A high-level summary of all SSH activities captured in the dataset.

#### 🧠 Purpose:
- Provides a quick overview of total SSH activity.
- Useful for identifying abnormal spikes in log volume.


---

## 📁 Project Structure
```
splunk/
└── ssh-log-analysis/
    ├── README.md
    ├── logs/
    ├── screenshots/
    └── queries/
```

---

## 🧠 Learning Outcomes
- Hands-on experience with SSH log analysis  
- Practical understanding of SPL queries  
- Detection of brute-force attacks  
- Dashboard creation in Splunk  

---

## 📌 Conclusion
This project demonstrates how SSH logs can be analyzed using Splunk to detect suspicious login behavior and potential attacks. It highlights the role of SIEM tools in real-time monitoring and threat detection.
