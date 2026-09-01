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

