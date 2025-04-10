Network Forensics Lab ["FirstHack AD1 Forensics Lab" on CyberDefenders](https://cyberdefenders.org/blueteam-ctf-challenges/insider/)


# Technical Incident Report: Privilege Escalation and Steganographic Payload Launch from Compromised Linux Host
- Analyst Name: Kyle I.
- Date of Analysis: 4/8/2025
- Incident Reference: Forensic Image – FirstHack.ad1

## Executive Summary
A logical image captured from a Linux host was analyzed for post-exploitation activity. The host, likely running Kali Linux, showed signs of suspicious activity involving privilege escalation, credential dumping, and the use of steganography to hide payloads. Detailed .bash_history, log files, and hidden artifacts embedded in image files confirmed malicious behavior, including an attack launched against another system. The attacker (user: KarenHacker) used a combination of tools (msfconsole, binwalk, touch, su) and maintained taunting notes in scripts and bash entries.

## Key Findings
| Field                          | Value                                     |
|-------------------------------|-------------------------------------------|
| Linux Distro                  | Kali Linux                                |
| Privilege Escalation Method   | su to root by user postgres               |
| Evidence of Credential Dumping| mimikatz_trunk.zip                        |
| Suspicious File Created       | /root/Desktop/SuperSecretFile.txt         |
| Evidence File (Attack Proof)  | irZLAohL.jpeg                              |
| Tool Used for Payload Extraction | binwalk                                |
| User Checklist - Goal #3      | Profit                                    |
| Number of Apache Runs         | 0                                         |
| Bash Working Directory        | /root/Documents/myfirsthack/              |
| Expert Taunted by Attacker    | Young                                     |

## Timeline of Events
| Timestamp     | Action                                                    |
|---------------|-----------------------------------------------------------|
| Mar 20 11:26  | su command executed by user postgres to gain root         |
| N/A           | PostgreSQL started via systemctl to support msfconsole    |
| N/A           | SuperSecretFile.txt created via output redirection        |
| N/A           | binwalk executed against didyouthinkwedmakeiteasy.jpg     |
| N/A           | Attack evidence embedded in irZLAohL.jpeg                 |
| N/A           | Final CWD set to /root/Documents/myfirsthack/             |

### Detailed Analysis
**1. Which Linux distribution is being used on this machine?**

The environment is consistent with Kali Linux, evidenced by the use of penetration testing tools like msfconsole, binwalk, and manual script-based attacks.

#### Answer: kali
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/Linux-Distro.png)

**2. What is the MD5 hash of the Apache access.log file?**

The access.log file under /var/log/apache2/ was found to be empty, with the corresponding MD5 hash:

#### Answer: d41d8cd98f00b204e9800998ecf8427e
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/MD5.png)

**3. What is the name of the downloaded file?**

The file mimikatz_trunk.zip was located in the Downloads folder, consistent with credential harvesting behavior.

 #### Answer: mimikatz_trunk.zip
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/mimikatz.png)

**4. A secret file was created. What is the absolute path to this file?**

From .bash_history, the attacker used: `touch snky snky > /root/Desktop/SuperSecretFile.txt`
#### Answer: /root/Desktop/SuperSecretFile.txt
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/Secret-File.png)

**5. What program used the file didyouthinkwedmakeiteasy.jpg during its execution?**

The image didyouthinkwedmakeiteasy.jpg was processed using binwalk, indicating payload extraction.

#### Answer: binwalk
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/Attacking-Machine.png)

**6. What is the third goal from the checklist Karen created?**

On Karen’s Desktop, a note or checklist revealed:

```
1. Gain access
2. Establish persistence
3. Profit
```

#### Answer: Profit

**7. How many times was Apache run?**

Apache logs showed zero recorded activity. The MD5 hash also confirmed the file was empty.

#### Answer: 0
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/MD5.png)

**8. This machine was used to launch an attack on another. Which file contains the evidence for this?**

The file irZLAohL.jpeg contained a screenshot of a terminal with elevated access — an image-based attack artifact.

#### Answer: irZLAohL.jpeg
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/Attacking-Machine.png)

**9. It is believed that Karen was taunting a fellow computer expert through a bash script within the Documents directory, who was it?**

A bash script in the Documents/myfirsthack/ folder contained messages mocking an individual named:  

#### Answer: Young

**10. A user executed the su command to gain root access multiple times at 11:26. Who was the user?**

Logs from /var/log/auth.log show: `su[4074]: + ??? root:postgres`

#### Answer: postgres
![](https://github.com/K-ING-TECH/Incident-Report_Mimikatz_InsiderThreat/blob/main/su_root-access.png)

**11. What is the current working directory?**

Final directory after a cd and pwd sequence in .bash_history:  

#### Answer: /root/Documents/myfirsthack/


## Indicators of Compromise (IOCs)
| Type               | Value                                |
|--------------------|--------------------------------------|
| User               | KarenHacker                          |
| Suspicious File    | SuperSecretFile.txt                  |
| Credential Tool    | mimikatz_trunk.zip                   |
| Payload File       | didyouthinkwedmakeiteasy.jpg         |
| Evidence of Attack | irZLAohL.jpeg                        |
| Bash Directory     | /root/Documents/myfirsthack/         |
| Taunt Target       | Young                                |

## MITRE ATT&CK Mapping
| Tactic              | Technique                             | ID         |
|---------------------|----------------------------------------|------------|
| Execution           | Command and Scripting Interpreter      | T1059      |
| Privilege Escalation| Abuse Elevation Control Mechanism      | T1548.003  |
| Defense Evasion     | Masquerading / Obfuscated Files        | T1036      |
| Persistence         | Boot or Logon Initialization Scripts   | T1037      |
| Collection          | Data from Local System                 | T1005      |
| Exfiltration        | Steganography                          | T1027.003  |
| Credential Access   | OS Credential Dumping                  | T1003      |
| Discovery           | System Owner/User Discovery            | T1033      |

## Conclusion and Recommendations
The image reveals that `KarenHacker` used a Kali-based host to perform actions including credential dumping, privilege escalation, and launching an attack from a concealed payload in a JPEG file. Her bash history reveals clear intent, including taunts and multiple trial commands. The system was used for offensive operations and contains valuable post-exploitation artifacts.

### Recommendations
- Forensically preserve the irZLAohL.jpeg file and associated image artifacts.

- Review access control for users with root or sudo privileges.

- Apply bash command logging and auditing through syslog and auditd.

- Perform a steganographic scan across all user directories for exfil risk.

- Monitor for use of tools like binwalk, mimikatz, and Metasploit.

- Disable unused accounts and rotate credentials.

- Educate users on script hygiene and unauthorized tool use.
