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
