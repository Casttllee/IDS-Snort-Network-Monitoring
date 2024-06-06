# IDS-Snort-Network-Monitoring

## Objective

The objective of this project is to install and configure Snort to analyze PCAP files for potential malicious activity. The project will involve setting up Snort, using it to scan PCAP files, identifying threats, and generating basic signatures based on the detected malicious patterns. The goal is to effectively utilize Snort for network security analysis and enhance threat detection capabilities through custom signature creation.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps

*Step 1*
  I first started by running my Ubuntu machine as well as making a "snort" directory. I then had to install some prerequisites and updates for my machine.
  
*Ref 1*
![VirtualBox_Ubuntu_01_06_2024_22_46_18](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/414fc77c-487c-4367-bcaa-4fc4b078e837)
  My second step was to intall hyperscan, which has some requirements for pattern matching because what is new compared to snort2. Snort3 utilizes hyper scans for fast pattern matching using regex. *Ref 1* is the second prerequisite downloaded which is installing gperftools.

*Ref 2*
![step 4 prereq](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/a90fb6b9-b076-40bd-8b2f-e62e8548da3b)
  This second screenshot is of the last prerequisite which is downloading the Boost C++ Libraries. The four prerequisites I had to install in order for Hyperscan to work included, Installing pcre, installing gperftools, install Ragel and lastly download but not install the Boost C++ Libraries.

*Ref 3*
![hypervisor installed](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/a0862859-9f81-4a2b-85a1-7ac79198568c)
  Moving forward I successful downloaded and installed Hyperscan.

*Ref 4*
![flatbuffers pre](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/5828efb2-4fda-448d-9976-7fe85578415d)
  In the following stage I had to install two more prerequisites before installing Snort3. *Ref 4* is the first prerequisite which is flatbuffers.

*Ref 5*
![step 8 DAQ](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/d2ac58b0-33d2-46f2-89c6-d54a7ce3ba9a)
  This is the second prerequisite needed for Snort which is Installing Data Acquistion (DAQ) from Snort.

*Ref 6*
![snort install](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/29899e78-e0db-4903-a2a8-db40baf75c13)
  In the following stage I downloaded and intalled Snort by using the command "wget https://github.com/snort3/snort3/archive/refs/tags/3.2.1.0.tar.gz -O snort3-3.2.1.0.tar.gz 
tar -xzvf snort3-3.2.1.0.tar.gz".

*Ref 7*
![verifysnort](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/d71bcc7c-6654-4478-96b5-2a4fedc4c2ef)
  In this next step I verified that Snort ran correctly by passing the snort executable to -V. The output also showed the version number.

*Ref 8*
![configuration0warning](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/54ea7aa1-a691-46a0-8bbf-b301b9f57443)
  Afterward I tested snort with the default configuration file. The output stated snort successfully validated the configuration with 0 warnings.

*Ref 9*
![ipa](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/e94b0445-03c9-427d-b238-258461361edd)
