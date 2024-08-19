# Tryhackme-Retracted---Mother-s-Plea
This project investigates a cybersecurity incident in TryHackMe's "Retracted Room," focusing on a missing ransomware case. It traces file creation, identifies malicious programs, and uncovers a threat actor's actions using Event Viewer and Sysmon. The goal is to piece together the event timeline and resolve the case.


## Investigating the Missing Ransomware on TryHackMe

![image](https://github.com/user-attachments/assets/eb86951e-30e6-49d5-9e18-2357a259b1e0)


### Introduction

In this project, I tackled the "Retracted Room" challenge on TryHackMe, focusing on investigating a complex case of missing ransomware. The goal was to analyze various system events to trace the creation of malicious files, identify the tools used by the attacker, and uncover the actions of a threat actor who exploited a system through Remote Desktop Protocol (RDP). Using tools like Event Viewer and Sysmon, I pieced together a timeline of events to understand the full scope of the incident.

### Task 2 — The Message

Question 1: What is the full path of the text file containing the “message”?

![image](https://github.com/user-attachments/assets/f78d7ed4-78db-4fb5-b197-76c6e0f851ea)

Answer: C:\Users\Sophie\Desktop\SOPHIE.txt

Question 2: What program was used to create the text file?

For this question, when it comes to searching for the program used, the hint that comes to mind is focusing on the Sysmon events. I opened the Event Viewer and followed the path:

![image](https://github.com/user-attachments/assets/dec3a351-4755-47d6-b23c-ab922b41039a)

mathematica
Copy code
Application and Service Logs > Microsoft > Windows > Sysmon > Operational
I observed a process creation event, identified by Event ID 1. I used that ID number for filtering.

Next, I searched for the text file SOPHIE.txt using the find feature, as illustrated in the image below. The search find automatically redirected me to the event containing the text file.
![image](https://github.com/user-attachments/assets/b55e3686-dda7-4d09-9395-48caa15ee6ff)

![image](https://github.com/user-attachments/assets/b95d3bd3-61b3-4d4b-88e2-35f25097a6cf)

![image](https://github.com/user-attachments/assets/b763950b-55bd-4943-87e3-91f1e51430b1)



Answer: notepad.exe

Question 3: What is the time of execution of the process that created the text file? (Timezone: UTC, Format: YYYY-MM-DD hh:mm
)
I searched for the Notepad key as the file used to create the text file we found.

![image](https://github.com/user-attachments/assets/cec9aaa1-025d-4d74-b8aa-b038d0bcf53c)

![image](https://github.com/user-attachments/assets/974dfb31-907b-4e6b-b9aa-834c3a874762)


Answer: 2024-01-08 14:25:30

### Task 3 — Something Wrong

Question 1: What is the filename of this “installer”? (Including the file extension)
I opened Internet Explorer on the Windows machine’s home screen and checked for any downloads.

![image](https://github.com/user-attachments/assets/26075606-5e04-4049-ad04-32e1952a6310)


Answer: antivirus.exe

Question 2: What is the download location of this installer?
I opened the file through Explorer, and you will find the path.

Answer: C:\Users\Sophie\download

### Question 3: The installer encrypts files and then adds a file extension to the end of the file name. What is this file extension?

Since we have the name of the installer, I searched for it in the Event Viewer.
![image](https://github.com/user-attachments/assets/84764667-9b4d-4c9f-ac5c-47293e548736)


Answer: .dmp

Question 4: The installer reached out to an IP. What is this IP?
Since the network connection has the event ID 3, I used it for filtering. After that, I searched for "Download."

![image](https://github.com/user-attachments/assets/63d8eef9-1f3b-4614-b963-40c5f8780896)

![image](https://github.com/user-attachments/assets/63ef3332-6936-4ca8-a384-1b190e529976)


Answer: 10.10.8.111

###Task 4 — Back to Normal

Question 1: The threat actor logged in via RDP right after the “installer” was downloaded. What is the source IP?
Since the threat actor used RDP, this indicates a network connection. I retained the previous filter for Event ID 3.

![image](https://github.com/user-attachments/assets/2f9c9ef6-7724-40a1-ae4b-755ce5ab093a)

Answer: 10.11.27.46

Question 2: This other person downloaded a file and ran it. When was this file run? (Timezone: UTC, Format: YYYY-MM-DD hh:mm
)
Considering we had seen a decryptor file downloaded before, I looked for the decryptor file and set the filter to 1 since that’s the event for process creation.
![image](https://github.com/user-attachments/assets/25400a76-4c69-4df4-964c-64bee838da2e)

![image](https://github.com/user-attachments/assets/ade4a7f8-920f-4347-a46f-61c0f7d6d07a)

![image](https://github.com/user-attachments/assets/aa79cd26-b61a-44c1-8225-9ec4083792a2)


Answer: 2024-01-08 14:24:18

### Task 5 — Doesn’t Make Sense
Arrange the following events in sequential order from 1 to 7, based on the timeline in which they occurred:

1.Sophie downloaded the malware and ran it.
2. The malware encrypted the files on the computer and showed a ransomware note.
3. Sophie ran out and reached out to you for help.
4. Someone else logged into Sophie’s machine via RDP and started looking around.
5. The intruder downloaded a decryptor and decrypted all the files.
6. A note was created on the desktop telling Sophie to check her Bitcoin.
7. We arrive on the scene to investigate

## Conclusion

Through meticulous analysis and the use of advanced forensic tools, I successfully traced the sequence of events in the ransomware case, identifying the key actions taken by the threat actor. This project not only enhanced my understanding of incident response and forensic investigation but also reinforced the importance of thorough analysis in cybersecurity. The insights gained from this investigation can be applied to similar cases in real-world scenarios, helping to prevent and mitigate future attacks.
