# Splunk Brute-Force Detection Dashboard

This project simulates a real-world SOC (Security Operations Center) scenario by detecting brute-force login attempts using Splunk.

## 🔍 Project Overview

I created a custom `.log` file containing failed Windows login attempts and ingested it into a local Splunk instance. Using SPL (Splunk Processing Language), I queried and extracted key information—specifically IP addresses responsible for repeated failed logins. The results were then visualized in a Splunk Dashboard using Dashboard Studio (Grid layout).

## What I Did

- Installed and configured Splunk Enterprise locally
- Uploaded a custom `.log` file with simulated EventCode 4625 (failed login)
- Created an index: `bruteforce_logs`
- Used SPL with `rex` to extract source IPs from raw logs
- Built a dashboard panel titled: **Failed Login Attempts by Source IP**
- Saved the dashboard using Dashboard Studio (Grid layout)

## 💻 SPL Query Used

```spl
index=bruteforce_logs "Source Network Address"
| rex field=_raw "Source Network Address:\s+(?<source_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by source_ip
| sort -count
```

## 📁 Files Included

- `sample_failed_logins.log` – Custom log file with Windows Security events
- `spl_query.txt` – SPL query used for analysis
- `dashboard_screenshot.png` – Visual of the final panel (add this manually)
- `README.md` – This file

##  How This Applies to Real-World SOC Roles

This project demonstrates:
- Ability to work with SIEM tools like Splunk
- Hands-on skill writing SPL queries
- Experience detecting brute-force login patterns
- Strong documentation and visual presentation of data

## 🔗 Optional Improvements

- Add real-time alerts to notify on brute-force thresholds
- Integrate live Windows log forwarding with Splunk Universal Forwarder
- Expand analysis to include usernames, ports, and timestamps
