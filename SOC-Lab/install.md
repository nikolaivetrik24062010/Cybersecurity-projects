SOC Lab – Splunk Log Analysis

This project demonstrates the process of setting up a Splunk Enterprise environment on macOS, ingesting Linux authentication logs, and analyzing brute-force attempts through search queries and visualizations.

🔹 1. Splunk Installation (macOS)
	•	Downloaded Splunk Enterprise 10.0.0 from Splunk Downloads.
	•	Selected macOS (Intel) .dmg package for easy installation.
	•	Installed via drag-and-drop and ran Splunk for the first time.
	•	Created the administrator account in the terminal (first-time setup).
 
<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 5 32 57 PM" src="https://github.com/user-attachments/assets/683a3ab5-c818-411d-9c7a-74bbd34eafce" />

📸 Screenshots included:
	•	Download page (Splunk 10.0.0 for macOS).
	•	First startup with admin account creation.

<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 5 40 17 PM" src="https://github.com/user-attachments/assets/a5724b1f-9798-46f0-8f88-375e7e8c1981" />

🔹 2. Dataset Collection
	•	Source: SecRepo.com – Security Datasets.
	•	Downloaded auth.log.gz (≈86k SSH login events).
	•	Dataset contains failed login attempts, invalid usernames, and SSH brute-force attempts from different IP addresses.

📸 Screenshots included:
	•	SecRepo dataset page.
 
<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 5 43 03 PM" src="https://github.com/user-attachments/assets/9b0410b3-89d3-48ca-9a68-61441e1e099d" />

🔹 3. Data Ingestion in Splunk
	•	Uploaded auth.log.gz via Add Data → Upload Files.
	•	Set Source Type = linux_secure (Splunk preset for Linux auth logs).
	•	Indexed and verified timestamps/events were parsed correctly.

📸 Screenshots included:
	•	Set Source Type (linux_secure).
	•	Event preview in Splunk.

<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 5 50 59 PM" src="https://github.com/user-attachments/assets/3b1325f8-49cd-40f4-bc6a-b2c6cf0389f5" />

🔹 4. Log Search & Analysis

Query 1: Search all events

index=* sourcetype=linux_secure

<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 6 48 49 PM" src="https://github.com/user-attachments/assets/899af5bb-dd44-4095-8e24-09eb750d120d" />

✅ Result: 86,839 events indexed.

Query 2: Detect failed logins

index=* sourcetype=linux_secure "Failed password"

<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 6 50 31 PM" src="https://github.com/user-attachments/assets/35d8a4af-b825-4fcb-bd05-d9a167007e73" />

✅ Extracted failed login attempts.

Query 3: Detect invalid users

index=* sourcetype=linux_secure "Invalid user"

<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 5 57 34 PM" src="https://github.com/user-attachments/assets/f70d1382-2d8e-4142-a255-a53d34d8cf73" />

✅ Extracted brute-force attempts with random usernames.

Query 4: Parse IPs and usernames

index=* sourcetype=linux_secure "Invalid user"
| rex "Invalid user (?<username>\w+) from (?<src_ip>[^\s]+)"
| stats count by src_ip, username
| sort - count

<img width="1352" height="878" alt="Снимок экрана 2025-09-10 в 6 06 16 PM" src="https://github.com/user-attachments/assets/76b5ec45-8de5-4bfd-971f-95d485dc37ef" />

✅ Aggregated table of attacker IPs and targeted usernames.
Example result:

src_ip	username	count
123.57.51.31	admin	360
188.87.35.25	test	96
220.99.93.50	nagios	65

📸 Screenshots included:
	•	Query execution.
	•	Table view with top brute-force IPs.

🔹 5. Skills Demonstrated
	•	SIEM setup: Installed and configured Splunk Enterprise on macOS.
	•	Log ingestion: Indexed Linux authentication logs from external dataset.
	•	Log parsing & extraction: Applied Splunk Search Processing Language (SPL) with regex.
	•	Threat analysis: Identified brute-force attempts and attacker infrastructure.
	•	SOC workflow: Simulated SOC process from ingestion → detection → reporting.

🔹 6. Next Steps
	•	Create a dashboard to visualize top attacker IPs and usernames.
	•	Build an alert for >10 failed logins from the same IP within 1 minute.
	•	Enrich attacker IPs with Threat Intelligence feeds (e.g., AbuseIPDB).



✅ This README shows a complete end-to-end lab: from setting up SIEM to analyzing a real-world dataset of attacks.
