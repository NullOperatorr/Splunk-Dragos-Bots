# Splunk-Dragos-Bots
CyberLab-09

<p align="center">
<img width="450" height="489" alt="image" src="https://github.com/user-attachments/assets/b37aa0b1-a001-4ba7-889e-75cb1b0d34d6" />
</p>

Hello Guys ! today I’m going to walkthrough one of Splunk scenarios related to IT/OT security.

https://bots.splunk.com/

 ## Scenario:
1up your ICS/OT cybersecurity team

BOTS scenario 1 ‘1UP Your ICS/OT Cybersecurity Team’ is an Industrial Control System (ICS) Cybersecurity 101 with Dragos. This capture-the-flag (CTF) scenario will upskill your team on Operational Technology (OT), ICS and SCADA cybersecurity topics in a fun and engaging way.

Topics covered in the scenario include control logic modifications, maintaining persistence inside networks, implementing command & control (C2), and much more. As IT & OT cybersecurity team member working through this scenario, you will develop an understanding of some key challenges related to protecting industrial networks. If you have questions on this scenario or would like more information about Dragos training programs, you can email us at ctf@dragos.com. We’ll do our best to reply quickly.

Before we start, some questions do not require technical skills, they require search skills.

“The lab includes 35 questions, so let’s get started.”  

---

## Questions:

## #101    
Which host gets notified when the 1756-L61/B LOGIX5561 card undergoes a PLC status change?

**Answer:** 192.168.97.6  

<img width="640" height="218" alt="image" src="https://github.com/user-attachments/assets/0c19e4df-7238-45be-a924-a67665b202a5" />  

```bash
index="dragos"  1756-L61/B LOGIX5561
| table body
```
Explanation: We took the PLC card name and searched with it hoping to find what we want and to make things clearer we used the table command.  

## #102  
Based on the previous question, who is the manufacturer of the card?

**Answer:** Allen-Bradley

## #103  
Based on the answer in question 102, answering in MB, how large is the user memory on the previously identified controller?

**Answer:** 2

## #104  
What is the built-in COM (communication) port?

**Answer:** rs-232  

<img width="640" height="682" alt="image" src="https://github.com/user-attachments/assets/b40616fb-fcd7-457c-8b1c-80305ca54df8" />  

## #105  
What is the destination IP address of the TCP reverse shell that was detected?

**Answer:** 10.0.0.131  

<img width="640" height="165" alt="image" src="https://github.com/user-attachments/assets/2a48dab6-c44b-4a07-be4c-42431c751caf" />

```bash
index="dragos"  TCP reverse shell
```

## #106  
What was the hostname that was connected to with a SMB command shell?

**Answer:** rslogix5000  

<img width="640" height="315" alt="image" src="https://github.com/user-attachments/assets/9d29e087-c16b-4bdf-867c-d0a6280206a5" />  

```bash
index="dragos"  SMB command shell
| table dest_host
| dedup dest_host
```

Explanation: we searched with (SMB) to find any results, organize by (table) and then delete any duplicate by (dedup).

Be noted that we go with this answer (rslogix5000) because it seems suspicious related to any other name.  

## #107  
If you were going to use the tool ‘pylogix’, what config file parameter needs to change in order to set the slot number?

**Answer:** ProcessorSlot

## #108  
Using pylogix, what value is used to read a tag by routing through another device?

**Answer:** route

## #109
Using pylogix, what value is used to enumerate and get all controller and program tags?

**Answer:** GetTagList()  

<img width="640" height="411" alt="image" src="https://github.com/user-attachments/assets/b6fb7619-5d23-4158-8978-3f14ffadb705" />  
<img width="640" height="95" alt="image" src="https://github.com/user-attachments/assets/d3b73345-d04d-44eb-9010-d2c02cf3624d" />  

The Pylogix Documentation below for your reference,  
https://github.com/dmroeder/pylogix/blob/master/docs/Documentation.md?source=post_page-----b79fbabbbcc5---------------------------------------#gettaglist

## #110  
On which hostname was the Metasploit alert for detected windows/speak_pwned run against?

**Answer:** srv-hq-nas01  

<img width="640" height="339" alt="image" src="https://github.com/user-attachments/assets/8c84d70a-01ac-4c7f-8e3d-ed1476dae842" />  
<img width="640" height="504" alt="image" src="https://github.com/user-attachments/assets/bdc42c1e-e8ee-403e-a6a7-ada76bfca696" />  

```bash
index="dragos"  body="Metasploit Detected: windows/speak_pwned"
```

Explanation: first we searched with the word metasploit, then we checked the body till we found windows/speak_pwned as in the question then the only dest_host was certainly our answer.  

## #111  

What offensive PowerShell tool was used by the adversary?

**Answer:** empire  

<img width="640" height="210" alt="image" src="https://github.com/user-attachments/assets/02f6999c-e2d7-44a9-a2fc-d05f2c60bb0e" />


```bash
index="dragos"  Powershell
```


## #112  
MS17–101 was run against a target. What was the target’s MAC address?

**Answer:** F8:DB:88:3E:83:A0  

<img width="640" height="228" alt="image" src="https://github.com/user-attachments/assets/1bcfe3dc-eebd-456d-bb93-295361476e7d" />  


```bash
index="dragos"  MS17-101 OR WannaCry OR EternalBlue
```
Explanation: As is well known, the vulnerability MS17–010 is often associated with EternalBlue and WannaCry. We searched for these common names, noting that this vulnerability targets the legacy SMBv1 protocol.

## #113
Which host attempted to modify the Usermemory object on the host 192.168.1.6 more than once?

**Answer:** 192.168.1.100  

<img width="640" height="341" alt="image" src="https://github.com/user-attachments/assets/fbf9aa26-f59a-4b91-a5f5-fb49c05c23b0" />

```bash
index="dragos"  dest_ip="192.168.1.6"
```

Explanation: Since 192.168.1.6 was the modified field, this indicates it will be the destination. We searched as described above and examined the body for anything related to the question, where we found the answer easily.
 
## #114  

Host 192.168.1.200 received a CIP error indicating an unauthorized command from host 192.168.1.6. What type of request created the alert?

**Answer:** Get Attribute List

<img width="640" height="275" alt="image" src="https://github.com/user-attachments/assets/aaecc8db-7e4c-44dc-8b19-6f9f7c06ee39" />

```bash
index="dragos"  CIP error
|table body
| dedup body
|sort _time
 ```

## #115  
There was a port scan initiated at 03:06. Providing the port number only, what was the highest port number scanned?

**Answer:** 1331  


```bash
index="dragos" sourcetype=dragos_alert
|where strftime(_time, "%H:%M")="03:06"
| table _time dest_ip src_ip dest_port signature body src_host
```


Explanation: What we do here that we needed to limit all the event to 03:06 by (strftime) then we searched in this minute anything related to port scanning.

## #116  
Based on the previous question, what is the hostname of where the scanner originated?

**Answer:** factory-talk-vi  

<img width="640" height="168" alt="image" src="https://github.com/user-attachments/assets/0d407dff-5e63-4861-8829-baf2c554804c" />  

## #117
Host 192.168.193.12 sent a file from 192.168.2.2. What was the access technique used?

**Answer:** None Logon  

<img width="640" height="142" alt="image" src="https://github.com/user-attachments/assets/64bbf7c2-1b00-4404-af58-b110225739ce" />  

```bash
index="dragos" src_ip=192.168.193.12 dest_ip=192.168.2.2
|table body
```

## #118  
There was a Metasploit reverse TCP shell detected, started from 10.0.0.128. Provide the IPv4 address of where it was connecting to.  
**Answer:** 10.0.0.131  

<img width="640" height="142" alt="image" src="https://github.com/user-attachments/assets/036f07a0-9ccc-486d-981e-3913f95c38b3" />  

```bash
index="dragos" Metasploit reverse TCP shell
```

## #119  
What is the IPv4 address of the host that uses pycomm3 the most?

**Answer:** 192.168.212.226

<img width="640" height="205" alt="image" src="https://github.com/user-attachments/assets/e13c5df9-80df-42f4-9857-5e28d6fcd474" />  

```bash
index="dragos"   pycomm3
|eval src_ip= split (src_ip, ",")
| mvexpand src_ip
| stats count by src_ip 
| sort -count
```

Explanation: The eval command was used to split multiple source IPs into separate values when they were stored in one field. The mvexpand command then separated these values into individual events so each IP could be analyzed on its own. After that, stats count by src_ip was used to count how many times each source IP appeared, and finally sort -count organized the results from the most frequent IP to the least frequent.

## #120  
What protocol does Pycomm3 to use to read and write tag values?

**Answer:** EtherNet/IP  

<img width="640" height="265" alt="image" src="https://github.com/user-attachments/assets/0728bf11-d0f9-4424-9fa2-ffb19c330330" />  

Only search for it.

## #121  
What type of data can be used with the ‘request_data’ command?

**Answer:** any

Only search for it.

## #122
In alphabetical order, and separated by commas, i.e. a,b,c — What three drivers come installed with pycomm3?

**Answer:** CIPDriver,LogixDriver,SLCDriver  

<img width="640" height="770" alt="image" src="https://github.com/user-attachments/assets/bd6c1e32-babf-4bd9-9a4f-5f32abd023e2" />  

Only search for it.

## #123  
What type of PLCs can be used with Pycomm3 ?

**Answer:** allen-bradley,rockwell automation  

<img width="640" height="102" alt="image" src="https://github.com/user-attachments/assets/e9f539ef-f5b4-4a34-9819-e012caa52604" />  

Only search for it.
  
## #124  
What is the IP address of the Honeywell DSA Primary?

**Answer:** 10.1.0.101  

<img width="640" height="196" alt="image" src="https://github.com/user-attachments/assets/1c6eba66-6c70-4e17-8ac9-db4e1ee2daf7" />


  ```bash
index="dragos" Honeywell DSA Primary
```

or you can search for the default IP online.

## #125  
What popular shell was used to execute commands on remote hosts from the MSSQL server?

**Answer:** xp_cmdshell  

<img width="640" height="153" alt="image" src="https://github.com/user-attachments/assets/6647c86a-4518-4b59-819c-49ccb4a8c525" />  

## #126  
By default that command is disabled. What command is used to enable it?

**Answer:** sp_configure

## #127  
Asset 21151 was potentially compromised. What was the first notification related to the asset after compromise was detected?

**Answer:** PLC Date/Time Change  

<img width="640" height="206" alt="image" src="https://github.com/user-attachments/assets/04c2e696-8af9-49d7-af81-4fea13920b6e" />  

```bash
index="dragos"  21151
| table body _time
| dedup body
| sort _time
```

## #128  

One of the hosts on the network is used for running certain pieces of Siemens software and is named accordingly. It looks like one of the hosts was attempting to download a file multiple times. What is the IPv4 address of the destination it was trying to download the file from?

**Answer:** 192.168.192.74  

<img width="640" height="518" alt="image" src="https://github.com/user-attachments/assets/a675a2e6-f691-4815-9cb9-1f599771ca1a" />  

```bash
index="dragos"
| table src_host
| dedup src_host
```

<img width="640" height="310" alt="image" src="https://github.com/user-attachments/assets/d3a8302d-b88a-473e-b3e5-756fd1f0d5d2" />  

```bash
index="dragos"  src_host="desktop-qi8ghvg,ews-hq-siemens0"
```

Explanation: You can try both Siemens host devices until you reach the correct answer. We will go with ews-hq-siemens0, then conclude that the download request originates from this device, so we will search for the destination IP.

## #129  
Referring to the previous question, what was the extension of the file that was downloaded?

**Answer:** jar  

<img width="640" height="267" alt="image" src="https://github.com/user-attachments/assets/d76f0076-af43-4f81-a672-78a3507226ba" />  

```bash
index="dragos"  src_host="desktop-qi8ghvg,ews-hq-siemens0"
```
  
## #130  
What is the source IP address that tried to negotiate RDP on port 55555?

**Answer:** 192.168.208.1

<img width="640" height="192" alt="image" src="https://github.com/user-attachments/assets/eeb3026b-7b70-4508-9b59-b6e34e49ecb4" />  

```bash
index="dragos" RDP
```

Explanation: We will search for the word RDP and the answer is very straight forward.

## #131  
What is the common port number used for RDP?

**Answer:** 3389  

<img width="640" height="257" alt="image" src="https://github.com/user-attachments/assets/1bdd5cf2-f1cd-4385-a0ea-0aaacd759fb4" />  

Explanation: It is common knowledge that Remote Desktop Services (RDP), which are used to access remote devices, operate on port 3389.

## #132  
During a forwarded RDP Negotiation request with a nonstandard destination port with a Dragos Source ID of 7834, what was the destination host name?

**Answer:** rshistorian

<img width="640" height="250" alt="image" src="https://github.com/user-attachments/assets/0accb558-7572-4272-9269-bc3123317f74" />
<img width="640" height="202" alt="image" src="https://github.com/user-attachments/assets/771555ed-71f1-4684-9cb1-d587dbbad364" />

```bash
index="dragos" src_dragos_id=7834   
index="dragos" 7834 src_dragos_id=7834 body="Forwarded RDP Negotiation Request - nonstandard dst port"
```

Explanation: First we search with the src_dragos_id as in the question then we look in the body for any useful data, finally we reach our goal and get the dest_name

## #133  
What is the Dragos ID number of the rshistorian host?

**Answer:** 33

<img width="640" height="215" alt="image" src="https://github.com/user-attachments/assets/9d0cc5ee-9aa9-4fbb-9fa4-131166b06a5d" />


```bash
index="dragos" 7834 src_dragos_id=7834 body="Forwarded RDP Negotiation Request - nonstandard dst port" dest_host=rshistorian
```

## #134  
Which test asset IP address was scanned by NMAP from the source IP of 192.168.208.1?

**Answer:** 192.168.192.74

<img width="640" height="449" alt="image" src="https://github.com/user-attachments/assets/97d03677-c728-4864-aeed-735e8ad558b9" />


```bash
index="dragos"  src_ip="192.168.208.1"
|table _time dest_ip body
```

Explanation: We identified 192.168.208.1 as the source IP, as it was clearly running Nmap (a network scanning tool). We then used the table command to display the body and destination IP fields from the logs.

Thank you.




