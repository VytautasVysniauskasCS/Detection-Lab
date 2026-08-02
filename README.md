# Detection Lab

## Objective
This project's objective was to build a home lab for practicing attack detection using a SIEM. Rather than just installing tools, I wanted to generate realistic attack activity, write my own detection logic, and document the full process from log ingestion to alert.

## What I Learned
- How to find information online and troubleshoot unexpected scenarios and errors.
- Establishing connection between multiple virtual machines.
- 

## Tools Used

| Category | Tool |
|----------|------|
| SIEM | Splunk |
| Log Source | Sysmon |
| Network Analysis | Wireshark |
| |  |

## Steps
## 1) Installation

Before beginning with anything, I had to download the necessary tools to set up the detection lab. Even during the installation process, I had to make sure my computer was not at risk for malware.

## 1.1) VirtualBox

I started by downloading VirtualBox to serve as the hypervisor for the lab. After downloading, I verified the file's SHA256 hash against the value published on the official site to confirm the installer hadn't been tampered with.

<img width="1669" height="479" alt="image" src="https://github.com/user-attachments/assets/32e0ebae-7f84-4d5b-af73-740228cc70f7" />

*Fig 1: SHA256 hash comparison*

When trying to install VirtualBox, I got a warning saying that some dependencies are missing, so after looking it up on the internet. I downloaded the file "VC_redist.x64" to make sure everything in the future will work as intended.

<img width="628" height="264" alt="image" src="https://github.com/user-attachments/assets/8d03974c-538a-4d3e-958e-77b529d61063" />

*Fig 2: Dependency warning and the installed dependency*

## 1.2) Windows virtual machine

To create a Windows image, I set up my own image because pre-built Windows images carry a risk of being modified with malicious scripts. To start, I downloaded the media creation tool from Microsoft itself and then chose to "create installation media" option. I do have to mention that this only works with a viable Microsoft windows license.

<img width="584" height="210" alt="image" src="https://github.com/user-attachments/assets/78ba3484-c722-4d3d-a836-2935666b021f" />

*Fig 3: Windows media creation tool*

After that, we proceed to pick ISO file when asked which media to use.

<img width="605" height="219" alt="image" src="https://github.com/user-attachments/assets/3929dcc0-41df-4252-be9b-0405c3557a62" />

*Fig 4: ISO file option being chosen*

After the download finished, I finally started setting up my windows virtual machine. I first set up the name and applied the ISO image that I just downloaded.

<img width="762" height="285" alt="image" src="https://github.com/user-attachments/assets/260ebda7-0eac-44e2-9c09-bff0ec64667c" />

*Fig 5: Windows Demo virtual machine creation*

I also switched the user name and password to ones I'll have an easier time remembering. I did write them down just in case I forget.

<img width="601" height="228" alt="image" src="https://github.com/user-attachments/assets/974a1f32-a59f-4893-91b1-1031f90fe1f1" />

*Fig 6: Virtual machine user and password changes*

Because windows virtual machine is not the only virtual machine I'll be setting up. I didn't give it too much hardware usage. I decided to go with 4GBs of memory usage and 1 CPU.

<img width="608" height="158" alt="image" src="https://github.com/user-attachments/assets/a5dd49a3-1121-4a67-9daa-96fc5977cae5" />

*Fig 7: Virtual machine hardware limitations*

And lastly for the base setup, I allowed 50GBs of disk size space.

<img width="627" height="340" alt="image" src="https://github.com/user-attachments/assets/6d39204e-fc9a-49cc-b240-9e5897dc182c" />

*Fig 8: Virtual machine disk size limitations*

After finishing the setup, all I had to do was wait out the automatic installation process that was happening in the virtual machine.

<img width="1013" height="842" alt="image" src="https://github.com/user-attachments/assets/e9e27194-77d5-4037-9e7f-a1e1237d0202" />

*Fig 9: Windows installation in virtual machine*

After waiting it out, I finally had the windows virtual machine installed with nothing else so far. In order to avoid being stuck with a malware or an error in the future, I took a snapshot of this clean version that I'd be able to always come back to in case something happens.

<img width="1025" height="849" alt="image" src="https://github.com/user-attachments/assets/55c7e424-d797-4e5a-96cc-b62ff22ac145" />

*Fig 10: Windows snapshot for backup*

Now I had set up my windows virtual machine and was able to move on to install the other necessary components for the detection lab.

## 1.3) Kali virtual machine

For Kali, I used the official pre-built VM provided directly by Offensive Security, since it's maintained and verified by the Kali team themselves, this saved setup time without introducing the same trust concerns as a third-party image.

<img width="873" height="379" alt="image" src="https://github.com/user-attachments/assets/26f87183-f3b9-4ce0-a910-2db01eb5c207" />

*Fig 11: Option for a pre-built Kali virtual machine*

Because I'm using VirtualBox for my windows VM, I proceeded to download the option for VirtualBox as well to simplify management between VM's.

<img width="1279" height="340" alt="image" src="https://github.com/user-attachments/assets/1e2954df-3df8-4495-9474-0ff7b95ef725" />

*Fig 12: Different options for pre-built VM's*

When downloading the kali-linux virtualbox file, I noticed that the download ends with .7z so to avoid any unexpected errors, I proceeded to download the 7-zip file archiver.

<img width="300" height="50" alt="image" src="https://github.com/user-attachments/assets/b2874949-2cfa-4b0d-9bc3-04e2ac05b0d3" />

*Fig 13: Kali-linux file ending with .7z*

After downloading it, I quickly did the installation process and was able to proceed with kali-linux VM set up.

<img width="295" height="202" alt="image" src="https://github.com/user-attachments/assets/330986bc-529f-4a46-9a6c-f7f15b5ced22" />

*Fig 14: 7-zip installation completed*

Before setting up the VM, I noticed the credentials for Kali login were kali/kali which I wouldn't have been able to do anything if I hadn't known this. I took a screenshot of the credentials but am always able to visit the site back and look up the login credentials if needed.

<img width="396" height="26" alt="image" src="https://github.com/user-attachments/assets/622daee0-b68a-4227-9b39-22402c824ffa" />

*Fig 15: Kali login credentials*

After the kali-linux files finished downloading, I navigated to the directory it downloaded to with 7-zip file manager and proceeded to extract the files.

<img width="461" height="263" alt="image" src="https://github.com/user-attachments/assets/eac2725f-8e65-4828-8028-f5647282af0d" />

*Fig 16: Finding the kali-linux files with 7-zip*

<img width="525" height="313" alt="image" src="https://github.com/user-attachments/assets/a86ca9b2-0942-4a99-b55c-839eec682875" />

*Fig 17: Extracting kali-linux files to the same directory*

After the extraction process was complete, all I had to do was double click the .vbox file and it automatically imported the VM to VirtualBox.

<img width="612" height="94" alt="image" src="https://github.com/user-attachments/assets/c4364f05-4bd0-4ef4-a064-ba4a50d70c33" />

*Fig 18: Double clicking the .vbox file to start importing*

<img width="528" height="122" alt="image" src="https://github.com/user-attachments/assets/74026e88-d4cb-466d-827d-2d98ac9ecfba" />

*Fig 19: Kali-linux being successfully imported to VirtualBox*

I then proceeded to boot up the VM in order to ensure everything works correctly and if it does, take a clean snapshot as a potential back up for the future.

<img width="397" height="247" alt="image" src="https://github.com/user-attachments/assets/5d7e137b-9843-412e-a04f-de7ee26b9890" />

*Fig 20: Using the kali/kali login credentials*

<img width="1280" height="590" alt="image" src="https://github.com/user-attachments/assets/4dab8e76-898b-408c-9bf2-f9c4a3643334" />

*Fig 21: Kali has launched, taking the first snapshot*

## 2) Configuration

In order to ensure my host computer wouldn't be damaged or infected while analyzing and testing with malware, I first had to configure the virtual machines properly to ensure that they're properly isolated or connected specifically how intended.

Because I will be analyzing malware, I proceeded to change my network type to "internal network" which makes all the virtual machines be able to interact with one another but are completely separated from the host network aka. my computer. The option "not attached" would also be safe but it wouldn't allow for virtual machines to communicate with one another. One thing worth noting is that with either of these options selected, the virtual machines won't have access to the internet.

<img width="581" height="333" alt="image" src="https://github.com/user-attachments/assets/d83221e1-80f7-4727-94f0-b84b24ff94eb" />

*Fig 22: Different network options*

I did the same for the Kali VM but it is worth noting that the network name must match between the VM's. In this case, I named the network as "networktest".

<img width="535" height="64" alt="image" src="https://github.com/user-attachments/assets/49fd0d40-6e7b-41f6-a6bf-e3c942d8609b" />

*Fig 23: Matching network name as "networktest*

Now my two VM's were in theory connected but I still had to statically assign their IP's for both the Windows and Kali VM in order for them to properly communicate between each other.

## 2.1) Windows configuration

To start configuring the settings and assigning a static IP, I right clicked the globe icon and then opened the network & internet settings.

<img width="303" height="122" alt="image" src="https://github.com/user-attachments/assets/bafa08ef-1813-46bd-9ec0-61c4a57e73ea" />

*Fig 24: Finding network settings*

In order to find where to changed the static IP address, I had to go into "change adapter settings", then go into properties of selected ethernet and then go into properties of "internet protocol version 4". Only then was I able to change the IP address manually.

<img width="390" height="102" alt="image" src="https://github.com/user-attachments/assets/8791e738-db3f-45c8-a5d4-0e1a6e628b8d" />

*Fig 25: Finding proper settings*

<img width="365" height="410" alt="image" src="https://github.com/user-attachments/assets/400c7b60-37cc-48f1-89c5-cc9be0aa8392" />

*Fig 26: Going into properties of internet protocol version 4*

<img width="388" height="442" alt="image" src="https://github.com/user-attachments/assets/4ab6df65-5fd5-44fe-824d-5c0f1ce924f2" />

*Fig 27: Switching to "Use the following IP address option"*

Before typing in an IP address and subnet mask, I had to quickly make sure the IP address would not be conflicting with my own IP address on the host computer. I did it by opening command prompt and typing in "ipconfig". This showed me my current IP address, subnet mask and a bunch of additional information not needed as much for this project.

<img width="623" height="171" alt="image" src="https://github.com/user-attachments/assets/8fd54937-dbfd-4491-b1ab-b9f85dc2eaa1" />

*Fig 28: Finding my own IP address to make sure it doesn't overlap*

After that, I typed in the static IP address as "192.168.20.10" and subnet mask as "255.255.255.0", the other options I left as default for now as they are not needed for this stage of configuration right now.

<img width="396" height="452" alt="image" src="https://github.com/user-attachments/assets/29d0a697-9c9b-4b09-8411-04b77fcb7d20" />

*Fig 29: Switching to static IP address for consistency*

To make sure the configurations saved correctly, I opened cmd on the VM and typed in "ipconfig", as confirmation I got the exact same IP address and subnet mask which I typed in earlier.

<img width="548" height="235" alt="image" src="https://github.com/user-attachments/assets/e075b28f-4c6e-4ae8-8a76-b139e8a9730c" />

*Fig 30: Confirming settings were changed correctly*

To have a reliable backup, I took another snapshot in case it's needed to go back to this state.

<img width="513" height="346" alt="image" src="https://github.com/user-attachments/assets/2f0a7926-54b8-4995-af34-126e2425110f" />

*Fig 31: Creating the 2nd snapshot*

## 2.2) Kali configurations

Now I had to do the exact same thing on Kali, though Kali is Linux based so it was a bit different.

To find the network connections in Kali, I right clicked the loading symbol at the top and went into "edit connections". I then selected the wired connection and pressed the gear button at the bottom.

<img width="373" height="244" alt="image" src="https://github.com/user-attachments/assets/a36e76db-d078-4d7f-907e-943d45f16fad" />

*Fig 32: Finding network settings for Kali*

<img width="609" height="425" alt="image" src="https://github.com/user-attachments/assets/a2b5c65e-2730-41c2-a248-9c0eecb4c125" />

*Fig 33: Going deeper into network connections*

After I selected IPv4 settings, I switched the mode to "manual" so that I could type in the IP address the same way as in Windows VM.

<img width="698" height="215" alt="image" src="https://github.com/user-attachments/assets/cc81aa4a-2714-4e1d-bc7a-998e0b951830" />

*Fig 34: Selecting the manual mode*

I then pressed the "add" button on the right and typed in the IP address of 192.168.20.11 which is almost the same as Windows one, just as x.x.x.11 instead of x.x.x.10 so that they don't clash with one another. For netmask I wrote 24 which is the same as 255.255.255.0 which was the subnet mask in Windows VM. The other configurations I left as default for now because they're not needed to modify.

<img width="693" height="540" alt="image" src="https://github.com/user-attachments/assets/d8ae4a2e-7b1d-45ff-9472-4879188fdc38" />

*Fig 35: Selecting the manual mode*

When I went to check the IP address in the terminal screen, I actually got an error and had my first problem to troubleshoot, instead of seeing the IPv4 address, it never showed and instead only showed IPv6 like IPv4 was not configured at all.

<img width="665" height="426" alt="image" src="https://github.com/user-attachments/assets/1047cafc-0d92-45b5-9763-dbd9ffcd7a39" />

*Fig 36: Inet information not showing, only inet6 showing*

What bugged me was the loading circle when navigating to network settings so I reloaded the VM and the icon was not loading anymore which made the confirmation work as intended.

<img width="248" height="61" alt="image" src="https://github.com/user-attachments/assets/c6c6d3fc-81aa-41b7-83ab-71dab5666e25" />

*Fig 37: Network settings option not being a loading circle anymore*

<img width="612" height="81" alt="image" src="https://github.com/user-attachments/assets/6cd2c095-ec88-4f08-8ffa-5d0342250514" />

*Fig 38: The IP address and netmask being shown exactly as configured*

The final confirmation I needed now was a successful connection between the two VMs but because of Windows firewall that would block unregistered ICMP traffic, I had to switch to Windows VM to test the connection.
Before that I took a snapshot of configured Kali VM.

<img width="422" height="182" alt="image" src="https://github.com/user-attachments/assets/6cbabb86-9b5d-422a-a8c2-2c5a3ff3d786" />

*Fig 39: Taking a second snapshot of Kali VM as backup*

The first time I tried to test the connection between the two VMs I actually got no response but I instantly figured out that the problem was me shutting down the Kali VM when trying to connect the two.

<img width="533" height="221" alt="image" src="https://github.com/user-attachments/assets/9e1bf40e-d1c8-4e8f-b313-c25cd2809da9" />

*Fig 40: No response when trying to ping Kali VM*

The second time I tried pinging the IP address of Kali VM, I instantly got a response which confirmed an existing connection between the VMs.

<img width="485" height="234" alt="image" src="https://github.com/user-attachments/assets/b612700f-84e2-4d68-ba85-0ebfc0d7eb5c" />

*Fig 41: Ping response from Kali VM, proving connectivity*

## 3) Splunk set up

I could've done this step as soon as I set up windows VM but I wanted to make sure there's an active connection between the Windows and Kali VMs. Now that I confirmed that there is a connection, I proceeded to both install and set up Splunk as my monitoring tool for the future malware analysis.

I immediately ran into a big problem because of this decision. Splunk needs to be downloaded on the internet and because I'm using internal network settings for my VMs, I have no access to the internet so I really had 2 options to choose from.

1) Switch to NAT network type, install the necessary tools and then redo the steps in internal network settings.
2) Try the shared folders feature and send the installation file of Splunk to the Windows VM.

Because I never used the shared folder feature before and redoing everything wouldn't be as informative. I decided to try my luck on the shared folder feature.

To start off, I had to go on the Windows VM, click on devices at the top, shared folders and shared folder settings.

<img width="496" height="184" alt="image" src="https://github.com/user-attachments/assets/4341edf5-abd1-4576-9c2f-f4c9f49006ff" />

*Fig 42: Shared folder settings navigation*

I then clicked "Machine Folders" and pressed the add shared folder button on the right which opened up my host file explorer and made me navigate to a folder that would be the shared folder. I created a new one on the C drive and called it "shared_folder". I applied Auto-Mount and made it machine-permanent so that it wouldn't be deleted after I restart the VM.

<img width="543" height="304" alt="image" src="https://github.com/user-attachments/assets/f8b8505b-f817-4f23-be6f-1897ddff7fba" />

*Fig 43: Creating a shared folder*

Surprisingly or not, I didn't see the shared folder I created on the VM which was supposed to be next to local disk but nothing was found there.

<img width="560" height="159" alt="image" src="https://github.com/user-attachments/assets/eb507358-05e7-4c5d-babe-c8e727829b96" />

*Fig 44: No "shared_folder" seen on the VM*

I then read on the internet that in order for shared folders feature to work, I needed to install guest additions on the VM. You can already see the guest additions next to the local disk but I had yet tried to navigate or install them. They appeared after I clicked on devices again and then clicked "Insert Guest Additions CD Image..."

<img width="266" height="266" alt="image" src="https://github.com/user-attachments/assets/12a93a2d-f6ff-4892-bae9-9541801b1b55" />

*Fig 45: Inserting guest additions cd image*

After figuring out the process on how to install them on the internet, I tried the same on my own VM. First I started the installation of additions by starting the "VBoxWindowsAdditions" installer.

<img width="614" height="65" alt="image" src="https://github.com/user-attachments/assets/bd0d1ed0-6dc5-49e2-97ac-ef5563bfceb3" />

*Fig 46: Starting the installer for the 64 bit machine*

After finishing the installation, a reboot was required for the VM at the end.

<img width="493" height="386" alt="image" src="https://github.com/user-attachments/assets/0b009a8b-a943-4114-870f-31c3caa4f3be" />

*Fig 47: Required reboot after install*

During the reboot, I encountered my first VM crash which made me restart the reboot process hoping everything will be working as intended.

<img width="566" height="469" alt="image" src="https://github.com/user-attachments/assets/80172a7f-bc13-40b4-b08e-ec5407f7970d" />

*Fig 48: Windows VM loading screen stuck during reboot*

After restarting the VM a second time and checking the file explorer, I saw that the shared folder disk now appears and is working as intended. I was able to proceed in actually installing Splunk now.

<img width="540" height="178" alt="image" src="https://github.com/user-attachments/assets/763e158c-65ca-4075-b91e-ec88fb4865ac" />

*Fig 49: Shared folder now working as intended*

On the host computer, I navigated to the Splunk website to download Splunk Enterprise free trial version.

<img width="568" height="376" alt="image" src="https://github.com/user-attachments/assets/a8c06d63-0dea-4ea5-be07-c8ba65a03369" />

*Fig 50: Splunk Enterprise free trial*

To start the free trial and begin downloading, I had to create an account and write some pretty private credentials that I won't share in this documentary but after creating an account and verifying via email, I was able to begin the installation file.

<img width="1211" height="213" alt="image" src="https://github.com/user-attachments/assets/9d987518-95e5-4c11-8361-e7d816724bf4" />

*Fig 51: Different install packages for different operating systems*

After downloading the .msi file, I put it in the shared folder that I created and see it successfully transfer to my Windows VM.

<img width="1504" height="339" alt="image" src="https://github.com/user-attachments/assets/2cb72a25-2f32-44de-9283-a19131f3f29a" />

*Fig 52: Different install packages for different operating systems*

With the troubleshooting process being finally done for now, I was able to begin installing and setting up Splunk on my Windows VM.

To begin the install process, I first had to agree with their license agreement.

<img width="521" height="405" alt="image" src="https://github.com/user-attachments/assets/2c3b3c85-6bf2-4b4e-a273-578ef2a0a952" />

*Fig 53: A need to agree with license agreement before starting install process*

Then I had to set up my login credentials, I will be using credentials that I personally know very well and should not forget in the near future.

<img width="494" height="381" alt="image" src="https://github.com/user-attachments/assets/5714cd22-f051-4f7b-9b74-cab3ea9f70f8" />

*Fig 54: Requirement to set up login credentials*

After filling them out, starting the install process and waiting it out, I was able to launch Splunk Enterprise on my own Windows VM.

<img width="525" height="395" alt="image" src="https://github.com/user-attachments/assets/ad5fd6d9-333a-480f-b4fa-a979a8f7c070" />

*Fig 55: Installation for Splunk Enterprise complete*

After launching Splunk on my localhost, the final step I had to do was fill in the credentials I wrote in before starting the installation process.

<img width="612" height="233" alt="image" src="https://github.com/user-attachments/assets/dbcdd7ef-1881-4593-b191-604c248a987d" />

*Fig 56: Log in credentials requirement for Splunk Enterprise*

Once I logged in to my account, I finally had full access to Splunk on the Windows VM.

<img width="1820" height="928" alt="image" src="https://github.com/user-attachments/assets/bca7bce5-6b6c-4cb9-888e-311c6b5c2959" />

*Fig 57: Splunk successfully launched on Windows VM*

To test out if it actually works, I decided to try add data and monitor the system. To do that I first pressed "Add Data" and then "Monitor" option.

<img width="983" height="297" alt="image" src="https://github.com/user-attachments/assets/e074fd2a-755b-4bce-840d-ec73f234eebf" />

*Fig 58: Adding monitoring data to test Splunk*

I chose to monitor local event logs and from them I picked system, security and applications.

<img width="1089" height="355" alt="image" src="https://github.com/user-attachments/assets/3c5bc40c-2cdf-4b18-9735-a81a92a1a112" />

*Fig 59: Choosing what things to monitor*

Once I chose the index as main and pressed next a couple more times, I was able to begin searching and monitor the logs.

<img width="848" height="459" alt="image" src="https://github.com/user-attachments/assets/5ca0d492-7f37-48da-98b6-6c4f9f5d3100" />

*Fig 60: Choosing index as main*

<img width="632" height="316" alt="image" src="https://github.com/user-attachments/assets/07103942-f320-496d-af44-e986a859a5ae" />

*Fig 61: Monitoring logs successfully selected*

After starting the search, I was able to finally look at the logs Splunk was showing me while monitoring the system and was able to confirm it's working on the VM system.

<img width="1756" height="797" alt="image" src="https://github.com/user-attachments/assets/f1347f62-4e90-41eb-9cc9-082545618b41" />

*Fig 62: Logs generated and confirming Splunk is working*

Because I made a ton of progress that I was scared to lose due to some error, I instantly took another snapshot after confirming Splunk has been installed and is working properly on the machine.

<img width="351" height="183" alt="image" src="https://github.com/user-attachments/assets/d00bfe38-8166-40f1-98ea-c06f7120152f" />

*Fig 63: Taking the 3rd snapshot after Splunk installation*

## 4) Sysmon Setup

Due to running into the same problem of Sysmon requiring internet to install, I decided to take use of the shared folder feature again to complete the Sysmon installation on Windows VM.

To download Sysmon, which is a free Microsoft tool for monitoring, I visited their website and downloaded the version for Windows because I'll be running it on Windows VM.

<img width="367" height="302" alt="image" src="https://github.com/user-attachments/assets/20c82eaf-d7e7-45a2-86d4-bb7a4bf65689" />

*Fig 64: Where to download Sysmon*

In order to avoid unnecessary noise when monitoring, I also downloaded a configuration file that will funnel out the noise I won't be needing.

For the config file, I used one that's on this github page of github.com/olafhartong/sysmon-modular/tree/master and then found the file sysmonconfig.xml which I proceeded to open, then pressed raw and right clicked anywhere to save as sysmonconf.xml but realistically you can save it as whatever you want, you just need to make sure it ends in ".xml".

<img width="927" height="50" alt="image" src="https://github.com/user-attachments/assets/7ce01d24-c491-413b-a11b-8dfdac616e89" />

*Fig 65: Finding the config file*

<img width="280" height="56" alt="image" src="https://github.com/user-attachments/assets/dbe301c4-a449-4d8e-8c95-fe3c5e25ac8f" />

*Fig 66: Pressing the "raw" button at the top right of the screen*

<img width="204" height="67" alt="image" src="https://github.com/user-attachments/assets/20d7b9fe-444f-43ab-9ccb-875a865be57f" />

*Fig 67: Saving as the file "sysmoncomf.xml"*

Before I put in the downloaded files into the shared folder for the VM, I extracted the zip when downloading Sysmon itself. Only then did I put in the files into the shared folder and received them on the VM.

<img width="544" height="279" alt="image" src="https://github.com/user-attachments/assets/0de87824-3e13-46a0-a54f-e4b9fa75c03d" />

*Fig 68: Extracting Sysmon.zip*

<img width="1266" height="324" alt="image" src="https://github.com/user-attachments/assets/eceb8b29-51db-4722-a7db-d5bd0a7c7b9e" />

*Fig 69: Transferring the files to the VM via shared folder feature*

For my own sake, I moved the files to the download folder because I didn't know the possibilities of doing the installation process in the shared folder and didn't want to risk anything. 

For the installation process, instead of just starting the executable file, I booted up PowerShell with admin privileges to install it properly because in short, system kernel and driver that requires such type of installation to make sure it works as intended.

<img width="774" height="279" alt="image" src="https://github.com/user-attachments/assets/ef49242f-4232-466b-b343-0a27ece32af2" />

*Fig 70: Starting up PowerShell with administrative privileges*

After that I needed to go the directory where the Sysmon files are at and for that I simply copied the directory from file explorer and pasted it in after writing "cd" into the PowerShell command line. 

<img width="675" height="163" alt="image" src="https://github.com/user-attachments/assets/1c8d7293-d124-498f-b3ad-de0112c898a6" />

*Fig 71: Copying the directory path to Sysmon files*

<img width="417" height="41" alt="image" src="https://github.com/user-attachments/assets/cf7bb959-ebf5-45a7-bf3a-e991f9ab9c3f" />

*Fig 72: Getting to the directory in PowerShell with cd command*

Before continuing with anything, I had to move the configuration file to the same directory as all the other files.

<img width="679" height="208" alt="image" src="https://github.com/user-attachments/assets/3c213451-a3aa-4b3e-ae6e-e3a02b6d368c" />

*Fig 73: Moving the sysmonconf file to the Sysmon directory*

After that, I was finally able to begin installing. There were a few different exe files but because I'm using a Windows VM for 64 bits, I needed to start Sysmon64 which I just wrote in the PowerShell command line and pressed tab to autofill.

<img width="366" height="19" alt="image" src="https://github.com/user-attachments/assets/b45e3895-7fa2-42a9-8800-cbb0eda83618" />

*Fig 74: Writing the command in to install Sysmon via PowerShell*

After I pressed enter, I got showed a lot of information that neither confirmed or not that Sysmon installed correctly so I had to confirm myself. For that I opened up Services menu via Windows search future and tried to find the Sysmon service.

<img width="834" height="583" alt="image" src="https://github.com/user-attachments/assets/994e8c97-03fd-40e3-a245-18653673900c" />

*Fig 75: Information for how to install Sysmon without confirming anything*

<img width="359" height="597" alt="image" src="https://github.com/user-attachments/assets/681ee738-cb41-46ce-a88c-87ff4fc83514" />

*Fig 76: Opening up Services page via Windows search tool*

Because services are sorted in an alphabetical manner, I searched all services starting with an "S" and scrolled until I found other similar service names. However, Sysmon was nowhere to be seen so I was able to confirm that it didn't install on the VM yet.

<img width="204" height="135" alt="image" src="https://github.com/user-attachments/assets/6b260995-63da-4e9b-9bfb-be29007b2237" />

*Fig 77: Confirming that Sysmon is not in services tab and didn't install yet*

After finding information online and reading the help command that appeared after I tried installing Sysmon, I tried again the same command but this time adding -i ./sysmonconf.xml which basically adds on the config file that I downloaded earlier to the Sysmon installation.

<img width="506" height="31" alt="image" src="https://github.com/user-attachments/assets/5b734609-3e01-4067-972b-b0aaabaf7f82" />

*Fig 78: Updated command line for Sysmon installation*

After pressing enter to start the command, I got a pop up with license agreement asking if I accept and after pressing accept it seemingly started the installation process.

<img width="462" height="320" alt="image" src="https://github.com/user-attachments/assets/8d0fe59a-7e8b-451c-8a1b-0bae799bf497" />

*Fig 79: License agreement pop up after entering the installation command*

<img width="618" height="269" alt="image" src="https://github.com/user-attachments/assets/6e2839d5-19da-42e6-b287-f0910b7ed0c6" />

*Fig 80: Presumably Sysmon being installed on the VM*

Finally, I still had to confirm if Sysmon actually installed and for that I used the exact same trick as before.

After clicking the refresh button at the top left of the services window, I was able to see Sysmon64 appear which confirmed it has installed properly on the Windows VM.

<img width="419" height="47" alt="image" src="https://github.com/user-attachments/assets/f66e9962-3b12-4895-9feb-d81a8a06a880" />

*Fig 81: Sysmon64 appearing on the services page and confirming the installation*

Without touching anything else, I took another snapshot for installing Sysmon and closed the Windows VM for now.

<img width="328" height="157" alt="image" src="https://github.com/user-attachments/assets/b4d9a828-7ab0-4664-8707-5841fddb162d" />

*Fig 82: Taking the 4th snapshot for Sysmon installation*

## 5) Extra Modifications

Before starting with malware setup, I wanted to do 3 things before that:

1) Increase the available RAM and CPU cores usage in the Windows VM from 4GB and 1 core to 8GB and 2 cores because the VM was working noticeably slow and it bothered me a bit.
2) Enable Sysmon on Splunk for malware analysis.
3) Disable shared folder function.

### 5.1) Increasing Windows VM System Usage

This was by far the easiest thing to do but I still couldn't ignore it without doing it. All I had to do was go into VirtualBox, select the Windows VM, go into settings and in the system category change base memory and number of CPUs to whatever I wanted. In this case it was 8GB of RAM and 2 CPU cores

<img width="545" height="114" alt="image" src="https://github.com/user-attachments/assets/bfeb8887-36dc-44db-a976-b019584968dc" />

*Fig 83: Changing available RAM usage*

<img width="560" height="169" alt="image" src="https://github.com/user-attachments/assets/b8e8a5a5-2ed6-4f2e-b235-3aa97ad832f8" />

*Fig 84: Changing available CPU cores usage*

### 5.2) Enabling Sysmon on Splunk

For this I had to actually start the Windows VM. Instantly it felt like the VM was running a lot better.

To enter Splunk, I had to open up my web browser, in this Microsoft Edge, and then enter localhost via typing localhost:8000 in the search engine. After that I had to login but my login credentials were already saved so all I had to do was press the login button.

<img width="1266" height="662" alt="image" src="https://github.com/user-attachments/assets/6bb25b92-abd9-4db0-99e3-4f2810e222d6" />

*Fig 85: Entering Splunk*

Before installing Sysmon to Splunk I actually had to close the VM and align even more RAM and CPU cores to the VM because Splunk was loading ridiculously slow. I'm not gonna show the screenshots again but I changed the available RAM from 8GB to 12GB and CPU cores from 2 to 6.

To get Sysmon on Splunk, I had to press "Find more apps" and then find "Splunk Add-on for Sysmon". This was the sentence I would've said and nothing more if everything went according to plan, but unknown to me, which should've been pretty obvious actually, I needed internet access if I wanted to find other apps to install. On the VM I was stuck on this loading screen thinking it was just Splunk loading too slow but in reality it was the issue that I had no internet access in a place where I needed internet.

<img width="1133" height="310" alt="image" src="https://github.com/user-attachments/assets/d76bbb8d-d8bd-4a33-869c-dbd67b1dcdce" />

*Fig 86: Not finding any apps due to no internet access from internal network on the VM*

I still decided to keep the extra resources I allocated on the Windows VM because it made navigating Splunk and other things easier and faster on the VM. Now I had to find a way to install the add-on on the VM with no internet access and decided to try my luck with the shared folder function once again.

I started off with logging into Splunkbase with my account to try and find the add-on I was looking for.

<img width="527" height="408" alt="image" src="https://github.com/user-attachments/assets/de2f15f3-5d68-4b9d-8d9a-d308970c70f7" />

*Fig 87: Login to my Splunk account*

After entering Splunkbase, the place to download extra applications for Splunk, I searched for Sysmon and quickly found what I was looking for.

<img width="539" height="397" alt="image" src="https://github.com/user-attachments/assets/ef3e5de2-7b76-4fc3-86c9-e543c1cd6a32" />

*Fig 88: Finding "Sysmon Add-on for Splunk"*

After finding it, it was a simple process of me just pressing the download button and agreeing with their license rules.

<img width="928" height="337" alt="image" src="https://github.com/user-attachments/assets/207bb4e6-2abe-4650-92c4-9429683bbe3c" />

*Fig 89: Downloading the add-on*

I once again transferred the file to shared_folder folder so that I could access it in the VM.

<img width="1194" height="453" alt="image" src="https://github.com/user-attachments/assets/8e0ac8ba-4f73-4657-9a59-27d0d1d03e7b" />

*Fig 90: Saving myself with the share folder function once again*

I moved the file to my download folder to make life easier and then got back into Splunk on the VM to go to "Manage apps" section and pressed on the button "Install App From File" to do exactly what it says.

<img width="486" height="117" alt="image" src="https://github.com/user-attachments/assets/a281dca2-e847-45fd-97fb-06624e41f049" />

*Fig 91: The option to install the add-on from a file*

I then simply dragged and dropped the file to the shown section and pressed "upload" to successfully install the add-on for Sysmon.

<img width="699" height="330" alt="image" src="https://github.com/user-attachments/assets/4e01aab6-d383-4985-a4b3-cd9e982dea14" />

*Fig 92: Uploading the file*

<img width="450" height="234" alt="image" src="https://github.com/user-attachments/assets/96652f97-cd7f-4ce6-b0af-d9b8b6a0b76d" />

*Fig 93: Confirmation for the successful installation*

Needless to say, I didn't hesitate to take another snapshot after the installation was complete. For now I believe to have finally been done with installation troubleshooting.

<img width="395" height="165" alt="image" src="https://github.com/user-attachments/assets/69c977fb-35eb-4d01-92ba-c004495107d2" />

*Fig 94: Taking 5th snapshot for Sysmon add-on installation*

### 5.3) Shared Folder Removal

Though I will not be installing any dangerous malware for now, it is still good practice to remove any possible connection from the VMs to my host machine. Believing to not need the shared folder feature for now anymore, I simply removed the folder I created via VirtualBox settings for the Windows VM.

<img width="706" height="79" alt="image" src="https://github.com/user-attachments/assets/6b2bc595-cbd2-46c4-b44c-7057639c230c" />

*Fig 95: Removal of the Windows VM shared_folder*

It is worth noting that I didn't actually delete the folder, I just removed access to it from the VM. If I will need in the future, the folder with it's contents is still on my host machine.

<img width="666" height="323" alt="image" src="https://github.com/user-attachments/assets/4e741f5f-9ce4-4148-b9e4-48c22333e41e" />

*Fig 96: Continued existence of the "shared_folder" on my host machine*

## 6) Malware Creation

After being done with quite a bit of setting up and troubleshooting, I was finally able to move on to the more interesting stuff. For a while I can be done with Windows and move onto Kali on Linux so first thing first of course, I booted up Kali VM.

After logging in with Kali login credentials from the setup, I first created a new file, checked my IP address with ifconfig and pasted it in the new file that I just created because I'll be needing it later for malware setup and I'd rather not trust my memory to get retype the IP address. It is definitely not a necessary step to take but I wanted to do it to avoid obvious attention mistakes that could cost me extra time later.

<img width="413" height="229" alt="image" src="https://github.com/user-attachments/assets/8b84ad07-328e-46c7-8301-9f32bf08e302" />

*Fig 97: Empty file creation to store the IP address*

<img width="599" height="77" alt="image" src="https://github.com/user-attachments/assets/09b44242-40e2-4e86-b842-222134a69f0f" />

*Fig 98: Finding the IP address of the VM*

<img width="429" height="222" alt="image" src="https://github.com/user-attachments/assets/01d43453-086b-40db-bdcd-580efa48152d" />

*Fig 99: Saving the IP address in the empty file*

Now on the terminal I ran the command "nmap -A 192.168.20.10 -Pn". It's an aggressive scan that targets my Windows VM and identifies open ports with their specifications. It's also able to bypass firewalls ping block which is the main reason we're using it.

And then I proceeded to get nothing! The scan showed nothing, everything ignored seemingly like firewall did actually block the scan. I scouted the internet and figured out that this command does indeed work with firewall enabled but I had to enable remote desktop first.

<img width="639" height="350" alt="image" src="https://github.com/user-attachments/assets/8659b578-bbb9-40ad-89a7-4b0878ab4d15" />

*Fig 100: Finding nothing with the nmap scan*

To enable remote desktop, I closed the Windows VM, went into settings, display and simply pressed the enable button. I didn't change anything else as it was not necessary.

<img width="591" height="259" alt="image" src="https://github.com/user-attachments/assets/dbaffae9-c83d-4dac-bc5c-78580a23cfea" />

*Fig 101: Enabling remote desktop for Windows VM*

After Windows VM booted up again, I was able to try again but before that I wanted to elaborate on the command line I'm using. After typing nmap -h it shows all the scan types I could do and I'm using -A because it gives general information without overcomplicating anything. Different scans may work better but so far I am not knowledgeable on the subject enough. -Pn is there to skip the initial ping and go straight into scanning.

<img width="609" height="33" alt="image" src="https://github.com/user-attachments/assets/d7c79f72-b866-4ed8-9722-330bc50d82e2" />

*Fig 102: Explanation of nmap -A usage*

With all that out of the way I was able to retry the command line again and see if anything shows up this time without needing to modify Windows VM firewall.

<img width="549" height="89" alt="image" src="https://github.com/user-attachments/assets/b6bad407-4364-4fd3-94bf-c06554973483" />

*Fig 103: Retrying the scan*

Complete nothing again, I did a bit more research and realized I probably should've turned on remote desktop on the VM itself instead of VirtualBox settings.

<img width="651" height="333" alt="image" src="https://github.com/user-attachments/assets/e39e2dc0-88b3-4060-ab84-cf742328d80b" />

*Fig 104: No luck in 2nd attempt at the scan*

A problem with that I encountered was that I couldn't just enable remote desktop as simply because it said my home edition Windows 10 didn't support it and I had to upgrade it in order to enable remote desktop.

<img width="603" height="335" alt="image" src="https://github.com/user-attachments/assets/cfb72e59-770f-4416-9dce-794cddf71bc0" />

*Fig 105: Unable to enable remote desktop function*

I then did some digging and found a public generic Windows 10 pro key that hopefully would work of "VK7JG-NPHTM-C97JM-9MPGT-3V66T". I then typed it in and the product key actually worked.

<img width="687" height="338" alt="image" src="https://github.com/user-attachments/assets/a06bf582-17e9-4976-b2b3-1b4c1d55ad1d" />

*Fig 106: Product key being correct*

I then pressed start and had to wait a bit for it to finish updating, it then restarted my VM on it's own. Once the restart was done, I checked the settings and indeed, I was able to enable remote desktop but before that, I shut down the VM and disabled remote desktop display on the VirutalBox settings from the previous misunderstanding.

<img width="569" height="240" alt="image" src="https://github.com/user-attachments/assets/052b9274-1735-4bb4-b07d-064a350de642" />

*Fig 107: Remote desktop function available to turn on now*

After turning off the remote display setting and booting up Windows VM again. I enabled remote desktop on the VM and proceeded to try the nmap command line on Kali once more.

<img width="534" height="82" alt="image" src="https://github.com/user-attachments/assets/52c21bfc-29cf-4bcf-986e-38c57d1de462" />

*Fig 108: 3rd attempt at Kali nmap scan*

As everyone says, 3rd time's the charm as I finally struck gold. The scan was successful and it showed that port 3389 was open.

<img width="661" height="587" alt="image" src="https://github.com/user-attachments/assets/c43f936f-921f-483b-a7e9-633016e8a42b" />

*Fig 109: 3rd attempt at Kali nmap scan succesfull and port 3389 open*

Now I finally had the time to craft my own malware. First thing first I typed in "msfvenom" to see all the available options with it. The screenshot failed to show all the general options msfvenom provides but it gives an accurate idea of what it's able to do.

<img width="656" height="586" alt="image" src="https://github.com/user-attachments/assets/7d51f743-efc1-4c6f-8da3-57b705b14d98" />

*Fig 110: Possible options with msfvenom*

To build my msfvenom malware I first had to pick a payload to use and I was able to see the list of payloads by typing "msfvenom -l payloads". I am also not to knowledgeable with msfvenom and all the different available payloads because there's just so many of them but I'll be using meterpreter reverse shell payload or more accurately "windows/x64/meterpreter_reverse_tcp"

<img width="1000" height="488" alt="image" src="https://github.com/user-attachments/assets/19646f96-6007-4363-91a2-d2164c3828a2" />

*Fig 111: Finding the payload I'll be using for msfvenom*

Now that I had the payload I'll be using, I was finally able to start building my malware. The command I had to enter required the attackers IP address which is the reason I saved my IP from before. For the port I put in 4444 because it's the default meterpreter port but it didn't matter too much. The -f exe means it's gonna be an executable and -o means that I named it "VytautoCV.pdf.exe" 

<img width="886" height="52" alt="image" src="https://github.com/user-attachments/assets/ab4af4ad-7750-4e9b-8e5c-bb4b91610429" />

*Fig 112: Typing in the command for msfvenom malware creation*

After running the command, I was able to see it successfully created on my desktop.

<img width="487" height="268" alt="image" src="https://github.com/user-attachments/assets/930b7ea8-6dec-4fb2-9c1f-8467852a7361" />

*Fig 113: VytautoCV.pdf.exe malware successfully created*

Now that I had set up my malware, I had to open up a Handler that would listen in on the port that I configured to in the malware. For that to be done I had to open up Metasploit by typing in "msfconsole".

<img width="553" height="571" alt="image" src="https://github.com/user-attachments/assets/81e9e9d3-aa5b-44c6-826b-5e2494a55cae" />

*Fig 114: Opening up Metasploit*

To continue, I had to use multi-handler to enter the exploit itself and for that I had to type in another command.

<img width="438" height="74" alt="image" src="https://github.com/user-attachments/assets/19ff5d72-c432-4202-954a-d39bdcb52f0d" />

*Fig 115: Typing in the command to use multi-handler*

Now when I typed in "options" and pressed enter I was able to see a bunch of different information about the malware but the main thing was that the payload information showed I was still using generic payload so I needed to change that.

<img width="706" height="341" alt="image" src="https://github.com/user-attachments/assets/3e57e2f0-d60a-4da9-a676-bb81e41f8f0b" />

*Fig 116: Malware information*

After typing in a command that changed the payload to the one I chose to be using and typing options again, I was able to see that the payload in use is the correct on this time.

<img width="795" height="402" alt="image" src="https://github.com/user-attachments/assets/93f3b178-331b-4982-bbc6-d34dcb727a4d" />

*Fig 117: Successfully changing the payload in use*

The only thing I still had missing was that the LHOST was not set so the listened information had nowhere to go, to change that I typed in a command to set my Kali VM IP address as the LHOST and saw that it has successfully set the LHOST address.

<img width="781" height="392" alt="image" src="https://github.com/user-attachments/assets/47a4cb90-0aa9-4ac2-9424-d78aaf0a89f8" />

*Fig 118: LHOST address and everything else in place*

With everything set up, I was able to start the handler by typing in "exploit" which started the listening in process.

<img width="461" height="84" alt="image" src="https://github.com/user-attachments/assets/db94c8b7-0032-4722-8c10-35a9ac08bc43" />

*Fig 119: Listening in malware successfully started*

Now that I had malware set up and actively waiting, I only needed a HTTP server for the malware to be downloaded on the victims machine. To do this I decided to use python and in a different terminal tab, I checked if I'm in the directory as the malware, deleted the file that contained the IP address because it's not needed anymore and created a HTTP server in port 6767 which can just be any port not in use.

<img width="536" height="345" alt="image" src="https://github.com/user-attachments/assets/527f0145-d57c-4074-8a3f-927f51c789f1" />

*Fig 120: Opened up a port with the malware inside*

After doing all that, the Windows VM should be able to access my Kali VM and download the malware like that but of course, that is all in theory only and I need to check if it actually works or not.

Before that even if I won't be closing the Kali VM, I still took a snapshot to always come back to this state as I should not be needing to touch Kali VM for a while.

Funny enough, after I took the snapshot, I immediately noticed that instead of the port being 6767, I wrote in 67677 which made it actually be 2141 due to overflowing. I quickly rewrote the command correctly and took another snapshot saving my progress.

<img width="549" height="477" alt="image" src="https://github.com/user-attachments/assets/92b47ef0-c4a1-48de-b80b-efbc2a531eda" />

*Fig 121: CORRECTLY Opened up a port with the malware inside*

<img width="455" height="194" alt="image" src="https://github.com/user-attachments/assets/06872945-b45a-43da-b072-10ed3a55db92" />

*Fig 122: 4th snapshot saved to have a backup if it's needed*

And so with that, everything is done on the Kali machine for now and I was able to put my full focus on the Windows VM.
