**🛡️ Lab: RMF 101 - Incident Response and Handling - Part2**

**🎯 Objective**

In this lab, you will:

1. Configure log forwarding from endpoints to the SIEM
2. Validate log ingestion using search or query
3. Apply filters to extract security-relevant data

This lab builds on the concepts from Part 1, focusing on the practical aspects of log collection and analysis.

---

**🧪 Lab Description**

This lab is Part 2 of the Incident Response and Handling series, focusing on log forwarding and SIEM integration. Students will learn how to collect, forward, and analyze security logs from various systems using industry-standard tools like Splunk.

---

**👁️ Observations**

- Splunk was not working when I first connected to the VM. I had to reinstall Splunk with `sudo ./splunk_reinstall_clean.sh`
- Stopped splunk services:
    
    Stop Splunk if it's running
    
    `sudo /opt/splunk/bin/splunk stop`
    
    Kill any remaining Splunk processes
    
    `sudo pkill -f splunk`
    
    `sudo pkill -f splunkd`
    
    Remove from system startup
    
    `sudo /opt/splunk/bin/splunk disable boot-start`
    
- Hard deleted everything Splunk-related and did a fresh installation of Splunk

---

**🚨 Vulnerabilities Identified**

Some potential weaknesses within the software include:

- Reinstalled Splunk: Malfunction

---

**🧪 My Lab Overview**

I uninstalled splunk completely, and then reinstalled splunk. After that I set up fake data for me to be able to look up and searched that data within splunk and created a few templates and saved them. One template for example I saved as Potential Brute Force Attacks and here’s the search that I saved:

`(
(sourcetype=windows:json OR sourcetype=winlogbeat) EventID=4625
)
OR
(
(sourcetype=linux_secure OR sourcetype=syslog) ("Failed password" OR "authentication failure")
)
| rex field=_raw "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| rex field=_raw "user=(?<username>\w+)"
| rex field=_raw "for (?<extracted_user>\w+) from"
| eval system=case(
sourcetype="windows:json" OR sourcetype="winlogbeat", "Windows",
sourcetype="linux_secure" OR sourcetype="syslog", "Linux"
)
| eval username=case(
sourcetype="windows:json" OR sourcetype="winlogbeat", TargetUserName,
sourcetype="linux_secure" OR sourcetype="syslog", coalesce(username, extracted_user)
)
| eval source_ip=case(
sourcetype="windows:json" OR sourcetype="winlogbeat", SourceIP,
sourcetype="linux_secure" OR sourcetype="syslog", src_ip
)
| stats count as attempts by source_ip, username, system
| where attempts > 2
| sort -attempts
| rename source_ip as "Source IP", username as "Username", system as "System", attempts as "Failed Attempts"`

---

📚 Lessons Learned

- Sudo is a very useful command for everything. I used it basically the whole lab. It allows a permitted user to execute a command as another user.
- I learned how to write search queries in Splunk to look for certain pieces of data, for example, my code above for potential brute force attacks
- I also learned how to completely uninstall Splunk, which took a good 10-25 minutes to learn.

🧰 Tools & Resources Used

- 🐧 Linux
- 💻 Terminal
- 📝 Text Editor

💭 Conclusion This lab helped me gain hands-on experience in conducting a **realistic risk assessment**. I learned how to use tools like Nmap, structure documentation, and assess risks using both qualitative and quantitative methods. It also reinforced the importance of documentation and attention to detail when evaluating security threats.