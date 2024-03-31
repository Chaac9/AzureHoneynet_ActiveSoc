# Building a SOC + Honeynet in Azure

## Introduction

This project involves the use of the Azure cloud computing platform and its resources to create a honeynet as to collect activity logs of suspicious behavior and potential intrusion attacks. Resources such as a Window and Linux virtual machine have their defenses weakened and are exposed on the public internet. These implemented vulnerabilities allow for the collection of logs within the Log Analytics Workspace, which then allows us to create attack map visualizations, alerts, and incidents within the Azure Sentinel (SIEM) service. By leaving Azure cloud resources exposed for 24 hours, I was able to use security metrics to measure the efficacy of security alerts by comparing “Before” and “After” metrics.

![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/d6f42e60-6b2c-4290-bd14-6c44b8ff25db)


The architecture of the Azure honeynet:
-	Azure Key Vault
    -	A cloud service that securely stores and safeguards secrets used by Azure cloud applications such as passwords, certificates, and cryptographic keys
        -	https://learn.microsoft.com/en-us/azure/key-vault/general/basic-concepts
-	Azure Storage Account
    -	A cloud storage solution that serves as a central location that contains Azure storage data objects, such as blobs, files, queues, and tables.
        -	https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal
-	Log Analytics Workspace
    -	A repository for log data from various Azure services and resources such as Azure Active Directory  and ‘Event Viewer’ from Windows virtual machines.
        -	https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview
-	Microsoft Sentinel
    -	A cloud-native Security information and event management solutions that assists in intrusion detection and threat response.
        -	https://learn.microsoft.com/en-us/azure/sentinel/overview
-	Network Security Group (NSG)
    -	Used to filter network traffic through security rules that either allow or deny Inbound or Outbound traffic to and from Azure resources within the virtual network.
        -	https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works
-	Virtual Network
    -	Enables communication between Azure resources, on-premises networks, and the internet.
        -	https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview

Security metrics used in our measurements of the efficacy of our security solutions when strengthening our Azure cloud environment and resources:
-	AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)
-	SecurityAlert (Log Analytics Alerts Triggered)
-	SecurityEvent (Windows Event Logs)
-	SecurityIncident (Incidents created by Sentinel)
-	Syslog (Linux Event Logs)

The security metrics used in the “Before” group are those from Azure resources who had their security tools disabled and exposed to the public internet, allowing inbound traffic. These Azure resources include the Windows And Linux virtual machines which had their network security groups allow all inbound traffic from any IP sources and any ports, as well as having their built-in firewall disabled. Alerts and incidents can also derive from authentication failures attempts or the access of sensitive information from resources such as Microsoft Entra ID (Azure Active Directory) or Azure Key Vaults. 

The security metrics used in the “After” group are those used when the Azure resources are hardened after being exposed for 24 hours to the public internet. The Network Security groups for the virtual machines are reconfigured to only allow access from the host device using a private connection and their built-in firewalls are re-enabled. 

## Architecture Before Hardening / Security Controls
![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/c8887777-1ccc-4b08-8171-dda867f20d2d)


## Attack Maps Before Hardening / Security Controls
![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/bb12261e-bf7e-4baa-ab2c-0d61b05c3dbe)
![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/ddb8f7be-648e-433e-bfa8-ceb0e82a5ffe)
![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/995ed817-167f-430d-8619-5d1068df2c6f)
![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/ce6f4962-9c53-4ebb-84e4-73fc58136b7a)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-03-25 12:43:53
Stop Time 2024-03-26 12:43:53

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 14623
| Syslog                   | 6394
| SecurityAlert            | 20
| SecurityIncident         | 163
| AzureNetworkAnalytics_CL | 2711

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Architecture After Hardening / Security Controls
![image](https://github.com/Chaac9/AzureHoneynet_ActiveSoc/assets/98796264/e944791f-bdae-4acf-8ab0-bcc1c3a89413)



## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-03-26 12:43:53
Stop Time	2024-03-27 12:43:53

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 0
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.

1tion of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint
