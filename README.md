# 🌐 Wireshark DNS Traffic Analysis – Network Inspection & Security Analysis

## 📌 Project Overview

This project demonstrates hands-on network traffic analysis using Wireshark on macOS, focusing on DNS (Domain Name System) activity. The goal was to capture live network traffic, isolate DNS queries, and analyze how systems communicate with external services during normal browsing.

This project simulates how a **security analyst monitors network behavior**, identifies domain requests, filters noise, and interprets traffic patterns to understand system activity and potential risks.

---

## 🎯 Objectives

* Capture live network traffic using Wireshark
* Filter and isolate DNS traffic from background noise
* Analyze domain name queries and responses
* Understand how websites trigger multiple backend services
* Develop practical network troubleshooting and analysis skills

---

## 🛠️ Tools Used

* Wireshark 4.6.4
* macOS
* Terminal (nslookup)

---

## 🖥️ Interface Used

* Wi-Fi: en0

---

# 🔍 Methodology

## 1. Traffic Capture

* Selected Wi-Fi interface (en0)
* Started live packet capture
* Generated traffic by:

  * Visiting websites (Google, YouTube, etc.)
  * Performing manual DNS lookup:
    nslookup espn.com

---

## 2. Filtering DNS Traffic

### Filters Used

dns
→ Displays all DNS traffic

dns && !mdns
→ Removes multicast DNS noise from local network

dns.qry.name
→ Highlights queried domain names

dns && ipv6
→ Captures DNS traffic over IPv6

---

## 3. Packet Analysis

* Inspected individual packets
* Analyzed DNS query and response structure
* Observed source/destination IPs and domain resolution

---

# 📊 Key Findings

### Multiple DNS Requests per Action

A single user action triggered multiple DNS queries.

Examples observed:

* accounts.google.com → Authentication service
* akamai...net → Content Delivery Network (CDN)
* bam.cell.nr-data.net → Analytics/monitoring service
* espn.com → Manual DNS lookup target

---

### Background Services Are Always Active

Websites rely on multiple external services:

* Authentication systems
* Analytics trackers
* CDNs for performance
* APIs and embedded content

---

### IPv6 Traffic Presence

* DNS traffic was observed over IPv6
* Filtering only IPv4 missed valid packets

---

### DNS Caching Behavior

* Previously visited domains did not always generate new queries
* Manual lookup (nslookup) forced fresh DNS requests

---

# 🧠 Key Security Insights

DNS traffic reveals:

* What websites a system is contacting
* Hidden background services and third-party dependencies
* Potential indicators of suspicious or malicious activity

Example:

* Unknown or unusual domains could indicate malware communication
* High-frequency DNS requests may signal automated behavior

---

# 🔐 Security Analysis

DNS is a critical part of network communication but also a common target for attacks.

### Potential Risks:

* DNS spoofing / poisoning
* Data exfiltration via DNS
* Communication with malicious domains
* Tracking via analytics and third-party services

### Observations from this Lab:

* All observed domains were legitimate
* No suspicious or malicious traffic detected
* Traffic patterns matched normal browsing behavior

---

# ⚠️ Challenges & Troubleshooting

### 1. Blank Filter Results

Cause:

* DNS caching
* No new DNS queries generated

Solution:

* Performed manual lookup using:
  nslookup espn.com

---

### 2. Noise from Local Traffic

Cause:

* Multicast DNS (mDNS)

Solution:

* Applied filter:
  dns && !mdns

---

### 3. IPv4 vs IPv6 Mismatch

Cause:

* System using IPv6 for DNS queries

Solution:

* Used filter:
  dns && ipv6

---

# 📚 Key Learnings

* How to capture and analyze live network traffic
* How DNS works in real-world environments
* How to apply Wireshark filters effectively
* How caching impacts network visibility
* How to differentiate normal vs suspicious traffic
* How websites depend on multiple backend services

---

# 🧩 Analyst Perspective

A security analyst can use DNS traffic to:

* Monitor user activity patterns
* Detect suspicious domains
* Identify potential malware communication
* Investigate network incidents

Even without payload data, DNS provides **valuable intelligence about system behavior**.

---

# 📸 Screenshots & Analysis

### DNS Query Analysis

<img width="1440" height="900" alt="Screenshot 2026-04-12 at 10 21 03 PM" src="https://github.com/user-attachments/assets/654a9c3c-63eb-4ee9-9c78-b49faecb3c68" />


* Shows domain resolution requests and responses
* Highlights external services contacted during browsing

### TCP & HTTPS Traffic (Port 443)

<img width="1440" height="900" alt="Screenshot 2026-04-12 at 10 24 33 PM" src="https://github.com/user-attachments/assets/52a966fe-d2d0-475d-b71d-e2a942b355f8" />


* Demonstrates encrypted communication after DNS resolution
* Shows connection setup and packet exchange

---

# 🚀 Future Improvements

* Analyze HTTP/HTTPS traffic patterns
* Investigate suspicious domains using threat intelligence tools
* Capture longer sessions for deeper analysis
* Combine with SIEM tools (e.g., Splunk)
* Perform malware traffic analysis in a controlled lab

---

# 🏁 Conclusion

This project demonstrates how DNS traffic can be analyzed to understand system behavior and network communication patterns. By filtering noise and focusing on relevant data, it is possible to gain meaningful insights into how systems interact with external services.

This lab provides a strong foundation for:

* Network traffic analysis
* DNS investigation
* Security monitoring and threat detection

---

## 👤 Author

Ashnoor Jattana

---
