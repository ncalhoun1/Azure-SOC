# Building a SOC + Honeynet in Azure (Live Traffic)

![Cloud Honeynet / SOC](https://i.imgur.com/FJP3df6.jpg)

## Introduction

In this project, I have constructed a mini honeynet within the Azure platform. The objective was to gather log data from diverse sources and channel it into a Log Analytics workspace. This workspace is then utilized by Microsoft Sentinel to generate attack maps, trigger alerts, and create incidents. To evaluate the security of the environment, I conducted measurements of various security metrics over a 24-hour period. Subsequently, I implemented security controls to fortify the environment and measured the metrics for an additional 24-hour duration. The results of these measurements are as follows:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/3vo3fwy.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/cJ6wFBH.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

Initially, all resources were deployed with open access to the internet. Virtual Machines had unrestricted Network Security Groups and built-in firewalls, while other resources had public endpoints visible to the internet, making private endpoints unnecessary

In the "AFTER" metrics phase, Network Security Groups were strengthened by blocking all traffic except for my admin workstation. Additionally, all other resources were safeguarded by their built-in firewalls and secured with Private Endpoint functionality.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/FLPiR6e.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/f4jCYRG.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/47MM8bc.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-04-25 03:09:28 PM
Stop Time  2023-04-26 03:09:28 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8956
| Syslog                   | 1568
| SecurityAlert            | 0
| SecurityIncident         | 189
| AzureNetworkAnalytics_CL | 193

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time2023-05-07-2023 2:13:16 PM
Stop Time	2023-05-08-2023 2:13:16 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 589
| Syslog                   | 24
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was built in Microsoft Azure to gather logs in a Log Analytics workspace. Microsoft Sentinel was utilized to generate alerts and incidents based on these logs. Metrics were measured in the insecure environment before implementing security controls and again afterward. The implementation of security measures resulted in a significant reduction in security events and incidents, highlighting the effectiveness of the controls.

# Azure-SOC
