<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines using Wireshark</h1>
In this tutorial, we will observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group
- Create a Virtual Machine
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>
</br>
</br>
<h3 align="center">
  Set up your virtual environment
</h3>
</br>
<p>
  First, let's create our Resource Group inside our Azure subscription.
</p>
<p>
  <img src="https://github.com/user-attachments/assets/3d17cd82-b31c-4b9d-9e08-05ee65ddcdc2" height="75%" width="100%" alt="Resource Group"/>
  <img src="https://github.com/user-attachments/assets/fdedd732-4916-4337-9b46-75ccda0d3dbc" height="75%" width="100%" alt="Resource Group"/>
</p>
<p>
  Now create your Windows virtual machine. I typically create the VM in (US) East US.
</p>
<p>
  While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Make sure to use the password option under the <strong>Administrator Account</strong> section:
</p>
<p>
  <img src="https://github.com/user-attachments/assets/74656655-67c2-4b3e-ad69-f63dc5fc55a6" height="75%" width="100%" alt="Windows VM"/>
  <img src="https://github.com/user-attachments/assets/e0bd7cc5-0432-4629-ae24-e4d57ff933c8" height="75%" width="100%" alt="Windows VM"/>
  <img src="https://github.com/user-attachments/assets/bdf5f1c3-933a-4d8e-b580-6fea695a2942" height="75%" width="100%" alt="Windows VM"/>
</p>
<p>
  Create an Ubuntu virtual machine.
</p>
<p>
  While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Make sure to use the password option under the <strong>Administrator Account</strong> section (not seen in image):
</p>
<p>
  <img src="https://github.com/user-attachments/assets/6f28d948-1c2c-40ca-a3b8-1c4f7caf82a7" height="75%" width="100%" alt="Ubuntu VM"/>
  <img src="https://github.com/user-attachments/assets/8835acbb-8dd7-4cb3-9bfe-54a447e455dc" height="75%" width="100%" alt="Ubuntu VM"/>
  <img src="https://github.com/user-attachments/assets/fe94cbc8-3179-4a04-aff9-ab7b3fc75653" height="75%" width="100%" alt="Ubuntu VM"/>
</p>
<br />
<h3 align="center">
   Lets install wireshark
</h3>
<br />
<p> 
  First connect to your windows Vm
</p>
<p>
 <img src="https://github.com/user-attachments/assets/46c0f982-6a48-41d1-850a-32f25c85a345" height="75%" width="100%" alt="Wireshark"/>
</p>
<p>
  Then open interent explorer, go to www.wireshark.com, click on the Windows x64 installer to download that version of the app and then click open file.
</p>
<p>
  <img src="https://github.com/user-attachments/assets/0faf39ca-563e-4b83-b897-ce24d6d3ad37" height="75%" width="100%" alt="Wireshark"/>
</p>
<p>
 Now we continue the installation process by clicking next. Make sure in the packet capture "install ncap 1.79" box is clicked. When it comes to the usb capture make sure the "install UsbPcap 1.5.4.0" box is unboxed. Then finish by clicking install.
</p>
<p>
  <img src="https://github.com/user-attachments/assets/9e2da3d9-09d2-4831-8257-80d6ec2a92b6" height="75%" width="100%" alt="Wireshark"/>
  <img src="https://github.com/user-attachments/assets/84644d7e-e12f-4d6e-893d-1d02bf9c4de8" height="75%" width="100%" alt="Wireshark"/>
  <img src="https://github.com/user-attachments/assets/dcdeb682-b5f9-4a26-a628-3269259c245e" height="75%" width="100%" alt="Wireshark"/>
</p>
<br />
<h3 align="center">
  Now let's observe some ICMP traffic
</h3>
<br />
<p>
  Open wire shark 
</p>
<p>
  <img src="https://github.com/user-attachments/assets/a62b4cdf-ce9f-4070-86fd-7adf98d5302d" height="75%" width="100%" alt="Microsoft Remote Desktop - Mac"/>
  <img src="https://github.com/user-attachments/assets/8bfad268-32fa-48c9-883b-1461635a354e" height="75%" width="100%" alt="Microsoft Remote Desktop - Mac"/>
  <img src="https://i.imgur.com/0BsfNiS.jpg" height="75%" width="100%" alt="Microsoft Remote Desktop - Mac"/>
  <img src="https://i.imgur.com/0BsfNiS.jpg" height="75%" width="100%" alt="Microsoft Remote Desktop - Mac"/>
</p>
<p>
  Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark:
</p>
<p>
  <img src="https://github.com/user-attachments/assets/5ce063a1-f441-4547-829d-624b01c8ed5d" height="75%" width="100%" alt="Ubuntu private IP"/>
  <img src="https://github.com/user-attachments/assets/31d7e3e4-55ed-44f6-9bdb-cd11743d8aba" height="75%" width="100%" alt="ICMP traffic - private IP"/>
</p>
<p>
  Attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark:
</p>
<p>
  <img src="https://github.com/user-attachments/assets/d91df590-d699-49f7-a7aa-490b0174ec3f" height="75%" width="100%" alt="ICMP traffic - public IP"/>
</p>
<p>
  Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM:
</p>
<p>
  <img src="https://github.com/user-attachments/assets/5ca936fb-5c46-4c58-b1ef-34631cf8585c" height="75%" width="100%" alt="ICMP traffic - perpetual ping"/>
  <img src="https://github.com/user-attachments/assets/937048cf-44d4-4355-b7d9-a40f3937c583" height="75%" width="100%" alt="ICMP traffic - perpetual ping"/>
</p>
<p>
  Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic, while back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity:
</p>
<p>
  <img src="https://github.com/user-attachments/assets/72e40b6f-1e8b-45fb-b0d8-c70031585307" height="75%" width="100%" alt="ICMP traffic - perpetual ping"/>
  <img src="https://github.com/user-attachments/assets/2bcf4d40-33c2-4cc7-b0e3-7c43e4da2069" height="75%" width="100%" alt="ICMP traffic - ICMP denied"/>
  <img src="https://github.com/user-attachments/assets/40b009a9-2646-4e88-a168-05714edf1931" height="75%" width="100%" alt="ICMP traffic - ICMP denied"/>
  <img src="https://github.com/user-attachments/assets/50888daf-c683-42bd-ba3b-781ba336d630" height="75%" width="100%" alt="ICMP traffic - ICMP denied"/>
  <img src="https://github.com/user-attachments/assets/8739fcde-a26d-4bd6-ad70-5e52b2f95239" height="75%" width="100%" alt="ICMP traffic - ICMP denied"/>
</p>
<p>
  Re-enable ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line ping activity (should start working again).Finally, stop the ping activity:
</p>
<p>
  <img src="https://github.com/user-attachments/assets/2ff0f885-8daa-405a-ad56-87708b5ce80a" height="75%" width="100%" alt="ICMP traffic - ICMP re-enabled"/>
  <img src="https://github.com/user-attachments/assets/03319056-e8b4-4728-8098-748768e294e2" height="75%" width="100%" alt="ICMP traffic - ICMP re-enabled"/>
</p>
<br />
<br />
<h3 align="center">
  Time to observe SSH traffic
</h3>
<br />
<p>
  Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.
</p>
</p>
  Exit the SSH connection by typing ‘exit’ and pressing [return]:
</p>
  <img src="https://github.com/user-attachments/assets/8b9be5c0-9dfe-40ff-b162-cd45f4924962" height="75%" width="100%" alt="SSH traffic"/>
  <img src="https://github.com/user-attachments/assets/129b1492-2076-4538-b426-b4dfec99827e" height="75%" width="100%" alt="SSH traffic"/>
  <img src="https://github.com/user-attachments/assets/61a556f5-384c-4c21-9613-e37afa90e263" height="75%" width="100%" alt="SSH traffic"/>
  <img src="https://github.com/user-attachments/assets/a3522ca0-a18e-4f87-a1c7-4c546eaf1be9" height="75%" width="100%" alt="SSH traffic"/>
  <img src="https://github.com/user-attachments/assets/7b44a927-7711-4d2d-a8f0-3aa74747fb6b" height="75%" width="100%" alt="SSH traffic"/>
  <img src="https://github.com/user-attachments/assets/232cefcb-ac86-40c7-8dee-16d170a0ad03" height="75%" width="100%" alt="SSH traffic"/>
<p>
<br />
<br />
<h3 align="center">
  Next, we're going to observe DHCP Traffic
</h3>
<br />
<p>
  Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
</p>
Observe the DHCP traffic appearing in WireShark:
</p>
<p>
  <img src="https://i.imgur.com/mKyAHFr.png" height="75%" width="100%" alt="DHCP traffic"/>
</p>
<br />
<br />
<h3 align="center">
  Let's now observe our DNS traffic next
</h3>
<br />
<p>
  Back in Wireshark, filter for DNS traffic only.
</p>
<p>
  From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark:
</p>
<p>
  <img src="https://i.imgur.com/mYZ8CAK.png" height="75%" width="100%" alt="DNS traffic"/>
</p>
<br />
<br />
<h3 align="center">
  Finally, we will observe RDP traffic to finish up this tutorial
</h3>
<br />
<p>
  Back in Wireshark, filter for RDP traffic only using "tcp.port==3389".
</p>
<p>
  You'll be obseving a non-stop stream of traffic. Do you know why there is constant traffic in our tcp.port==3389?
</p>
<p>
  The answer is because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted:
</p>
<p>
  <img src="https://i.imgur.com/hNlhTVp.png" height="75%" width="100%" alt="RDP traffic"/>
</p>
<p>
  Now that we're finished observing the network, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT! This will prevent you from incurring additional charges and you won't be left surprised!
</p>
<p>
  Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion. You'll typically be notified or can click unde the bell notification just to make sure.
</p>
</p>
