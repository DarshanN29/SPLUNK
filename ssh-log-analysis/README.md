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

## 📸 Dashboard Visualizations

### 🔹 SSH Authentication Overview Dashboard
![Dashboard](screenshots/dashboard1.png)

This dashboard presents an overview of SSH authentication activity, including counts of successful and failed login attempts. It helps in monitoring access behavior and identifying unusual authentication patterns.

---

### 🔹 Failed Login & Brute Force Detection Dashboard
![Dashboard](screenshots/dashboard2.png)

This dashboard focuses on failed login attempts and highlights IP addresses generating repeated authentication failures. It is used to detect potential brute-force attacks and suspicious login activity.

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
