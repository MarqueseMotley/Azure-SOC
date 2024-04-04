# Azure-SOC
# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://github.com/MarqueseMotley/Azure-SOC/assets/165986939/0912f316-cc32-4a4b-b64e-ecf8092bc34a)


## Introduction

For this endeavor, I constructed a compact honeynet within Azure and funneled log data from diverse sources into a Log Analytics workspace. Microsoft Sentinel leverages this data to craft attack visualizations, prompt alerts, and generate incident reports. Over a 24-hour period, I assessed security metrics within the vulnerable setup, implemented security measures to fortify the environment, conducted another 24-hour assessment, and now present the ensuing results. The showcased metrics include:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://github.com/MarqueseMotley/Azure-SOC/assets/165986939/0ff6bb14-d518-4f61-8528-888b76e1ac98)


## Architecture After Hardening / Security Controls
![Architecture Diagram](https://github.com/MarqueseMotley/Azure-SOC/assets/165986939/4bd8ea79-1764-470d-97af-1a4bf66d60df)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/MarqueseMotley/Azure-SOC/assets/165986939/62b906c8-6007-4ef4-8fc4-e5aa6f6382ea)
<br>
![Linux Syslog Auth Failures](https://github.com/MarqueseMotley/Azure-SOC/assets/165986939/1d052f44-14c6-4722-861d-8b86dd42ec7c)
<br>
![Windows RDP/SMB Auth Failures](https://github.com/MarqueseMotley/Azure-SOC/assets/165986939/8c645fc9-d47b-421f-85f3-16d9f853722a)
<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-04-01T18:37:19.0741684Z
Stop Time 2024-04-02T18:37:19.0741684Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 23929
| Syslog                   | 4718
| SecurityAlert            | 2
| SecurityIncident         | 168
| AzureNetworkAnalytics_CL | 3556

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-04-03T00:26:16.6517441Z
Stop Time	2024-04-04T00:26:16.6517441Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 11170
| Syslog                   | 27
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
