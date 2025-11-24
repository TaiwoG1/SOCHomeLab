<h1>Endpoint Attack Simulation & Telemetry Analysis Lab</h1>


<h2>Overview</h2>
This project involved the design, implementation, and execution of a controlled attack simulation within a virtualized home lab environment. The primary objective was to mimic a real-world cyberattack scenario to generate comprehensive endpoint security telemetry, followed by its ingestion and analysis in Splunk. This allowed for hands-on experience in understanding attack chains, observing the digital footprint of malicious activities, and identifying potential detection patterns for security operations.
<br />
<br />
<b>Key Components & Technologies:</b>

- <b2> Virtualization Platform: VirtualBox </b2>
- <b2> Attacker Machine: Kali Linux (IP: 192.168.20.11) </b2>
- <b2> Target Machine: Windows 10 Client (IP: 192.168.20.10) </b2>
- <b2> Malware Generation: MSFVenom </b2>
- <b2> Command & Control (C2): Metasploit Framework (Meterpreter reverse shell) </b2>
- <b2> Log Collection: Sysmon, Splunk Universal Forwarder </b2>
- <b2> Log Analysis & SIEM: Splunk Enterprise (with Splunk Add-on for Microsoft Sysmon, Splunk Add-on for Microsoft Windows) </b2>
- <b2> Network Configuration: Isolated Internal Network </b2>
<br />



<h2>Project Steps & Highlights:</h2>
<br />

- <b2> Environment Setup: Configured an isolated virtual network with Kali Linux and Windows 10 VMs. Deployed Splunk Enterprise, a Splunk Universal Forwarder on the Windows client, and Microsoft Sysmon with a robust configuration to ensure granular event logging. A dedicated index=endpoint was established in Splunk for centralized endpoint telemetry. </b2>

  <p align="center">
  <img width="393" height="344" alt="create new index endpoint" src="https://github.com/user-attachments/assets/f13b9ae7-06f9-4e4e-bffc-75971bf8721c" />
  <br/>
  Create new index "endpoint" <br/>
  <br/>
  <img width="960" height="443" align = "center" alt="Splunk indexes page" src="https://github.com/user-attachments/assets/6c664cee-edde-4781-9271-091910a82303" />  
  Splunk indexes page <br/>

  <br />
  </p>
  
- <b2> Attack Execution: </b2>
  - <b2> Reconnaissance: Performed basic port scanning from Kali to identify open services on the target. </b2>
  - <b2> Malware Creation: Used MSFVenom to craft a Windows/x64/meterpreter/reverse_tcp executable payload, configured to connect back to the Kali attacker. </b2>
  - <b2> C2 Handler: Set up a Metasploit multi/handler on Kali to await the reverse shell connection. </b2>
  - <b2> Malware Delivery: Hosted the generated malware on a Python 3 HTTP server (port 9999) on Kali, allowing the Windows client to download it. </b2>
  - <b2> Execution & Persistence: Executed the malware on the Windows client (with Defender temporarily disabled for lab purposes), establishing a Meterpreter session. </b2>
  - <b2> Post-Exploitation Simulation: Performed typical post-exploitation commands (e.g., ipconfig, net user, net localgroup) through the Meterpreter shell to generate               realistic log data. </b2>


  <p align="center">  
  <img width="444" height="168" alt="MSFVenom command, MSFConsole handler, Python HTTP server running" src="https://github.com/user-attachments/assets/e7ecfc54-7af0-4e2a-b0fc-6bc92a6b23b6" />
  <img width="451" height="392" alt="set payload and lhost" src="https://github.com/user-attachments/assets/2e85462c-1436-4f14-b713-98f53580251e" />
  <br> MSFVenom command, MSFConsole handler, Python HTTP server running listening for connection <br/>
  <br />
  </p>

  <p align = "center">
  <img width="333" height="69" alt="task manager shows malware running" src="https://github.com/user-attachments/assets/0985ab5f-a2e0-45d7-8197-9663f3e4927e" />
  <br>task manager showing downloaded and executed exe malware file <br/>
    
  <p align = "center">
  <img width="302" height="73" alt="establish shell from kali to windows machine" src="https://github.com/user-attachments/assets/50c8a2ab-e43b-477f-9e97-fa8b5f8b40b1" />
  <br> Establish metasploit shell connection<br/>
  
    <p align="center">  
  <img width="480" height="256" alt="established connection from windows to kali machine" src="https://github.com/user-attachments/assets/73122615-ebc6-428f-964b-ad80d53b6497" />
  <br> Windows showing established connection <br/>
  <br />
  </p>
  
- <b2> Telemetry Collection & Analysis: </b2>
  - <b2> Verified that Sysmon and Windows Event Logs, including details of process creation, network connections, and command execution, were being successfully ingested by           Splunk into the endpoint index. </b2>
  - <b2> Leveraged Splunk's search capabilities to correlate events by IP address, hostname, and the malware filename (TestMal.pdf.exe). </b2>
  - <b2> Observed the full kill chain within the log data, from initial execution to post-exploitation activities, providing tangible evidence of the attack's progression. </b2>
  
  <p align="center">
  <img width="960" height="442" alt="Splunk search results showing Sysmon logs of TestMal.pdf.exe" src="https://github.com/user-attachments/assets/1548a820-1bf1-4f72-8663-6d2fdc16e8e9" />
  <br> Splunk search results showing Sysmon logs of TestMal.pdf.exe<br/>
  <br />
  </p>
  <p align="center">
  Splunk search results showing network connections from the malware (ipconfig command)<br/>
  <img src="https:" height="80%" width="80%" alt="Splunk search results showing network connections from the malware (ipconfig command)"/>
  <br />
  </p>
<br />


<h2>Outcomes & Learning:</h2>
This project provided invaluable practical experience in:
<br />
<br />

- <b2> Offensive Security Basics: Understanding malware generation, delivery, and C2 establishment. </b2>
- <b2> Defensive Security Fundamentals: Configuring endpoint logging (Sysmon, Windows Event Logs) for comprehensive visibility. </b2>
- <b2> SIEM Operations: Ingesting and analyzing security telemetry within Splunk, demonstrating the power of a centralized logging solution. </b2>
- <b2> Threat Detection: Identifying specific log patterns and anomalies indicative of malicious activity, laying the foundation for developing robust detection rules and           alerts in a production environment. </b2>
- <b2> Problem-Solving: Troubleshooting network connectivity, log ingestion, and tool configurations in a controlled lab setting. </b2>
<br />

<b2>This exercise solidified my understanding of how a simulated attack translates into actionable security telemetry, highlighting the importance of rich log sources and effective SIEM correlation for detecting and responding to cyber threats.</b2>
