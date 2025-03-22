

# Kioptrix Level 1 - CTF Write-up 🚀  

## 📌 Introduction  
**Kioptrix Level 1** is an entry-level **Capture The Flag (CTF)** challenge designed for beginners in penetration testing.  
The objective is to **gain root access** by identifying and exploiting system vulnerabilities using various tools and techniques.  
This challenge provides a **hands-on learning experience** in a controlled environment, focusing on **ethical hacking and security assessment skills**.  

---  

## 🔍 Reconnaissance  

### **🛠 Tools Used:**  
- `netdiscover` – Identify the target IP.  
- `nmap` – Scan for open ports and services.  
- `nikto` – Web vulnerability scanning.  
- `ffuf` – Directory brute-forcing.  

### **🔎 Findings:**  
- **Target IP Address:** `192.168.X.X`  
- **Open Ports:**  
  - `22` (SSH)  
  - `80` (HTTP - Apache 2.3.20)  
  - `443` (HTTPS)  
- Apache 2.3.20 running on **Red Hat with mod_ssl 2.8.4**  

---  

## 💥 Exploitation  

- The **ExploitDB** script was outdated and did not work.  
- Used an **updated exploit from GitHub:**  
  🔗 [OpenLuck - GitHub](https://github.com/heltonWernik/OpenLuck)  

### **🔧 Steps Taken:**  
1️⃣ Install required dependencies:  
   ```bash
   sudo apt-get install libssl-dev
   ```  
2️⃣ Compile the exploit:  
   ```bash
   gcc -o exploit exploit.c -lssl -lcrypto
   ```  
3️⃣ Execute the exploit:  
   ```bash
   ./openFuck
   ```  
4️⃣ **Gained Root Access! 🎉**  

---  

## 🔝 Privilege Escalation  

Since the exploit **granted immediate root access**, no further privilege escalation was required.  

---  

## 🎯 Conclusion  

The **Kioptrix Level 1** challenge provided valuable insights into **real-world vulnerabilities** and security misconfigurations. Key takeaways include:  
✅ The importance of **enumeration** before exploitation.  
✅ How outdated software (Apache 2.3.20) can be a major security risk.  
✅ The need for **up-to-date exploits** for successful penetration testing.  

---  

## 📂 Additional Resources  

🔗 [Kioptrix VM Series](https://www.vulnhub.com/series/kioptrix,7/)  
🔗 [ExploitDB](https://www.exploit-db.com/)  

🚀 **Follow me for more write-ups and CTF challenges!**  

