
<h1>Active Directory Attack Lab</h1>

<h2>Description</h2>
The Active Directory Home Lab project is designed to provide IT and cybersecurity professionals with a comprehensive environment for hands-on experience in Active Directory management, network penetration testing, and vulnerability assessments. The lab features a Windows Server with Active Directory for domain management, a Splunk instance for analyzing security events, Kali Linux for attack simulation, and a target machine to act as the victim for penetration testing exercises. Additionally, Atomic Red Team is employed for adversary emulation. This setup enhances skills in configuring and securing Active Directory environments, provides insights into attack methodologies, and highlights IT administration best practices. The project emphasizes a hands-on approach using Oracle VM VirtualBox for a virtualized, isolated environment, laying the foundation for future exploration in cybersecurity.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Atomic Red Team</b>
- <b>Sysmon</b>
- <b>Crowbar</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Windows Server 2022</b>
- <b>Active Directory</b>
- <b>OracleVM VirtualBox</b>
- <b>Kali Linux</b>
- <b>Ubuntu Server</b>
- <b>Splunk</b>

<h2>Project Walk-through:</h2>

<p align="center">
Step 1: Build a visual representation to map out the lab and how the different components will interact with one another: <br/>
<img src="https://i.imgur.com/LroOl3I.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 2: Provision four virtual machines. The first with Windows 10 which will act as the target machine, the second with Kali Linux which is where we will execute various attacks, the third with Windows Server 2022 which will act as our Domain Controller, and the fourth with Ubuntu Server which will act as our Splunk Server:  <br/>
<img src="https://i.imgur.com/L2jNGbk.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/NjUzCsM.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/pKQdU3V.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/LYsZYOW.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/sF5dHK4.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 3: Run any necessary updates within the Splunk Server: <br/>
<img src="https://i.imgur.com/MhL26HA.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 4: A dedicated NAT network called "AD-Project" with the IP range 192.168.10.0/24 was configured within Oracle VM VirtualBox to isolate the virtual lab from the physical network, ensuring a safe and controlled environment. This setup allows all VMs (the target machine, Kali Linux server, domain controller, and Splunk server) to interconnect and access the internet for necessary tasks, while maintaining consistent and predictable IP addressing for simplified configuration and troubleshooting:  <br/>
<img src="https://i.imgur.com/ObsmcpI.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 5: Set a static IP address for the Splunk server to ensure consistent access and configuration, as other devices in the network rely on its IP address to send data. It also provides stability for configurations like data inputs and forwarder settings, which depend on the Splunk server's IP address. By using the command sudo nano /etc/netplan/00-installer-config.yaml, the network configuration can be defined to maintain a static IP:  <br/>
<img src="https://i.imgur.com/NcGeask.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 6: Download Splunk Enterprise:  <br/>
<img src="https://i.imgur.com/KnTZm4h.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 7: The command sudo adduser mydomain vboxsf adds the user mydomain to the vboxsf group. This is crucial for shared folder access and simplified filer transfer:  <br/>
<img src="https://i.imgur.com/mTq7CQ1.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 8: Create a new directory called “share” for organized file sharing:  <br/>
<img src="https://i.imgur.com/0Wjevnq.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 9: The command sudo mount -t vboxsf -o uid=1000, gid=1000 Active-Directory-Project share/ is used to mount the VirtualBox shared folder "Active-Directory-Project" into the "share" directory in the virtual machine (VM). This command ensures that the mounted shared folder is accessible with the correct permissions, allowing the VM user to read, write, and execute files. By establishing this shared folder, seamless file sharing and data exchange between the host system and the VM are enabled, which is essential for the project's operations:  <br/>
<img src="https://i.imgur.com/M3wvnkf.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 10: Install Splunk Enterprise on the virtual machine:  <br/>
<img src="https://i.imgur.com/Sn8y8jQ.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 11: Set the IP address, subnet mask, default gateway, and preferred DNS server of the target machine:  <br/>
<img src="https://i.imgur.com/Yf3pQZS.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 12: Test connectivity to Splunk dashboard:  <br/>
<img src="https://i.imgur.com/o5OqxUV.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 13: Download Splunk Universal Forwarder to efficiently collect and forward logs and metrics from various sources to a central Splunk server for analysis. It reduces the processing load on target machines by performing initial data filtering and aggregation, and ensures secure data transmission:  <br/>
<img src="https://i.imgur.com/UADiuqI.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 14: Download and install Sysmon which provides detailed and advanced monitoring of Windows system activities. It captures valuable information about process creations, network connections, and file changes, which are crucial for detecting and investigating security incidents. By integrating Sysmon data with Splunk, the project gains enhanced visibility into system behavior, enabling more effective security monitoring and analysis:  <br/>
<img src="https://i.imgur.com/euPNcHz.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 15: Editing the inputs.conf file to configure the Splunk Universal Forwarder ensures the collection and forwarding of crucial Windows Event Logs to the Splunk server. This setup captures vital logs like Application, Security, System, and Sysmon Operational logs, organizing them under the "endpoint" index for systematic analysis. Additionally, the use of XML format for Sysmon data preserves the event structure, enhancing data parsing and analysis capabilities. This configuration is essential for establishing an effective logging system for security monitoring and incident investigation in a Splunk environment:  <br/>
<img src="https://i.imgur.com/5nM6X0s.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 16: Click to enable the “Local System Account”. This is crucial for granting the forwarder the necessary permissions to access and collect system-level data and logs. This account has extensive privileges on the local machine, allowing the forwarder to monitor and gather information from various sources that may require elevated permissions. It ensures comprehensive data collection for effective monitoring and analysis within the Splunk environment.:  <br/>
<img src="https://i.imgur.com/vOy4OrJ.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 17: Within the Splunk dashboard, add a new index called “endpoint.” This dedicated index serves as a central repository for storing and categorizing endpoint-related logs and events, such as system, application, and security logs:  <br/>
<img src="https://i.imgur.com/gKLVRjE.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 18: Under Forwarding & Receiving within the Splunk dashboard, set the port 9997 to be a receiving port under “Receive data.” This allows the Splunk server to accept incoming data from the Splunk Universal Forwarders installed on other machines:  <br/>
<img src="https://i.imgur.com/NeQKWNT.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 19: To ensure that data is being pulled into the splunk dashboard, enter “index=endpoint” into the search bar to query for results:  <br/>
<img src="https://i.imgur.com/On0ys9y.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 20: Install Sysmon and Splunk Universal Forwarder on the Windows server:  <br/>
<img src="https://i.imgur.com/G25PZWN.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 21: Now on the Windows Server, configure the following IP address and DNS server:  <br/>
<img src="https://i.imgur.com/o7WLuLQ.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 22: Test connectivity to the Splunk Server:  <br/>
<img src="https://i.imgur.com/9Oom4QZ.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 23: Within the Server Manager, click on Manage, then Add Roles and Features to begin configuring this server:  <br/>
<img src="https://i.imgur.com/dLtbFw4.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/P8TyTfZ.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/aOEawzm.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 24: Now promote the Windows Server to a domain controller. This allows the server to manage user accounts, computers, security policies, and access permissions within the domain:  <br/>
<img src="https://i.imgur.com/WkWAEqw.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/l9vsqbl.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 25: Create organizational units and users within the domain:  <br/>
<img src="https://i.imgur.com/uGXZStb.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/NOKEnAE.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 26: Now that the Windows Server is configured as a domain controller and the users have been created, we will navigate to the target machine and join it to the server:  <br/>
<img src="https://i.imgur.com/gIsYpsU.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 27: Verify that the prior step worked and the target machine is joined to the server:  <br/>
<img src="https://i.imgur.com/cuioQ97.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 28: Add the target machine to the domain. This step allows the target machine to authenticate users and enforce policies defined in the Active Directory:  <br/>
<img src="https://i.imgur.com/PsWkZ2M.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/QgK1lFW.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 29: Now we will begin configuring the Kali Linux virtual machine first by setting an IP address, subnet mask, default gateway, and DNS server:  <br/>
<img src="https://i.imgur.com/em3sEDJ.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<img src="https://i.imgur.com/0kSKBQw.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 30: Test connectivity to the Splunk Server:  <br/>
<img src="https://i.imgur.com/2xLZfsv.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 31: Run any necessary updates within the Kali Linux virtual machine:  <br/>
<img src="https://i.imgur.com/IfU34Xn.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 32. Create a directory called ad-project to keep all files and tools organized:  <br/>
<img src="https://i.imgur.com/1wASbKX.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 33. Now install Crowbar. Crowbar is a brute-forcing tool used in penetration testing to attack various protocols. It is used to perform brute force attacks on protocols such as OpenVPN, Remote Desktop Protocol (RDP) with NLA support, SSH private key authentication, and VNC key authentication:  <br/>
<img src="https://i.imgur.com/sU6omwF.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 34: We now run the following commands. The command cd /usr/share/wordlists is used to change the directory to the location where Kali Linux stores its wordlists, including the Rockyou wordlist. This is a common directory for storing various wordlists used for password cracking and other security testing purposes​. The command sudo gunzip rockyou.txt.gz is used to decompress the Rockyou wordlist file, which is initially stored in a compressed format (gzip) to save space. By decompressing it, you make the wordlist usable for tools that require a plaintext wordlist, such as password cracking tools:  <br/>
<img src="https://i.imgur.com/3H489mb.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 35: Since the rockyou.txt wordlist is very long, we will create a smaller wordlist by adding the first twenty entries of it to a new file called passwords.txt:  <br/>
<img src="https://i.imgur.com/drIJIXk.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 36: Now change the directory and edit the passwords.txt file to add the passwords of the created users from the Windows Server to the text file in preparation for the brute force attack:  <br/>
<img src="https://i.imgur.com/KL0fBm2.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 37: Within the target machine, enable remote desktop connections to allow the execution of brute force attacks against the RDP (Remote Desktop Protocol) service:  <br/>
<img src="https://i.imgur.com/509jW9Q.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 38: Use the Crowbar tool to execute a brute force attack against one of the users on the RDP service:  <br/>
<img src="https://i.imgur.com/fjpx7yA.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 39: Observe evidence of the attack within the Splunk Dashboard:  <br/>
<img src="https://i.imgur.com/J0MxMmf.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 40: Before installing Atomic Red Team on the target machine, the command Set-ExecutionPolicy Bypass CurrentUser is run in PowerShell to temporarily bypass the default execution policy. This is necessary because the default execution policy on Windows clients is Restricted, which prevents the execution of all script files, including PowerShell scripts. By setting the execution policy to Bypass for the CurrentUser scope, it allows the PowerShell script for installing Atomic Red Team to run without being blocked by the execution policy:  <br/>
<img src="https://i.imgur.com/eRSktxa.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 41: Add an exclusion prior to downloading Atomic Red Team.By adding an exclusion, you ensure that Atomic Red Team can run its simulations without being hindered by the security software:  <br/>
<img src="https://i.imgur.com/fOzIIoI.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 42: Install Atomic Red Team:  <br/>
<img src="https://i.imgur.com/3NYopRD.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 43: Choose a technique from the MITRE ATT&CK Website and use Atomic Red Team to execute it. These techniques that are represented by identifiers on the website are used to categorize and reference different adversarial techniques that are observed in real-world cyber attacks:  <br/>
<img src="https://i.imgur.com/Wa8YMme.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 44: Use Atomic Red Team to execute technique T1059.001, which is a Command and Scripting Interpreter tactic that involves using PowerShell to execute actions on a target system, such as running executables, downloading files, and performing system actions:  <br/>
<img src="https://i.imgur.com/O1SZvH0.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
<br />
<br />
Step 45: Use Atomic Red Team to execute technique T059.001, which is an Execution tactic that involves creating a local user account on the targeted machine. By analyzing the output, we can build alerts to detect this activity in the future:  <br/>
<img src="https://i.imgur.com/mlWCZu8.png" height="80%" width="80%" alt="Active Directory Attack Lab"/>
</p>



