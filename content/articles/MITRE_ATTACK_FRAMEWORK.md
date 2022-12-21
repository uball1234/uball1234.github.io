---
title: "MITRE ATT&CK FRAMEWORK"
date: 2022-12-13T18:44:56-08:00
draft: false
---

![](https://verveindustrial.com/wp-content/uploads/2021/05/5bfdce88cd3820f7c5c21e02_mitre.png)

## What is the MITRE ATT&CK Framework?

Before we can explain the MITRE ATT&CK Framework and what it is, we first need to understand what Advanced Persistent Groups (APT) and TTPs are. APTs are groups, teams, or even countries that engage in long-term attacks against other countries and organizations. Some common attributes of an APT include having vast amounts of resources at their disposal and sophistication of proprietary attacks and tools. In order to analyze APTs operations, security professionals use an approach called TTP, also known as Tactics, Techniques, and Procedures. Tactics can be understood as the adversary's goal or objective while the technique is how the adversary achieves the goal or objective. Finally the procedure is how the techniques are executed.  The MITRE ATT&CK framework can be looked at as a record and a document of common TTPs that APT groups use to attack enterprise windows, macOS, and linux networks. An easy way to think about ATT&CK is:

**A**dversaries
**T**actics
**T**echniques
**C**ommon **K**nowledge (procedures).

## Why is this Framework important?

The MITRE ATT&CK framework is important for both security analysts as well as penetration testers. Moreover, it is vital for security analysts because the framework takes the attackers point of view and allows security analysts (Blue Teamers) to understand the possible ways an adversary can attack their organization. It can help security analysts assess the effectiveness of their defensive measures and the processes of their security operation centers, through which they can identify areas of improvement. Furthermore, it also allows penetration testers (Red Teamers) an open source tool to find information to create a plan of attack.




## BREAKDOWN OF MITRE ATT&CK                     
### (TECHNIQUE & PURPOSE)

| **TECHNIQUE**            | **PURPOSE**                                                           |
|--------------------------|-----------------------------------------------------------------------|
| **Initial Access**       | Tactics used to gain initial access to a computing device             |
| **Execution**            | Methods to get process execution i.e. run a script, malware           |
| **Persistence**          | Methods to maintain access even if user logs off or system restarts   |
| **Privilege Escalation** | Tactics used to obtain elevated credentials i.e. SYSTEM or ROOT       |
| **Defense Evasion**      | Tactics and tools used to bypass antivirus and other defenses         |
| **Credential Access**    | How an adversary mines the local system and network for credentials   |
| **Discovery**            | Identifying interesting network resources i.e. file shares, databases |
| **Lateral Movement**     | The ability for the adversary to move from one machine to another     |
| **Collection**           | How an adversary might acquire data from local and network devices    |
| **Command and Control**  | Methods for communicating and maintaining remote access               |
| **Exfiltration**         | Moving data away and out of where it was gathered                     |
| **Impact**               | Causing an effect on the victim network i.e. delete logs, files       |


