# Azure-Honeypot🍯

The project’s main objective was to expose, monitor, record, and then secure virtual machines against sophisticated cyber threats, utilizing a suite of Azure tools including Azure Log Analytics, Microsoft Sentinel, and Microsoft Defender for Cloud.

_**Inception State:**_ The project deployed a dual-phased approach: initially establishing an exposed environment to catalog and analyze potential attack vectors, followed by a secondary phase of implementing targeted hardening strategies. This methodology not only showcased the initial vulnerabilities but also highlighted the dramatic improvements in security that could be achieved through systematic adjustments based on the NIST 800-53 framework.

_**Completion State:**_ This honeypot project not only met but exceeded its objectives, by demonstrating a profound transformation from a highly vulnerable to a securely hardened environment. It serves as a compelling example of how targeted cybersecurity measures, underpinned by a deep analysis of attack data and trends, can dramatically enhance the security of networked systems. The project’s success lays a foundation for future security initiatives and provides a replicable model for similar cybersecurity enhancements across the industry.

---

![image](https://github.com/user-attachments/assets/72795e49-0416-4c91-a687-738da0040520)


# Technology/Tools Utilized
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

- [System Configurations & Set-up](#step-1-system-configurations--set-up)
- [Security Measures & Baseline](#step-2-security-measures--baseline)
- [Data Collection Methodology](#step-3-data-collection-methodology)
- [Analysis of Initial Exposure](#step-4-analysis-of-initial-exposure)
- [Post Hardening Analysis](#step-5-post-hardening-analysis)
- [Conclusion](#step-6-conclusion)
    
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

![Sys Logs](https://github.com/user-attachments/assets/86ff2f3d-a2c8-4f96-bf2b-3719a89b7dc5)

![AzureNetworkAnalytics_CL Logs](https://github.com/user-attachments/assets/b384fc90-f5c8-40f0-a05b-60324133a79a)

![Security Event Logs](https://github.com/user-attachments/assets/9a45f192-99cb-4034-9f7a-4e040c9c9033)

### Step 3) Data Collection Methodology

To facilitate comprehensive data collection, a variety tools & Azure resources were configured to collaboratively capture, store, and analyze security-related data. These resources were strategically selected and configured to enable a holistic view of the security landscape affecting the virtual machines deployed in the project.

## **Infrastructure Setup**

1.	***Azure Log Analytics Workspace***:

•	An Azure Log Analytics Workspace was established as the central repository for logs gathered from various Azure resources. This workspace serves as the primary platform for querying and analyzing collected data, enabling a consolidated view of security events and patterns.

2.	**Microsoft Sentinel**:

•	To enhance our capabilities for detecting, investigating, and responding to potential security threats, we deployed Microsoft Sentinel. This native Azure SIEM (Security Information and Event Management) system integrates seamlessly with other Azure services to provide advanced threat detection and response.

3.	**Microsoft Defender for Cloud**:

•	A Microsoft Defender for Cloud instance was activated to aggregate comprehensive security data, including system events, network activities, and detailed security logs from both Windows and Linux VMs. This information is crucial for understanding the security posture of each VM and is stored within the Log Analytics workspace for subsequent analysis.

![Defender Security Posture Score](https://github.com/user-attachments/assets/a6bf79ec-3927-4e6a-93d4-54e147551893)

4.	**Azure Storage Account**:

•	An Azure Storage Account was provisioned to manage the storage of raw log data, particularly for high-volume logs such as Network Security Group (NSG) flow logs. This setup ensures that large datasets are managed efficiently before they are processed and analyzed in the Log Analytics Workspace.

![MS Sentinel Custom Rules](https://github.com/user-attachments/assets/740363bc-405b-4bac-a139-ffb8935382e3)

## **Data Visualization and Threat Analysis**

**Threat Actor Visualization**:

In Microsoft Sentinel, a watchlist was created to assist in visualizing the geographic distribution of potential threat actors. This watchlist enables the generation of heat maps that display the physical locations of these actors, offering insights into attack origination points and highlighting regions with elevated activity levels.

![Linux SSH Auth Map](https://github.com/user-attachments/assets/845e4918-47ff-43ba-b9be-0dbf70c7f829)

![NSG Map](https://github.com/user-attachments/assets/affeb5c2-cd75-4b85-beb0-96c3659a7b90)

![Windows RDP Auth Map](https://github.com/user-attachments/assets/91036e34-3eb1-4fcb-831e-6621dae09616)

## **Data Flow and Analysis**

These interconnected Azure services form a robust ecosystem for the continuous monitoring, recording, and analysis of security data. By leveraging this setup, the project captures a wide range of security metrics, providing a before-and-after snapshot of the environment’s security posture.

## **Data Recording Format**

The collected data is structured to facilitate clear before-and-after comparisons, crucial for assessing the effectiveness of the security measures implemented. Key metrics include:

•	Start and Stop Time

•	Security Events (Windows VMs)

•	Syslog (Linux VMs)

•	Security Alerts (Microsoft Defender for Cloud)

•	Security Incidents (Sentinel Incidents)

•	NSG Inbound Malicious Flows Allowed

![HP Project Stats Record](https://github.com/user-attachments/assets/4c40b60d-f908-4fbc-b2a6-3c23bf82b221)

---

### Step 4) Analysis of Initial Exposure

The initial exposure phase of the honeypot project, designed to evaluate the vulnerabilities of unsecured virtual environments on Azure, yielded critical insights into the nature and frequency of cyber threats. By deliberately lowering defenses, such as disabling Windows Defender and modifying Network Security Group settings to permit all inbound traffic, both the Linux and Windows VMs attracted a wide range of attacks, including brute force SSH attacks and extensive network scanning. These activities were heavily documented and analyzed using Microsoft Sentinel and Azure Log Analytics Workspace, providing a detailed view of attack patterns and origins, particularly highlighting the global nature of cyber threats.

![Analysis Stats](https://github.com/user-attachments/assets/c1321a23-20fc-4129-94fb-c596e046d8b3)

**Types of Attacks Detected**

1.	**Brute Force SSH Attempts (Linux VMs)**:

**Description**: The SysLog and NSG flow logs recorded multiple failed SSH login attempts, indicating a brute force attack strategy aimed at guessing passwords to gain unauthorized access.

**Frequency**: High frequency, with numerous attempts recorded within a 24-hour period.

**Source**: Primarily from IP addresses that seem to originate from diverse geographic locations, as indicated by the initial review and subsequent heat map analyses.

2.	**Network Scanning and Probing (Windows VMs)**:

**Description**: Security event logs from the Windows VMs suggest various reconnaissance activities, including network scans which are typically preliminary activities to identify open ports and vulnerable services.

**Frequency**: Multiple incidents were detected, pointing to systematic scanning activities.

**Sources:** The heat maps created using Sentinel watchlists revealed that the majority of attack attempts originated from specific regions, notably Eastern Europe and East Asia, highlighting these as hotspots for the origin of malicious traffic.

![Sentinel Analytics](https://github.com/user-attachments/assets/900dc307-a87b-4153-aa78-eac9d7cfbf4f)

![Sentinel Incidents](https://github.com/user-attachments/assets/3aeec363-e156-4f6a-a7a7-5933512941f2)

**Notable Security Incidents**

1.	**High Volume of Inbound Malicious Flows (NSG Logs)**: The NSG logs showed 3,443 inbound malicious flows that were allowed, indicating significant exposure to network-based attacks. 

2.	**Sentinel Incidents**: There were 239 security incidents logged by Microsoft Sentinel, 128 in the last 24 hours, which collated and analyzed security events from various sources to flag potential security breaches or suspicious activities.

![Sentinel Overview](https://github.com/user-attachments/assets/2338950f-72aa-4282-93d8-3d385c6928e1)

**Frequency and Distribution of Attacks**

The project setup ensured continuous monitoring, with the data showing a persistent and consistent pattern of attack attempts across both VMs. This persistent threat activity underscores the attractiveness of the honeypot to attackers.

The data collected serves as a fundamental baseline for the next phase of the project, where specific security hardening measures will be implemented and evaluated for their effectiveness in mitigating these identified threats. This process not only underscores the critical necessity for robust security measures but also sets the stage for data-driven enhancements to better protect networked systems.

![nsg-malicious-allowed-in](https://github.com/user-attachments/assets/7f516c4b-4392-4196-bf9d-bc2941bbbc43)

![windows-rdp-auth-fail](https://github.com/user-attachments/assets/3ee577ad-81a2-4097-8f9d-abd63646c27d)

![linux-ssh-auth-fail](https://github.com/user-attachments/assets/2bd32dc3-198e-47a7-8420-bf4ff34730de)

---

## System Hardening

In response to the identified gaps in the the NIST SP 800-53 R5 framework as well as information communicated by the MS Cloud Security Benchmark, targeted hardening efforts were prioritized to bolster the security of network communications and resource accessibility within the honeypot environment. Focusing on the System and Communications Protection domain substantially hardened the network security of the honeypot environment. The following is a new network Topology set up. Among other things,  one of the primary changes was the inclusion of the resources into a segmented network with extremely secure parameters.

![NIST 800-53](https://github.com/user-attachments/assets/a4774c97-64b2-42a0-8d03-cbc64c218ff0)


**Enhancements Undertaken:**

1.	**Implementation of Private Endpoints:**

•	**Private Links for Key Vault and Storage Accounts**: To mitigate the risk of unauthorized data exposure and interception, private endpoints were established for critical Azure resources such as the Key Vault and Storage accounts. These private links ensure that all data transmitted to and from these resources occurs within the Azure backbone network, thereby not exposing data to the public internet.

•	**Benefits**: This configuration significantly reduces the attack surface by ensuring that access to these resources is strictly controlled and not reachable via the public internet. It also complies with strict data residency and sovereignty requirements by confining data to a specific geographic region.

![PE Overview](https://github.com/user-attachments/assets/51daeec9-c6ab-42e0-ac16-d9e15756b1e1)

![PE Blob Overview](https://github.com/user-attachments/assets/1469cfe4-2d6b-4cad-a4ef-af6e2e7fb1b1)

![PE AKV Overview](https://github.com/user-attachments/assets/1c4322cc-c6e6-4b22-bbba-3f6172dbcab3)

2.	**Firewall Configuration Adjustments:**

•	**NSG Rules Modification**: The Network Security Group (NSG) rules for the virtual machines were meticulously revised to deny all inbound and outbound traffic except from designated IP addresses, specifically the IP address of the security operations center. This stringent rule set ensures that only authorized personnel have network access to the honeypot VMs, thus significantly enhancing the security posture.

•	**Benefits**: This measure not only minimizes the potential for malicious access but also aligns with the principle of least privilege, ensuring that only necessary communications are permitted. This configuration aids in effective perimeter security management and reduces the likelihood of accidental or malicious breaches.

![Windows NSG](https://github.com/user-attachments/assets/7fa57ac0-c1f8-47da-a35b-424b0a82eb32)

![Linux NSG](https://github.com/user-attachments/assets/366ecc40-a721-4a6d-ae24-d1854f359a10)

Focusing on the System and Communications Protection, specifically the boundary protection enhancements substantially hardened the network security of the honeypot environment. In addressing these gaps identified by the NIST SP 800-53 R5 compliance framework, significant hardening measures were implemented within the honeypot project’s virtual environments. Private endpoints were established for the Key Vault and Storage account resources, ensuring that data interactions remain within the secure confines of the Azure network and not exposed to the public internet. Furthermore, the Network Security Group (NSG) rules were modified to deny all inbound and outbound traffic except from specified IP addresses, drastically reducing the risk of unauthorized access. These enhancements, markedly fortified the network security, aligning with data security standards and substantially mitigating potential cyber threats.

### Step 5) Post Hardening Analysis

The targeted hardening efforts focused on System and Communications Protection have substantially enhanced the overall security posture of the honeypot environment. By strategically applying improvements based on compliance frameworks and security benchmarks, the project now demonstrates a robust defence mechanism capable of significantly mitigating potential cyber threats. The results of these hardening measures provide a compelling testament to the efficacy of data-driven and compliance-focused security enhancements in protecting networked environments against increasingly sophisticated cyber-attacks.

**Summary of Changes and Enhancements:**

The strategic enhancements based on the NIST SP 800-53 R5 framework and Microsoft Cloud Security Benchmark focused on tightening access controls and securing data transmissions:

1.	**Private Endpoints for Key Vault and Storage Accounts**:

•	**Impact**: By creating private endpoints, data transmissions to these critical resources were confined within the Azure private network, completely isolated from public internet exposure. This change significantly reduced the attack vectors available to external actors, as it removed the possibility of intercepting or accessing the data from outside the network.

•	**Resulting Data**: This led directly to the reduction of Syslog events to zero, indicating an elimination of common network-related security incidents such as reconnaissance and unauthorized access attempts.

2.	**Restrictive NSG Rules**:

•	**Impact**: Modifying the NSG rules to deny all inbound and outbound traffic except from specific, authorized IP addresses dramatically reduced the risk profile by controlling exactly who could interact with the VMs. This measure effectively negated any unsolicited attempts to connect to the systems, which were previously possible due to the generic and open rules.

•	**Resulting Data**: This adjustment is reflected in the elimination of NSG Inbound Malicious Flows, dropping from 3,443 to zero, showcasing a complete stop of recognized malicious traffic entering the network.

3.	**Decrease in Security and Sentinel Incidents**:

•	**Impact**: The overall reduction in exposure and attack surface also reduced the operational load on security monitoring tools, resulting in fewer anomalies needing investigation and response. With tighter security controls, fewer incidents of potential breaches or suspicious activities were detected.

•	**Resulting Data**: Sentinel Incidents decreased from 239 to 36, indicating a more secure and controlled environment requiring fewer interventions.

![Sentinel Overview](https://github.com/user-attachments/assets/d2c2dd79-b9eb-4c52-b4f0-f8f1887a387e)

![Sentinel Incidents](https://github.com/user-attachments/assets/c8eda0b1-d4dd-41ce-a069-892bf9e32251)

**Comparative Analysis:**

•	**Security Events (Windows VMs)**: Drastically reduced from 64,939 to 497 events, indicating a significant decrease in detected security threats. This represents a 99.23% drop. 

•	**Syslog (Linux VMs)**: Reduced to zero, highlighting the elimination of recorded security events or incidents. This represents a 100% drop.

•	**SecurityAlert (Microsoft Defender for Cloud)**: Remained at zero, consistent with the initial data, indicating no significant security alerts generated.

•	**SecurityIncident (Sentinel Incidents)**: Decreased from 239 to 36 incidents, showing a substantial reduction in the number of security incidents logged. This represents an 84.94% drop.

•	**NSG Inbound Malicious Flows Allowed**: Reduced from 3,443 to zero, demonstrating a complete mitigation of malicious inbound traffic through stringent NSG rule enforcement. This represents a 100% drop.

![Stats](https://github.com/user-attachments/assets/130dbdbb-a3c2-4ece-b798-a26aaced08b1)

The implemented hardening measures have profoundly impacted the security landscape of the honeypot environment. The implementation of private endpoints effectively removed the exposure of critical resources to potential external threats. Meanwhile, the meticulous revision of NSG rules has nearly eliminated unauthorized network access, directly contributing to the significant reduction in security incidents and malicious flows. These actions collectively have not only closed the previously identified security gaps but also aligned the project with best practices and compliance requirements.

Post-implementation, a follow-up compliance assessment showed marked improvements in meeting the NIST SP 800-53 R5 controls related to system and communications protection. The measures specifically addressed previously identified deficiencies, resulting in a higher overall compliance score.

---

### Step 6) Conclusion

The honeypot project, meticulously conducted using Microsoft Azure’s robust virtual machine capabilities, adeptly achieved several key objectives centered around cybersecurity enhancement and vulnerability assessment. Initially designed to expose network vulnerabilities, the project employed Azure VMs in a controlled, exposed environment to gather actionable data on attack patterns and system vulnerabilities. This initial phase successfully cataloged a significant volume of security incidents, with the Windows VMs alone recording 64,939 security events, which vividly illustrated the systems’ susceptibility to external threats.

Subsequently, the project’s focus shifted towards hardening these virtual environments based on the insights gained from the initial exposure. Through targeted security measures such as the implementation of private endpoints for critical Azure resources and stringent adjustments to Network Security Group (NSG) rules, the project not only fortified the VMs but also drastically curtailed the frequency of intrusions. Post-hardening data highlighted a monumental reduction in security events—over 99% for Windows VMs and a complete eradication of Syslog events for Linux VMs, which effectively demonstrated the efficacy of the implemented hardening strategies.

Throughout the project, attack data was meticulously analyzed to discern trends and patterns, guiding subsequent enhancements in security protocols. This analytical approach was instrumental in reducing detected intrusions by a remarkable percentage, showcasing a significant improvement in the VMs’ security postures. Moreover, each phase of the project was thoroughly documented, resulting in detailed reports and presentations that not only chronicled the project’s progress and findings but also significantly enhanced organizational understanding of the potential security threats. These documents serve as a valuable resource for ongoing security strategy adjustments and for educating stakeholders on effective cybersecurity practices.

In conclusion, this honeypot project not only met but exceeded its objectives by demonstrating a profound transformation from a highly vulnerable to a securely hardened environment. It serves as a compelling example of how targeted cybersecurity measures, underpinned by a deep analysis of attack data and trends, can dramatically enhance the security of networked systems. The project’s success lays a foundation for future security initiatives and provides a replicable model for similar cybersecurity enhancements across the industry.

---
