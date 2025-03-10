# AWS WAF - Uptime Robot IPs Blocked

## Overview
This document outlines the process to check if Uptime Robot IPs are being blocked by AWS WAF. The query provided helps filter and analyze blocked requests from specific Uptime Robot IPs.

## How to Get Uptime Robot IPs
Uptime Robot regularly updates its list of monitoring IPs. You can retrieve the latest IPs by:
1. Visiting the Uptime Robot status page: [https://uptimerobot.com/inc/files/ips/IPv4.txt](https://uptimerobot.com/inc/files/ips/IPv4.txt)
2. Checking their official documentation: [https://uptimerobot.com/help/](https://uptimerobot.com/help/)
3. Using the API to programmatically fetch the latest IP addresses.

## Query to Check Blocked Uptime Robot IPs
Use the following AWS WAF query to identify blocked requests from Uptime Robot IPs:

```sql
fields @timestamp, httpRequest.clientIp, action, ruleId
| filter action == "BLOCK"
| filter httpRequest.clientIp in [
  "216.144.250.150", "69.162.124.226", "69.162.124.227", "69.162.124.228", "69.162.124.229", "69.162.124.230", "69.162.124.231", "69.162.124.232", "69.162.124.233", "69.162.124.234", "69.162.124.235", "69.162.124.236", "69.162.124.237", "69.162.124.238", "63.143.42.242", "63.143.42.243", "63.143.42.244", "63.143.42.245", "63.143.42.246", "63.143.42.247", "63.143.42.248", "63.143.42.249", "63.143.42.250", "63.143.42.251", "63.143.42.252", "63.143.42.253", "216.245.221.82", "216.245.221.83", "216.245.221.84", "216.245.221.85", "216.245.221.86", "216.245.221.87", "216.245.221.88", "216.245.221.89", "216.245.221.90", "216.245.221.91", "216.245.221.92", "216.245.221.93", "208.115.199.18", "208.115.199.19", "208.115.199.20", "208.115.199.21", "208.115.199.22", "208.115.199.23", "208.115.199.24", "208.115.199.25", "208.115.199.26", "208.115.199.27", "208.115.199.28", "208.115.199.29", "208.115.199.30", "216.144.248.18", "216.144.248.19", "216.144.248.20", "216.144.248.21", "216.144.248.22", "216.144.248.23", "216.144.248.24", "216.144.248.25", "216.144.248.26", "216.144.248.27", "216.144.248.28", "216.144.248.29", "216.144.248.30", "46.137.190.132", "122.248.234.23", "167.99.209.234", "178.62.52.237", "54.79.28.129", "54.94.142.218", "104.131.107.63", "54.67.10.127", "54.64.67.106", "159.203.30.41", "46.101.250.135", "18.221.56.27", "52.60.129.180", "159.89.8.111", "146.185.143.14", "139.59.173.249", "165.227.83.148", "128.199.195.156", "138.197.150.151", "34.233.66.117", "52.70.84.165", "54.225.82.45", "54.224.73.211", "3.79.92.117", "3.21.136.87", "35.170.215.196", "35.153.243.148", "18.116.158.121", "18.223.50.16", "54.241.175.147", "3.212.128.62", "52.22.236.30", "54.167.223.174", "3.12.251.153", "52.15.147.27", "18.116.205.62", "3.20.63.178", "13.56.33.4", "52.8.208.143", "34.198.201.66", "35.84.118.171", "44.227.38.253", "35.166.228.98", "99.80.173.191", "99.80.1.74", "3.111.88.158", "13.127.188.124", "18.180.208.214", "54.249.170.27", "3.105.190.221", "3.105.133.239"
]
| sort @timestamp desc
| limit 100
```

## Steps to Check AWS WAF Logs
1. Open **AWS WAF & Shield** in the AWS Management Console.
2. Navigate to **Logs Insights**.
3. Select the AWS WAF log group where blocked requests are stored.
4. Copy and paste the above query.
5. Click **Run query**.

![image](https://github.com/user-attachments/assets/d743e41f-992d-4a8a-a86f-f8850cbc0ee2)


## Resolving Blocked Uptime Robot IPs
If Uptime Robot IPs are being blocked:
- Verify your AWS WAF rules and allowlist Uptime Robot IPs if needed.
- Check rate-based rules that might be unintentionally blocking legitimate requests.
- Adjust rule priorities to ensure critical monitoring services are not affected.

## Conclusion
This query helps identify if Uptime Robot monitoring requests are being blocked by AWS WAF. Regularly monitoring logs and adjusting rules ensures smooth operation and accurate uptime monitoring.

