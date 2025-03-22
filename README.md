# Writeup for Kioptrix: Level 1 from Kioptrix VM Image Challenges

**Author:** Omkar Sahni  
**Difficulty:** Beginner  
**Objective:** Gain root access to the machine

---

## Introduction

The **Kioptrix: Level 1** VM is an entry-level **Capture The Flag (CTF)** challenge designed for beginners in penetration testing. The goal is to gain **root access** by exploiting system vulnerabilities using various tools and techniques. This challenge provides a hands-on learning experience in a controlled environment, focusing on ethical hacking skills.

---

## Getting Started

After extracting the Kioptrix VM files, update the `kioptrix_level_1.vmx` file to switch the network adapter from **Bridged** to **NAT** mode. This ensures that the VM can communicate with your host machine properly.

![Original vmx file](media/image2.png)

*Fig: Original vmx file*

![Modified vmx file](media/image4.png)

*Fig: Modified vmx file*

---

## Reconnaissance

### Tools Used:
- **netdiscover**: To identify the IP address of the target machine.
- **nmap**: For port scanning and service enumeration.
- **nikto**: A web vulnerability scanner to identify potential security issues.
- **ffuf**: A directory brute-forcing tool to search for hidden directories or files.

### Finding the IP Address

Using **netdiscover**, we identified the IP address of the Kioptrix VM.

![netdiscover](media/image5.png)

*Fig: netdiscover*

![netdiscover Result](media/image6.png)

*Fig: netdiscover Result*

### Scanning & Enumeration

We used **nmap** to scan the target machine and identify open ports and running services.

![nmap command](media/image7.png)

*Fig: nmap command*

![Services running](media/image8.png)

*Fig: Services running*

From the scan, we discovered that **port 80 (HTTP)** and **port 443 (HTTPS)** were open, running a default Apache web server.

![Apache Page](media/image9.png)

*Fig: Apache Page*

### Directory Brute-Forcing with FFUF

We used **ffuf** to search for hidden directories or files on the web server.

![Ffuf command](media/image10.png)

*Fig: Ffuf command*

Unfortunately, no interesting directories or files were found during the scan.

### Web Vulnerability Scanning with Nikto

Next, we ran **Nikto** to identify potential security issues on the web server.

![Nikto](media/image11.png)

*Fig: Nikto*

Nikto revealed that the server was running **Apache 2.3.20** on **Red Hat** with **mod_ssl 2.8.4**. This version of Apache is known to be vulnerable to certain exploits.

---

## Exploitation

### Identifying the Vulnerability

After some research, we found that the **Apache 2.3.20** version is vulnerable to a **buffer overflow** exploit. However, the exploit available on **ExploitDB** was outdated and did not work.

![Google search result](media/image12.png)

*Fig: Google search result*

### Using an Updated Exploit

We decided to use an updated exploit from **GitHub** called **OpenLuck**.

**Exploit Link:** [OpenLuck](https://github.com/heltonWernik/OpenLuck)

![Clone exploit to local](media/image13.png)

*Fig: Clone exploit to local*

### Installing Dependencies

To ensure the exploit works correctly, we installed the **libssl-dev** package, which provides the necessary OpenSSL development libraries.

```bash
sudo apt-get install libssl-dev
