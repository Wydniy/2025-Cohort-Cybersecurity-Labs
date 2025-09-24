**🛡️ Lab: RMF 201 - Incident Handling and Response - Part - 3**

**🎯 Objective**

This lab will teach you how to:

1. Simulate a brute-force attack and generate alerts
2. Detect and investigate the simulated incident using the SIEM
3. Document the event and propose an escalation path
4. Create automated alerts for ongoing detection and response

---

**🧪 Lab Description**

This hands-on cybersecurity lab provides students with practical experience in simulating, detecting, and responding to brute force authentication attacks. Students will learn to generate realistic attack traffic, analyze security events using a SIEM platform, and document incident response procedures following industry best practices.

---

**👁️ Observations**

- The cat command on the terminal goes into a file or looks into something. for example I wrote `cat scripts/brute_force_ssh.py` to look into that file.
- Brute Force Attacks can be ran using Python in the terminal which I found interesting.

---

**🚨 Vulnerabilities Identified**

Some potential weaknesses within the software include:

Although there were no vulnerabilities, I used a code that used python that was a SSH brute force attack, ran it, and used another terminal to watch the logs of all of the attempts. After 108 attempts, the python code figured out the login: `weakuser: 123456` .

I also ran a RDP Brute Force Attack code in the terminal.

---

**🧪 My Lab Overview**

Looked into a code using python, and ran it using the terminal. This code was used to run brute force attacks and figure out a password for an account. As this code was running, I also had another terminal running which was used to check the logs and watch the attempts to find the password and username. 

---

🧰 Tools & Resources Used

- **SIEM Platform:** Splunk Enterprise
- **Target System:** Local Linux server with SSH and RDP services
- **Attack Tools:** Custom Python scripts and Hydra
- **Monitoring:** Real-time log analysis