# 🚀 Brute Force Attack Detection using Splunk

## 📌 Overview
This project focuses on detecting brute force attacks using log analysis in Splunk.  
The BOTSv3 dataset is used to simulate real-world enterprise logs and identify suspicious authentication activity.

---

## 🎯 Objectives
- Detect failed login attempts  
- Identify attacking systems (IP/hosts)  
- Analyze targeted user accounts  
- Detect brute force patterns  
- Visualize attacks using dashboards  

---

## 🛠 Tools & Technologies
- Splunk Enterprise  
- SPL (Search Processing Language)  
- BOTSv3 Dataset  

---

## 📂 Dataset
- **Name:** BOTSv3 Dataset  
- **Description:**  
  Simulated enterprise environment logs including authentication, network, and system logs.  
- **Use Case:** Widely used for cybersecurity training and threat detection practice  

---

## ⚙️ Implementation Steps

### 1️⃣ Data Ingestion
- Uploaded dataset into Splunk  
- Verified using:
```
index=botsv3
```

---

### 2️⃣ Authentication Failure Analysis
```
index=* failed OR failure
| stats count by host source
| sort -count
```
👉 Identifies systems generating high failed login attempts  

---

### 3️⃣ Top Attacking Systems
```
index=* failed OR failure
| stats count by host
| sort -count
| head 10
```
👉 Highlights top attacking hosts  

---

### 4️⃣ Targeted Users
```
index=* failed OR failure
| stats count by username
| sort -count
| head 10
```
👉 Shows most targeted user accounts  

---

### 5️⃣ Brute Force Detection
```
index=* failed OR failure
| stats count by host source
| where count > 5
| sort -count
```
👉 Detects suspicious repeated login attempts  

---

### 6️⃣ Time-Based Attack Analysis
```
index=* failed OR failure
| stats count min(_time) as first max(_time) as last by host source
| where count > 10
| convert ctime(first) ctime(last)
```
👉 Analyzes attack duration  

---

## 📊 Dashboard
- Bar charts → Attack sources  
- Tables → Detailed logs  
- Line charts → Time-based patterns  

📸 Screenshots available in `/screenshots` folder  

---

## 📈 Results
- Successfully detected brute force patterns  
- Identified high-risk systems and users  
- Visualized attack trends using dashboards  

---

## 🧠 Challenges Faced
- Dataset ingestion issues  
- Learning SPL queries  

---

## 🔮 Future Improvements
- Implement real-time alerts in Splunk  
- Enhance dashboards with more insights  

---

## 💼 Use Case
Useful for **SOC Analysts** to detect unauthorized access attempts and prevent account compromise.

---

## 🔗 Project Report
📄 Detailed report available in:  
project_report.pdf

---

## 👩‍💻 Author
Trusha Pandya 

---

## ⭐ If you like this project
Give it a star on GitHub!