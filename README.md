# Splunk-Dragos-Bots
CyberLab-09

<p align="center">
<img width="450" height="489" alt="image" src="https://github.com/user-attachments/assets/b37aa0b1-a001-4ba7-889e-75cb1b0d34d6" />
</p>

Hello Guys ! today I’m going to walkthrough one of Splunk scenarios related to IT/OT security.

https://bots.splunk.com/

 ## Scenario:
1up your ics/ot cybersecurity team

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

### 104  
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






