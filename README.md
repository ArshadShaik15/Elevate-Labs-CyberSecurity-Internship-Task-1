# Elevate-Labs-CyberSecurity-Internship-Task-1<br>

<br>Task 1: Local Network Port Scan<br><br>
<br>

### **🎯 Objective:**  <br>

<p align="left"> The primary goal of this task is to learn and practice fundamental network reconnaissance skills by discovering open ports on devices within a local network to understand the network's exposure and potential security risks. <br> </p>
<br> 
<br>

### **🛠️ Lab Setup:** <br> <br>

### **Installing Nmap:**  <br>
<p align="left"> &nbsp; •	I have installed the latest version of Nmap for windows from the official website. <br> </p>
<p align="left"> &nbsp; •	Official Website: Navigate to the Nmap download page https://nmap.org/download <br> </p>
<p align="left"> &nbsp; •	Choose the installer for your operating system (Windows, Linux, macOS). For Windows, the installer is usually called nmap-setup.exe </p> 

### **Installing Wireshark:** <br>
<p align="left"> &nbsp; •	I have installed the latest version of Wireshark for windows from the official website. <br> </p>
<p align="left"> &nbsp; •	Official Website: Navigate to the Wireshark download page https://www.wireshark.org/download.html <br> </p>
<p align="left"> &nbsp; •	Choose the installer for your operating system (Windows, Linux, macOS). For Windows, the installer is usually called Wireshark-4.6.0-x64.exe </p>


<br>

### **Step-1: Finding the local IP range:**

1)	I have found my local IP network by running the command ipconfig in Command Prompt. You can follow the steps mentioned below (I will be hiding the IP Address and MAC Address).

    a.	Command for macOS/Linux: ip a (or) ifconfig

    b.	Press Windows Key + R, type cmd, and press Enter to open the command prompt.
  
    c.	Identify the range by looking for the section related to your Wi-Fi or Ethernet connection.
  
    d.	Find the IPv4 Address (e.g., 192.168.1.10)
  
    e.	Find the Subnet Mask (e.g., 255.255.255.0)
  	
<br>
<img width="617" height="459" alt="Screenshot 2025-10-20 181437" src="https://github.com/user-attachments/assets/64bf4db0-7e74-4b26-9b17-d2e47192a9ef" />  <br>


<br>


### **Step-2: Running the TCP SYN Scan:**

I executed the scan in two different ways to check if the result varies or not:

1)	Running the command with administrator/root privileges for the TCP SYN scan (-sS) to work correctly. 

      •	In Windows: Right-click on Command Prompt and select "Run as Administrator."<br>
     <p align="left"> •	The Command Prompt uses CLI (Command Line Interface) which allows you to use flags (like -sS and -oA in your command), which unlock Nmap’s most advanced and specific features. </p>
     <br>
2)	Run the command in Nmap directly.

      <p align="left"> •	It is a GUI (Graphical User Interface). Generally, This is what you're used to (like clicking a web browser or the Nmap installer). It's easy because it is designed in an interactive manner (clicking buttons, Options/Filters, etc) but it limits you to the options the developers put into buttons and menus. </p>
      <br>
3)  After running the scan, Both Command Prompt and Nmap provided me with the same results. 


    <br>  <img width="748" height="814" alt="Screenshot 2025-10-20 232300" src="https://github.com/user-attachments/assets/521a2fd6-7e44-431f-9a25-05a8cc7d276a" />  <br>
 

    <br>  <img width="710" height="858" alt="Screenshot 2025-10-20 232702" src="https://github.com/user-attachments/assets/73f20b98-2292-4e46-b9e3-49a98bf14144" />  <br>

<br>

4) I have also captured the packet for further analysis using Wireshark <br>

    <br>  <img width="1508" height="921" alt="Screenshot 2025-10-20 233525" src="https://github.com/user-attachments/assets/4fbcd13a-a307-4641-a20f-fb5decedbea3" />  <br>

 
<br>  
<br>

### **Step-3: Noting down the IP Addresses, Open Ports, and Services found:**

      
### **Nmap Scan Results: Active Hosts and Open Ports**

| IP Address | Host Description (Service Profile) | Open Ports (TCP) | Key Services Identified |
| :--- | :--- | :--- | :--- |
| **192.168.29.X** | Network Gateway / Router 📡 | 80, 443, 1900, 7443, 8080, 8443 | HTTP, HTTPS, UPnP, HTTPS-alt |
| **192.168.29.XX** | Windows Device (PC/Server) 🖥️ | 135, 139, 445, 1069, 4343, 4449, 7070 | MSRPC, NetBIOS/SMB (File Sharing), Realserver |
| **192.168.29.YY** | Streaming/Video Device | 80, 554 | HTTP, **RTSP** (Real-Time Streaming Protocol) |
| **192.168.29.ZZ** | Active Host (Secure/Firewalled) | None | All 1000 scanned ports were reported as closed. |
<br>

<br>

### **Step-4: Identify Potential Security Risks from Open Ports:**  <br>

The most critical part of this task is researching of commonly running services on these ports. An open port is only a risk if the service running on it is vulnerable or misconfigured.

The highest risk ports you found are:
<br>
1) Ports 139/tcp and 445/tcp (SMB/CIFS): These are used for Windows file and printer sharing.

   <p align="left">  • Risk: If the operating system (OS) or the sharing service is not patched, an attacker can exploit vulnerabilities like the infamous <strong>EternalBlue</strong> to gain control or plant malware (e.g., ransomware). It also exposes system information like user lists and shared folders to anyone on the network.  </p> 
   <br>
2) Port 1900/tcp (UPnP): This protocol allows devices to open ports on your router automatically without your permission.

   <p align="left">  • Risk: Malware can use UPnP to open a port for itself, bypassing your firewall and making your device reachable from the public internet.  </p>
   <br>
3) Ports 80/tcp, 443/tcp, 8080/tcp, 8443/tcp (Web Services):

   <p align="left">  • Risk: If the router's management interface or a local application running on these ports is running old software, it can be vulnerable to exploits like Cross-Site Scripting (XSS) or Authentication Bypass. Since the router is on **192.168.29.1**, it's the primary risk point.  </p>
   <br>  
4) Port 554/tcp (RTSP): If this is a camera, it likely requires strong authentication.

     • Risk: Weak or default passwords on an exposed camera/video system could allow an attacker to view your video feed.
<br>

   
### <br> **Conclusion:**  <br>

1)    The Nmap TCP SYN scan of the local network **(192.168.29.0/24)** successfully identified four active hosts. The analysis focused on the three devices that presented open ports to the network.<br>

2)    The scan revealed critical security gaps, most notably on host **192.168.29.XX** and the network router **(192.168.29.X)**. <br> The primary risk vectors identified were: <br> 
     <p align="left">   •    **File Sharing (Ports 139/445)**: These exposed services are vulnerable to well-known exploits **(e.g., EternalBlue)** if the operating system is not fully patched. <br> </p>
     <p align="left">   •    **UPnP (Port 1900):** This service grants devices the ability to automatically bypass the router's firewall, creating an unauthorized vulnerability for malware. <br> </p>

3)    To mitigate these immediate security risks, the following actions are strongly recommended: <br>
     <p align="left">   •     Disable UPnP on the router **(192.168.29.X)** to prevent unauthorized firewall bypasses. <br> </p>
     <p align="left">   •     Block TCP Ports 139 and 445 on all non-essential devices using the Windows Firewall or, preferably, disable the File and Printer Sharing service completely. <br> </p>
     <p align="left">   •     Enforce a strong, non-default password on the router's administration interface. <br> </p>
