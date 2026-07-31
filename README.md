# Detection Lab

## Objective
This project's objective was to build a home lab for practicing attack detection using a SIEM. Rather than just installing tools, I wanted to generate realistic attack activity, write my own detection logic, and document the full process from log ingestion to alert.

## What I Learned
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

