# Azure-Honeypot🍯

In this Honeypot project, we The project’s main objective was to expose, monitor, record, and then secure virtual machines against sophisticated cyber threats, utilizing a suite of Azure tools including Azure Log Analytics, Microsoft Sentinel, and Microsoft Defender for Cloud.

_**Inception State:**_ The project deployed a dual-phased approach: initially establishing an exposed environment to catalog and analyze potential attack vectors, followed by a secondary phase of implementing targeted hardening strategies. This methodology not only showcased the initial vulnerabilities but also highlighted the dramatic improvements in security that could be achieved through systematic adjustments based on the NIST 800-53 framework.

_**Completion State:**_ This honeypot project not only met but exceeded its objectives, by demonstrating a profound transformation from a highly vulnerable to a securely hardened environment. It serves as a compelling example of how targeted cybersecurity measures, underpinned by a deep analysis of attack data and trends, can dramatically enhance the security of networked systems. The project’s success lays a foundation for future security initiatives and provides a replicable model for similar cybersecurity enhancements across the industry.

---

![image](https://github.com/user-attachments/assets/72795e49-0416-4c91-a687-738da0040520)


# Technology Utilized
- Microsoft Azure
- Azure Virtual Machines
- Azure Log Analytics Workspace
- Microsoft Sentinel (SIEM)
- Microsoft Defender for Cloud
- Azure Network Security Groups (NSG)
- Azure Storage Account
- Azure Private Link
- Azure Key Vault

---


# Table of Contents

- [System Configurations & Set-up](#Step-1-System-Configurations-&-Set-up)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Mock Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

### Step 1) System Configurations & Set-up

To initiate the honeypot project, an Azure subscription was established, enabling access to a broad array of resources available on the Azure platform. A dedicated resource group named “HP-Cyber-Lab” was configured to serve as a centralized hub for all assets associated with this lab. This organizational strategy mirrors best practices in enterprise IT management, where resource groups are employed to maintain a structured and easily navigable architecture, supporting specific projects, teams, or business units.

two virtual machines (VMs) were provisioned with the following specifications:

**VM #1 - Windows Environment**

•	**Size**: Standard_E2bs_v5

•	**Operating System**: Windows 10 Pro

•	**vCPUs**: 2

•	**RAM**: 16GB
![WindowsVM - Overview](https://github.com/user-attachments/assets/cf63b8af-3ab4-4a31-89dc-9ed06cd00b7c)

**VM #2 - Linux Environment**

•	**Size**: Standard_E2bs_v5

•	**Operating System**: Ubuntu 20.04

•	**vCPUs**: 2

•	**RAM**: 16GB
![LinuxVM - Overview](https://github.com/user-attachments/assets/896b5a39-c860-4094-b7ab-38ef667fd17f)

---

### Step 2) Security Measures & Baseline

Following the provisioning of the virtual machines, the next critical phase involved establishing a security baseline for each system. Initially, both VMs were configured with standard recommended settings. Subsequent modifications were aimed at deliberately lowering defences to make the VMs more susceptible to cyber-attacks, thereby serving as effective honeypots.

**Windows 10 VM & Linux VM:**

1. **Network Security Group (NSG) Configuration**:

**Rule Adjustment**: The default NSG rule designed to block potentially malicious traffic was removed. This adjustment was intended to reduce the defensive posture of the VM.

**New Rule Implementation**: A permissive rule was added to allow all inbound traffic, regardless of origin, destination port, or protocol. This rule transformed the VM into a more attractive target for threat actors by appearing openly accessible on the network.

![WindowsVM - Net Settings](https://github.com/user-attachments/assets/ffb4cbfb-5bf3-4a50-88fa-fe82639da49f)

![LinuxVM - Net Settings](https://github.com/user-attachments/assets/f2686c4a-501a-4bae-82e1-dfdad244513a)

2. **Windows Defender Deactivation**: The built-in firewall and default security system, Windows Defender, was disabled. This action was taken to eliminate any barriers that could prevent the reconnaissance and exploitation attempts by malicious entities *(Only applicable for Windows 10 VM)*.

<img width="1512" alt="Windows VM Firewall" src="https://github.com/user-attachments/assets/8fc71152-5f0d-43df-8b44-d26a003ad9a0" />

3. **Logging and Monitoring**:

•	The VMs were configured to record detailed logs and security events. Specific queries were utilized to capture essential data regarding attack attempts and system interactions. This logging setup played a pivotal role in establishing a comprehensive incident-oriented baseline, documenting the initial state of security before any hardening measures were implemented.

![MS Sentinel Custom Rules](https://github.com/user-attachments/assets/740363bc-405b-4bac-a139-ffb8935382e3)

#### Step 3) Data Collection Methodology

To facilitate comprehensive data collection, a variety tools & Azure resources were configured to collaboratively capture, store, and analyze security-related data. These resources were strategically selected and configured to enable a holistic view of the security landscape affecting the virtual machines deployed in the project.

•	An Azure Log Analytics Workspace was established as the central repository for logs gathered from various Azure resources. This workspace serves as the primary platform for querying and analyzing collected data, enabling a consolidated view of security events and patterns.

2.	**Microsoft Sentinel**:

•	To enhance our capabilities for detecting, investigating, and responding to potential security threats, we deployed Microsoft Sentinel. This native Azure SIEM (Security Information and Event Management) system integrates seamlessly with other Azure services to provide advanced threat detection and response.

3.	**Microsoft Defender for Cloud**:

•	A Microsoft Defender for Cloud instance was activated to aggregate comprehensive security data, including system events, network activities, and detailed security logs from both Windows and Linux VMs. This information is crucial for understanding the security posture of each VM and is stored within the Log Analytics workspace for subsequent analysis.

4.	**Azure Storage Account**:

•	An Azure Storage Account was provisioned to manage the storage of raw log data, particularly for high-volume logs such as Network Security Group (NSG) flow logs. This setup ensures that large datasets are managed efficiently before they are processed and analyzed in the Log Analytics Workspace.

**Data Visualization and Threat Analysis**

**Threat Actor Visualization**:

In Microsoft Sentinel, a watchlist was created to assist in visualizing the geographic distribution of potential threat actors. This watchlist enables the generation of heat maps that display the physical locations of these actors, offering insights into attack origination points and highlighting regions with elevated activity levels.

### **Data Flow and Analysis**

These interconnected Azure services form a robust ecosystem for the continuous monitoring, recording, and analysis of security data. By leveraging this setup, the project captures a wide range of security metrics, providing a before-and-after snapshot of the environment’s security posture.

### **Data Recording Format**

The collected data is structured to facilitate clear before-and-after comparisons, crucial for assessing the effectiveness of the security measures implemented. Key metrics include:

•	Start and Stop Time

•	Security Events (Windows VMs)

•	Syslog (Linux VMs)

•	Security Alerts (Microsoft Defender for Cloud)

•	Security Incidents (Sentinel Incidents)

•	NSG Inbound Malicious Flows Allowed

---

### Step 3) Policy Finalization and Senior Leadership Sign-Off

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution.  

---

### Step 4) Mock Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  

#### Vulnerability Management Discussion

**Josh**: Good morning, Jimmy!  

**Jimmy**: Good morning! I heard you're ready to conduct some scans.  

**Josh**: Yep, now that our vulnerability management policy is in place, I wanted to get started on conducting some scheduled credentialed scans of your environment.  

**Jimmy**: Sounds good to me. What’s involved, and how can we help?  

**Josh**: We're planning to schedule weekly scans of the server infrastructure. We estimate it’ll take about 4 to 6 hours to scan all 200 assets. We’ll need you to provide administrative credentials so the scan engine can remotely log into the servers and assess them.  

**Jimmy**: Whoa, hold on. What exactly does scanning entail? I’m a bit concerned about resource usage, also you want admin credentials for all 200 machines? That doesn’t sound safe.  

**Josh**: Those are valid concerns. The scan engine sends different traffic to the servers to check for vulnerabilities. This includes looking at the registry, checking for outdated software, and identifying insecure protocols or suites. That’s why credentials are needed.  

**Jimmy**: I see. As long as it doesn’t take the servers offline, I think we’ll be okay.  

**Josh**: Absolutely. Let’s start by scanning just one server and monitor the resource utilization.  

**Jimmy**: That sounds like a good idea.  

**Josh**: Great. Also, for the credentials, could you set something up in Active Directory? You can leave the credentials disabled until we’re ready to scan, then enable them during the scan. Afterward, we can de-provision or disable the account. A kind of “just-in-time” access approach.  

**Jimmy**: That sounds good. I’ll have Susan start working on the automation for account provisioning.  

**Josh**: Awesome. Talk soon!  

**Jimmy**: Sounds good. I’ll get back to you once the credentials are set up. See you later!  

**Josh**: See you later!  

---

### Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  

<img width="402" alt="Scan 1" src="https://github.com/user-attachments/assets/ef4d31b9-154f-4c1e-b79b-3c14f6b754f6" />

---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates

---

### Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/bbf9478f-e1d1-4898-846e-b510ec8c6f72">

[Remediation Email](https://github.com/joshmadakor1/lognpacific-public/blob/main/misc/remediation-email.md)

---

### Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 

#### Vulnerability Management Discussion

**Josh**: Morning, Jimmy! How are you doing?  

**Jimmy**: Not bad for a Monday. How about you?  

**Josh**: I’m still alive, so I can’t complain. Before we dive into the vulnerabilities, how did the scan go on your end? Any outages or resource overutilization?  

**Jimmy**: The scan went well. We monitored it closely, and aside from all the open connections, we wouldn’t have even noticed a scan was happening.  

**Josh**: That’s good to hear. I didn’t expect any major issues, but we’ll keep monitoring going forward to ensure resource utilization stays in check. Do you mind if we dive into the findings?  
**Jimmy**: Absolutely.  

**Josh**: Great. Let me share my screen. Most of the vulnerabilities seem to come from outdated software, particularly Wireshark. You can see it’s installed on multiple servers, and the software is out of date.  

Another finding is that the local guest account on some servers belongs to the local administrators group, which is concerning. There were a few other vulnerabilities, such as the Microsoft Edge Chromium issues, which will likely be resolved by running Windows Updates.  

We also found vulnerabilities involving self-signed certificates, which aren’t critical. Lastly, we should address the deprecated cipher suites and insecure protocols, like TLS 1.1 and 1.0, as they’re no longer secure, making this a critical vulnerability.  

In summary, the main issues to remediate are:  
- **Outdated Wireshark installations**.  
- **Deprecated cipher suites and protocols**.  
- **Removing the local guest account from the administrators group**.  

**Jimmy**: Interesting. The good news is most of our servers likely share these vulnerabilities, so remediation should be straightforward.  

**Josh**: Exactly—a uniform issue makes things easier. Do you foresee any challenges with remediating the cipher suites and protocols?  

**Jimmy**: I doubt it’ll be a problem. We’ll run these changes through the next Change Control Board. As for Wireshark and the guest account, those shouldn’t be an issue either since they shouldn’t be on the servers in the first place. I’ll check with our CIS admins about that.  

**Josh**: Great. I’ll start building remediation packages to simplify the process for you.  

**Jimmy**: Sounds good.  

**Josh**: By the way, do you already have a patch management system in place for handling the Windows Update-related vulnerabilities?  

**Jimmy**: Yes, no worries there. Windows Updates are handled automatically, and everything should be patched by next week.  

**Josh**: Excellent. I’ll get started on researching the best ways to address the findings and have something ready for the next Change Control Board.  

**Jimmy**: Sounds good. Talk to you soon.  

**Josh**: Cool, talk to you soon!  


---

### Step 9) Mock CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed and approved the plan to remove insecure protocols and cipher suites. The plan included a rollback script and a tiered deployment approach.  

#### CAB Vulnerability Remediation Discussion

**Johnny**: Next up on the list are a couple of vulnerability remediations for the server team. First, the removal of insecure protocols, and second, the removal of insecure cipher suites. It looks like Josh from the Risk department is working in conjunction with Jimmy from Infrastructure on this. Jimmy, do you want to walk us through the technical aspects of the change being implemented?  

**Jimmy**: Normally, I would, but do you mind giving this one to Josh? He actually built the solution for us. We’re still getting used to the process.  

**Josh**: Sure, I can explain. Insecure cipher suites and protocols mean that the system is capable of negotiating and using outdated algorithms or protocols that have been deprecated. For example, if a server only supports these insecure protocols, a system could connect using them, which poses a security risk.  

These settings are controlled by the Windows registry. The fix is straightforward—we wrote a PowerShell script that disables all the insecure protocols and cipher suites while enabling the secure, standardized ones. It’s a simple but effective solution.  

**Jack**: That sounds good, but what if something goes wrong? Do we have a rollback plan in place?  

**Josh**: Absolutely. We’ve implemented a tiered deployment process. It starts with a pilot group of a few systems, then moves to pre-production, and finally to production for the full rollout.  

Additionally, we’ve built automated rollback scripts for each remediation. If any issues arise, the scripts will restore the original protocols and cipher suites, ensuring minimal disruption.  

**Jack**: That’s reassuring. Since the fixes are just registry updates, I’m not too concerned.  

**Josh**: Exactly, it’s a low-risk implementation. Any more questions?  

**[No further questions from the group.]**  

**Johnny**: Great, that wraps things up for this week’s CAB meeting. See you all next week!  

**Group**: See you later!


---
### Step 10 ) Remediation Effort

**Remediation Round 1: Outdated Wireshark Removal**

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/remediation-wireshark-uninstall.ps1)  

<img width="853" alt="Scan 2" src="https://github.com/user-attachments/assets/2807a01c-2a63-4478-8a64-cf86fa8380f3" />

**Remediation Round 2: Insecure Protocols & Ciphers**

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-cipher-suites.ps1)

<img width="848" alt="Scan 3" src="https://github.com/user-attachments/assets/29685f17-c995-47fa-b1f5-56a9d38975d9" />

**Remediation Round 3: Guest Account Group Membership**

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  

<img width="907" alt="Scan 4" src="https://github.com/user-attachments/assets/c18d0430-e4cc-4573-a7be-6675161c0f85" />

**Remediation Round 4: Windows OS Updates**

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="905" alt="Scan 5" src="https://github.com/user-attachments/assets/af441fdb-7f5f-472e-8825-701fc960a0c6" />

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="605" alt="Chart" src="https://github.com/user-attachments/assets/afef6535-0d95-44a4-b19b-a894d8b917cf" />

[Remediation Data](https://docs.google.com/spreadsheets/d/1cr3xjuoHGy_XTyVxa3yo96gj9QPJ0XIo0JSn9IHJzCU/edit?usp=sharing)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
