# Elevate-Labs-CyberSecurity-Internship-Task-1<br>

<br>Task 1: Local Network Port Scan<br><br>


**Step-1: Installing Nmap:**

•	I have installed the latest version of Nmap for windows from the official website.
•	Official Website: Navigate to the Nmap download page
•	Download the Installer: Choose the installer for your operating system (Windows, Linux, macOS). For Windows, the installer is usually called nmap-setup.exe

<br>

**Step-2: Finding the local IP range:**

1)	I have found my local IP network by running the command ipconfig in Command Prompt. You can follow the steps mentioned below (I will be covering the information as it is sensitive).

    a.	Command for macOS/Linux: ip a (or) ifconfig

    b.	Press Windows Key + R, type cmd, and press Enter to open the command prompt.
  
    c.	Identify the range by looking for the section related to your Wi-Fi or Ethernet connection.
  
    d.	Find the IPv4 Address (e.g., 192.168.1.10)
  
    e.	Find the Subnet Mask (e.g., 255.255.255.0)
  	
<br>
<img width="617" height="459" alt="Screenshot 2025-10-20 181437" src="https://github.com/user-attachments/assets/64bf4db0-7e74-4b26-9b17-d2e47192a9ef" />
<br>

<br>

**Step-3: Running the TCP SYN Scan:**

I executed the scan in two different ways to check if the result varies or not:

1)	Running the command with administrator/root privileges for the TCP SYN scan (-sS) to work correctly. 

      •	In Windows: Right-click on Command Prompt and select "Run as Administrator."<br>
      •	The Command Prompt uses CLI (Command Line Interface) which allows you to use flags (like -sS and -oA in your command), which unlock Nmap’s most advanced and specific features.
  	<br>

2)	Run the command in Nmap directly.

      •	It is a GUI (Graphical User Interface). Generally, This is what you're used to (like clicking a web browser or the Nmap installer). It's easy because it is designed in an interactive manner (clicking buttons, Options/Filters, etc) but it limits you to the options the developers put into buttons and menus.

3)  After running the scan, Both Command Prompt and Nmap provided me with the same results.


    <img width="1093" height="1199" alt="Screenshot 2025-10-20 204214" src="https://github.com/user-attachments/assets/98aad51b-e2df-46ef-a1ac-12ce14308313" />

    <br> 
**Step-4: Noting down the IP addresses and open ports found:**

      
## Nmap Scan Results: Active Hosts and Open Ports

| IP Address | Host Description (Service Profile) | Open Ports (TCP) | Key Services Identified |
| :--- | :--- | :--- | :--- |
| **192.168.29.1** | Network Gateway / Router 📡 | 80, 443, 1900, 7443, 8080, 8443 | HTTP, HTTPS, UPnP, HTTPS-alt |
| **192.168.29.15** | Windows Device (PC/Server) 🖥️ | 135, 139, 445, 1069, 4343, 4449, 7070 | MSRPC, NetBIOS/SMB (File Sharing), Realserver |
| **192.168.29.50** | Streaming/Video Device | 80, 554 | HTTP, **RTSP** (Real-Time Streaming Protocol) |
| **192.168.29.25** | Active Host (Secure/Firewalled) | *None* | *All 1000 scanned ports were reported as closed.* |
