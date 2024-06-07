# IDS-Snort-Network-Monitoring

## Objective

The objective of this project is to install and configure Snort to analyze PCAP files for potential malicious activity. The project will involve setting up Snort, using it to scan PCAP files, identifying threats, and generating basic signatures based on the detected malicious patterns. The goal is to effectively utilize Snort for network security analysis and enhance threat detection capabilities through custom signature creation.

### Skills Learned

- Software Installation and Configuration: Installing and configuring various software packages such as Snort, Hyperscan, DAQ, etc.
- Custom Rule Creation: Writing, testing, and implementing custom Snort rules for specific traffic types (e.g., ICMP)
- Network Traffic Analysis: Analyzing network traffic using Snort and interpreting generated alerts and logs.
- Troubleshooting and Problem Solving: Diagnosing and resolving issues related to software installation, configuration, and rule creation.
- Data Analysis: Analyzing Snort outputs, signatures, and PCAP files to identify potential security threats.

### Tools Used

-Snort: An open-source network intrusion detection system (NIDS) and intrusion prevention system (IPS).
- PulledPork: A script for managing Snort rule sets, automating the download and installation of rules.
- ethtool: A command-line utility for querying and controlling network device driver and hardware settings.
- pcap (Packet Capture) Files: Files containing network traffic data used for analysis.
- wget: A command-line utility for downloading files from the web.

## Steps

*Step 1*
  I began by starting my Ubuntu machine and creating a directory named "snort". Next, I installed the necessary prerequisites and updates for my system.
  
*Ref 1*
![VirtualBox_Ubuntu_01_06_2024_22_46_18](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/414fc77c-487c-4367-bcaa-4fc4b078e837)
  The second step involved installing Hyperscan, a critical component for Snort 3 due to its advanced pattern matching capabilities. Unlike Snort 2, Snort 3 leverages Hyperscan for faster regex-based pattern matching. Ref 1 shows the installation of another prerequisite, gperftools, which is necessary for the successful setup of Hyperscan.

*Ref 2*
![step 4 prereq](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/a90fb6b9-b076-40bd-8b2f-e62e8548da3b)
  This second screenshot is of the last prerequisite which is downloading the Boost C++ Libraries. The four prerequisites I had to install in order for Hyperscan to work included, Installing pcre, installing gperftools, install Ragel and lastly download but not install the Boost C++ Libraries.

*Ref 3*
![hypervisor installed](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/a0862859-9f81-4a2b-85a1-7ac79198568c)
Continuing with the setup, I successfully downloaded and installed Hyperscan.

*Ref 4*
![flatbuffers pre](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/5828efb2-4fda-448d-9976-7fe85578415d)
  In the subsequent phase, I needed to install two more prerequisites before proceeding with the Snort 3 installation. Ref 4 shows the installation of the first prerequisite, Flatbuffers.
  
*Ref 5*
![step 8 DAQ](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/d2ac58b0-33d2-46f2-89c6-d54a7ce3ba9a)
  The second prerequisite was the Data Acquisition (DAQ) library, as depicted in Ref 5, which is essential for Snort's operation.

*Ref 6*
![snort install](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/29899e78-e0db-4903-a2a8-db40baf75c13)
  After installing the prerequisites, I downloaded and installed Snort 3 using the following command: wget https://github.com/snort3/snort3/archive/refs/tags/3.2.1.0.tar.gz -O snort3-3.2.1.0.tar.gz followed by tar -xzvf snort3-3.2.1.0.tar.gz.

*Ref 7*
![verifysnort](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/d71bcc7c-6654-4478-96b5-2a4fedc4c2ef)
  In the next step, I verified that Snort was running correctly by using the -V flag with the Snort executable. The output confirmed that Snort was installed correctly and displayed the version number.

*Ref 8*
![configuration0warning](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/54ea7aa1-a691-46a0-8bbf-b301b9f57443)
  Afterward, I tested Snort using the default configuration file. The output indicated that Snort successfully validated the configuration with zero warnings.

*Ref 9*
![ipa](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/e94b0445-03c9-427d-b238-258461361edd)
  Next, I ensured that both generic and large receive offloads were disabled on my network cards, as these settings can affect packet inspection and analysis. The screenshot shows the ip a command, which displays the network adapter name needed for the next steps.

*Ref 10*
![ethtool2](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/908c5ab0-0c95-4763-af50-17d94d767020)
  I proceeded to disable the receive offload using a service to ensure it remains off after rebooting Snort. I created this service using ethtool. The screenshot shows the command input into ethtool with the correct network adapter, creating the service.

*Ref 11*
![receive-offload complete](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/4a96aa2b-350f-441f-878c-a301724c4205)
  Following this, I enabled and started the service by typing sudo systemctl enable ethtool. This screenshot shows that receive offload is disabled for both settings.

*Ref 12*
![ICMPrulecreation](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/daea6379-4110-4cfd-97f1-56af501bbaa3)
  In the following stage, I created a custom rule for Snort to detect ICMP traffic. I started by creating a file with an alert rule, configured to monitor any address and any port. Additionally, I included a custom message to be output and generated a unique signature for the rule.

*Ref 13*
![ICMPruleconfigured](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/69ff788b-b4ce-4e64-b8f5-5ffbfba03004)
  I then tested the new rule by running Snort and ensuring the rule did not generate any errors. I did this by using sudo -c to point Snort to the configuration file, followed by -R to point to the rules file. This screenshot shows that Snort successfully validated the configuration with zero warnings.

*Ref 14*
![ping](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/3bba1ca6-6921-4e43-9705-e6f4b48e4cad)
  Next, I ran Snort to listen for network traffic. I specified my network adapter in the command and configured Snort to print alerts in a concise one-line format. This screenshot shows Snort actively listening to traffic using my network adapter.

*Ref 15*
![IPSsnort](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/c82d72ac-b231-449d-852d-68bb378fa814)
  Afterward, I modified my Snort configuration to eliminate the need to manually specify the rules location in future runs. I did this by updating the Snort configuration file, navigating to the IPS section, enabling the built-in rules, and hardcoding the path to the rules.

*Ref 16*
![pullporkinstall](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/8eaefb20-a363-41cb-b4be-7ba9d8a0a207)
  The next step was to expand the rule set by downloading free rules. I achieved this by installing PulledPork, which automatically retrieves the rules. This screenshot shows the installation process.

*Ref 17*
![pullporkverify](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/79a95c8e-87d0-44ab-9be6-447ed0b1ed51)
  Continuing, I verified that PulledPork was running correctly by specifying its location and running the PulledPork Python file. This screenshot shows that there were no errors and displays the current version.

*Ref 18*
![pulledporkrules1](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/803b768a-cd45-4b4f-9b65-62ebb90c9569)
  Following this, I modified the Snort configuration file. In the screenshot, I downloaded the registered ruleset, one of three available choices. To enable this, I had to input my Oinkcode from the Snort website. I also commented out the block list path since I didn't download any block lists. Lastly, I uncommented the Snort path and the local rules path to point to my custom rules.

*Ref 19*
![rulesfromoink](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/d7c1ad0f-0324-4a63-bda1-ee6660cabaad)
  In the subsequent stage, I encountered a warning indicating that the rules archive could not be loaded due to a 422 client error. This screenshot shows the Python script where I removed the version and hardcoded the necessary file as specified by the error in the ruleset URL from the Snort registered rules.

*Ref 20*
![ruleswork2!](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/354405b8-4643-4d0b-9b17-b690aef2fadf)
  This screenshot demonstrates that PulledPork is working correctly.

*Ref 21*
![nanopullrules](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/3b15a9b8-3bb5-41d4-9ed2-4cf17cc80116)
  To ensure everything was functioning properly, I modified the Snort configuration to point to PulledPork's rules. I navigated to the IPS section and updated the local rules path to reference PulledPork's rules.

*Ref 22*
![catpullrules](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/47521d2b-5c30-416e-aefa-7445cf10f8fc)
  This screenshot shows the use of the cat command to view the rules.

*Ref 23*
![snortconfiggood!!](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/8bfb2a96-52fd-4808-9cb2-76c339874577)
  This screenshot shows Snort running without any warnings, successfully validating the configuration.

*Ref 24*
![malware downloaded](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/cc8df59e-2c3e-4ff8-acfa-f7a8b536dbee)
  In the next step, I downloaded a PCAP file from Malware Traffic using the wget command and then unzipped the file.

*Ref 25*
![ARP](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/8c662c11-6087-460c-9c0c-aa315e37ddad)
  I then ran Snort and fed it the PCAP file to see what signatures it generated.

*Ref 26*
![rareto not pcap](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/9e076076-e217-41d9-a81a-1662bdcbcc49)
  Next, I used the cut command to remove unnecessary marks and words. This screenshot shows the signatures organized from the most frequent at the top to the rarest at the bottom. The output indicated the presence of the Trojan WhisperGate, pinpointing where to look within the PCAP. 

*Ref 27*
![LASTONE](https://github.com/Casttllee/IDS-Snort-Network-Monitoring/assets/137667912/adba9b25-6e6a-4606-89d6-625e73fe937a)
  In my final step, I used grep to search for malware within the PCAP signatures, ignoring case sensitivity with the -i flag. The output revealed an IP address, which can be investigated further.

## Conclusion
  In conclusion, this project successfully demonstrated the process of installing and configuring Snort on an Ubuntu machine to detect malicious activity in network traffic. By setting up prerequisites such as Hyperscan, DAQ, and utilizing tools like PulledPork, I was able to enhance Snort's rule set and improve its detection capabilities. Custom rules were created and tested to detect ICMP traffic, and configurations were fine-tuned to ensure optimal performance. Finally, by analyzing a PCAP file, Snort was able to generate valuable signatures, including the detection of the Trojan WhisperGate, and pinpoint potential threats for further investigation. This project highlights the effectiveness of Snort as a robust intrusion detection system and provides a solid foundation for ongoing network security monitoring and threat analysis.
