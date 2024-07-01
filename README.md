![image](https://github.com/steevelodina/SIEM/assets/173463043/473b32b1-0a8d-4bac-ab46-228ae97bf752)

## Introduction
For this project, I developed a small Azure honeynet and ingested log sources from several sources into a workspace called Log Analytics. Microsoft Sentinel then uses this workspace to create incidents, generate alerts, and create attack maps. After measuring security metrics in the unsecure environment, I applied security measures to harden the environment and monitored security metrics again for a further day. The outcomes are displayed below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/steevelodina/SIEM/assets/173463043/04fd155f-b82d-4f59-8712-f141f208fca9)

## Architecture After Hardening / Security Controls
![image](https://github.com/steevelodina/SIEM/assets/173463043/1288f08b-839b-4b9d-aa1b-e57bc938d13b)

The following elements make up the Azure micro honeynet's architecture:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel
  
All resources were initially deployed and made available to the internet for the "BEFORE" metrics. All other resources were deployed with public endpoints visible to the Internet; that is, there was no necessity for private endpoints. The virtual machines had both their built-in firewalls and Network Security Groups wide open.

Network Security Groups were hardened for the "AFTER" metrics by preventing ALL traffic saved
from my admin workstation. All other resources were shielded by both private endpoints and the firewalls that were already installed.

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/steevelodina/SIEM/assets/173463043/b8dd3aac-86ca-417b-8168-2c3f23168cce)
![image](https://github.com/steevelodina/SIEM/assets/173463043/e31b2279-8186-4528-ab51-c262e7a4595b)
![image](https://github.com/steevelodina/SIEM/assets/173463043/db79d780-3a28-41a5-99c4-9b53c6bf2046)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:05:30
Stop Time 2023-03-16 17:05:30

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

This project involved building a little honeynet in Microsoft Azure and integrating log sources into a workspace for log analytics. Based on the ingested data, Microsoft Sentinel was used to generate incidents and set off alarms. Furthermore, measurements were taken in the compromised environment both before and after security safeguards were put in place. Notably, the implementation of security measures resulted in a significant decrease in the quantity of security events and incidents, indicating their efficacy.

Recall that in the 24 hours after the security restrictions were put into place, more security events and warnings probably would have been created if normal users were making heavy use of the network's resources.





