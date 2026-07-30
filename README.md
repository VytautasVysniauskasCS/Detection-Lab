# Detection Lab

## Objective
This project's objective was to build a home lab for practicing attack detection using a SIEM. Rather than just installing tools, I wanted to generate realistic attack activity, write my own detection logic, and document the full process from log ingestion to alert.

## What I Learned
- How a SIEM ingests, parses, and correlates logs from multiple sources
- How to read and interpret raw log data to identify suspicious activity
- Recognizing attack signatures and mapping them to known techniques
- Fundamentals of network protocols and common attack vectors
- Troubleshooting and problem-solving when detections didn't work as expected

## Tools Used

| Category | Tool |
|----------|------|
| SIEM | Splunk |
| Log Source | Sysmon |
| Network Analysis | Wireshark |
| Attack Simulation | *(e.g. Atomic Red Team)* |

## Steps
## 1) Installation

Before beginning with anything, I had to download the necessary tools to set up the detection lab. Even during the installation process, I had to make sure my computer was not at risk for malware.

## 1.1) VirtualBox

I started by downloading VirtualBox to serve as the hypervisor for the lab. After downloading, I verified the file's SHA256 hash against the value published on the official site to confirm the installer hadn't been tampered with.

<img width="1669" height="479" alt="image" src="https://github.com/user-attachments/assets/32e0ebae-7f84-4d5b-af73-740228cc70f7" />

*Fig 1: SHA256 hash comparison*

When trying to install VirtualBox, I got a warning saying that some dependencies are missing, so after looking it up on the internet. We downloaded the file "VC_redist.x64" to make sure everything in the future will work as intended.

<img width="628" height="264" alt="image" src="https://github.com/user-attachments/assets/8d03974c-538a-4d3e-958e-77b529d61063" />

*Fig 2: Dependency warning and the installed dependency*

## 1.2) Windows virtual machine

To create a Windows image, I set up my own image because it is presumed to be the safest way of setting up a windows home lab. To start, I downloaded the media creation tool from Microsoft itself and then chose to "create installation media" option. I do have to mention that this only works with a viable Microsoft windows license.

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
