# Wireshark DNS Traffic Analysis

## Project Overview

This project demonstrates basic network traffic analysis using Wireshark on macOS. The goal was to capture live network traffic, isolate DNS activity, remove local multicast noise, and analyze the domains contacted by the system during normal browsing and manual DNS lookups.

This project helped build foundational cybersecurity skills in packet capture, DNS analysis, traffic filtering, troubleshooting, and interpreting background network communications.

## Objective

* Capture live traffic from the Wi-Fi interface using Wireshark
* Filter DNS traffic from general network noise
* Identify real domain lookups made by the system
* Understand how websites trigger multiple background service requests
* Practice beginner-friendly network analysis and troubleshooting

## Tools Used

* Wireshark 4.6.4
* macOS
* Terminal (`nslookup`)

## Interface Used

* `Wi-Fi: en0`

## Key Filters Used

* dns - Shows DNS traffic.
* dns && !mdns - Shows DNS traffic while excluding multicast DNS local network chatterz
* dns.qry.name - Helps identify queried domain names more clearly.
* dns && ipv6 - Shows DNS traffic over IPv6.

## Procedure

1. Installed Wireshark and configured the helper tool required for packet capture on macOS.
2. Opened Wireshark and selected the `Wi-Fi: en0` interface.
3. Started a live capture.
4. Generated traffic by visiting websites and performing a manual DNS lookup using:

```bash
nslookup espn.com
```

5. Applied filters to isolate DNS traffic.
6. Examined packet details to identify queried domains and related background services.
7. Noted that some traffic used IPv6 rather than IPv4, which affected filtering.

## Findings

The capture showed that one user action can trigger multiple DNS lookups for background services.

Examples observed:

* `accounts.google.com` — Google authentication service
* `akamai...net` — content delivery network traffic
* `bam.cell.nr-data.net` — analytics and monitoring service
* `espn.com` — manual DNS lookup target

## Key Observations

* DNS requests are used to translate domain names into IP addresses.
* Some website traffic did not appear immediately because of DNS caching.
* Manual lookup with `nslookup` forced a fresh DNS request.
* Multicast DNS (`mdns`) created noise and needed to be filtered out.
* IPv6 DNS traffic was present, so filtering only by IPv4 missed valid packets.
* A single website often depends on several external services such as authentication, analytics, fonts, and content delivery networks.

## Challenges and Troubleshooting

### 1. Blank filtered results

At times, filters returned no packets. This happened because:

* DNS responses were cached
* A fresh DNS request had not occurred during the capture
* Traffic was using IPv6 instead of the expected IPv4 address

### 2. Noise from local network traffic

`MDNS` traffic appeared frequently and had to be excluded using:

```text
dns && !mdns
```

### 3. IPv4 vs IPv6 mismatch

Filtering with an IPv4 address did not capture all DNS traffic because the system was using IPv6 for DNS queries.

## What I Learned

* How to install and use Wireshark for live packet capture
* How DNS works at a practical level
* How to apply display filters to isolate meaningful traffic
* How caching affects network visibility
* How to recognize normal background domains versus potentially suspicious ones
* How websites communicate with multiple supporting services behind the scenes

## Why This Project Matters

* Capture and inspect live traffic
* Interpret DNS behavior
* Troubleshoot missing results
* Analyze network communications with an investigative mindset

## Author

Ashnoor Jattana
