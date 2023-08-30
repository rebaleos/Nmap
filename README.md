# Nmap
Network Enumeration and Scanning with Nmap (HTB Academy):

#Challange 1:

#Firewall and IDS/IPS Evasion - Easy Lab
Challenge Overview
In this challenge, you will be testing the IT security defenses, including the IDS and IPS systems, of a company that has hired you. The client's goal is to enhance their IT security, and they will make improvements to their IDS/IPS systems based on the results of these tests. Your task is to gather specific information from the given situations.


**Firewall and IDS/IPS Evasion — Easy Lab**

In this GitHub challenge project, we aim to demonstrate the use of Nmap, a powerful network scanning tool, to identify the operating system running on a provided machine. The task involves evading firewalls and intrusion detection/prevention systems (IDS/IPS) to accurately determine the target system's operating system.

**Objective:**
Our client has presented us with the task of identifying the operating system of a specific machine. This challenge requires us to bypass any firewalls and IDS/IPS that might be in place to safeguard the target machine.

**Nmap Command:**
To achieve this, we employ the Nmap tool with a specific script for SMB OS discovery. The command used for scanning is as follows:

root@kali:~# nmap --script smb-os-discovery 10.129.16.187


**Scan Results:**
Upon running the Nmap scan, we receive the following results:

```
Starting Nmap 7.94 ( <https://nmap.org> ) at 2023-07-19 12:14 AKDT
Nmap scan report for 10.129.16.187
Host is up (0.39s latency).
Not shown: 993 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
110/tcp   open  pop3
139/tcp   open  netbios-ssn
143/tcp   open  imap
445/tcp   open  microsoft-ds
10001/tcp open  scp-config
Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: nix-nmap-easy
|   NetBIOS computer name: NIX-NMAP-EASY\\x00
|   Domain name: \\x00
|   FQDN: nix-nmap-easy
|_  System time: 2023-06-25T13:16:13+02:00
Nmap done: 1 IP address (1 host up) scanned in 3.26 seconds
```

The Nmap scan successfully identifies the target machine's operating system as "Windows 6.1 (Samba 4.3.11-Ubuntu)".

**Script Parameter:**
Nmap offers a versatile feature called script parameters. In this context, we demonstrate the utilization of a specific script, namely `smb-os-discovery`. This script is employed to perform OS (Operating System) identification on SMB (Server Message Block) services. SMB is a protocol used for various network communication purposes, such as file and printer sharing.


------------------------

#Firewall and IDS/IPS Evasion - Medium Lab

Within this segment of our GitHub challenge project, we delve into a medium-level lab designed to extend our skills from the introductory exercise. Following our initial assessment, we have become aware of the administrators' proactive measures to enhance network security. With adjustments made to the IDS/IPS and firewall configurations, the administrators aim to implement more stringent traffic filtering, presenting us with an advanced security environment to navigate.

Lab Context:
Our understanding of the administrators' dissatisfaction with their previous configurations reveals their pursuit of an even more robust defense strategy. Our challenge involves determining whether we can effectively extract the version information of the target's DNS server despite these elevated security measures.

Lab Instructions:
To tackle this, we once again employ the versatile Nmap tool, this time with a more tailored approach. The command used to uncover the DNS server version is as follows:

root@kali:~# nmap -sSU -p 53 --script dns-nsid 10.129.16.187


Scan Findings:
Executing the Nmap scan yields the following outcomes:

```
Starting Nmap 7.94 ( <https://nmap.org> ) at 2023-07-19 11:04 AKDT
Nmap scan report for 10.129.16.187
Host is up (0.052s latency).
PORT   STATE    SERVICE
53/tcp filtered domain
53/udp open     domain
| dns-nsid: 
|_  bind.version: HTB{GoTtgUnyze9Psw4vGjcuMpHRp}
Nmap done: 1 IP address (1 host up) scanned in 1.19 seconds
```

The Nmap scan effectively uncovers the target's DNS server version, as evidenced by the identifier `bind.version: HTB{GoTtgUnyze9Psw4vGjcuMpHRp}`.

Explanation of Command:
- `-sSU`: These parameters form part of the Nmap command, shaping its behavior.
- `-s` designates the scan type, here, a SYN scan for TCP ports.
- `U` denotes a UDP scan, encompassing both TCP and UDP ports.
- `-p 53`: This option focuses the scan on a specific port, in this case, port 53, commonly used for DNS services.
- `--script dns-nsid`: With this flag, Nmap is directed to execute the `dns-nsid` script during the scan. This script is tailored to perform DNS Name Server Identifier (NSID) queries, uncovering essential attributes of the DNS server.

**Final Remarks:**
In this medium-level lab, we demonstrate our ability to navigate and extract critical information within a heightened security context. As we advance through escalating challenges, we further enhance our comprehension of strategies related to firewall and IDS/IPS evasion.

------------------


#Firewall and IDS/IPS Evasion - Hard Lab

In this advanced phase of our GitHub challenge project, we confront a formidable hard-level lab designed to stretch our capabilities within a high-security environment. Building on insights gained from our second test, our client's administrators have undergone a comprehensive week-long training to fortify their expertise in IDS/IPS systems. Now, equipped with newfound knowledge and precautionary measures, they invite us for a reevaluation due to significant changes in service configurations and software communication enhancements.

Lab Scenario:
Our mission is to tackle the intricate task of extracting version information from actively running services. The challenge arises from specific modifications made by our client, prompting us to discern the version of the target service. We're required to submit the corresponding flag as our solution.

**Lab Instructions:**
To navigate this intricate challenge, we employ the versatile networking tool Netcat (nc). The command to unravel the desired details is as follows:

root@kali:~# nc -nv -p 53 10.129.21.116 50000


Scan Findings:
Executing the Netcat command yields a revealing response:

```
(UNKNOWN) [10.129.2.47] 50000 (?) open
220 HTB{kjnsdf2n982n1827***************}
```

The response carries a message housing the sought-after version information, encapsulated within the flag: `HTB{kjnsdf2n982n1827***************}`.

Command Insight:
- `nc`: The core command, representing "netcat," serves as a versatile networking utility for data transfer and communication.
- `-nv`: These command-line options influence the `nc` command's behavior.
- `-n`: It prevents DNS name resolution, ensuring IP addresses remain unaltered.
- `-v`: Enabling verbose output furnishes comprehensive connection details.
- `-p 53`: This supplementary option designates the source port for the connection.
- `-p`: Indicates the source port specification.
- `53`: Set to port 53, recognized as the DNS service port.
- `10.129.21.116`: The target IP address for establishing the connection.
- `50000`: The chosen destination port for the connection.

**Final Reflections:**
In this formidable hard-level lab, we display our adeptness in navigating intricate security landscapes and discerning version details from active services. The experience solidifies our competence in the realm of firewall and IDS/IPS evasion.



------------


#Skills Gained:

1. **Nmap Proficiency**:
   * Acquired comprehensive knowledge of Nmap's functionalities, including host discovery, port scanning methodologies, and techniques for operating system detection.
   * Demonstrated proficiency in using Nmap to perform network enumeration tasks and gather crucial information about target systems.

2. **Network Enumeration Techniques**:
   * Developed a strong grasp of fundamental network enumeration techniques, such as identifying active hosts, discovering open ports, and enumerating services running on target systems.

3. **Nmap Scripting Engine (NSE)**:
   * Utilized Nmap's Scripting Engine to extend the tool's capabilities, enhancing the ability to gather specific information and identify vulnerabilities through scripted tests.

4. **Working with Scan Results**:
   * Successfully worked with saved Nmap scan results, showcasing skills in analyzing and interpreting gathered information to make informed decisions.

5. **Firewall and IDS/IPS Evasion**:
   * Engaged in practical labs focusing on evading network defenses, including firewalls and Intrusion Detection/Prevention Systems (IDS/IPS), demonstrating practical skills in testing network security.

6. **Problem Solving and Investigation**:
   * Accomplished a series of practical challenges involving OS detection, port enumeration, and version identification, showcasing problem-solving skills in network assessment.

7. **Ethical Hacking and Cybersecurity Practices**:
   * Applied ethical hacking practices by performing controlled tests on systems protected by IDS/IPS systems and firewalls, emphasizing adherence to ethical guidelines and responsible testing.
