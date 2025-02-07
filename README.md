# Cyber Security Home Lab

This project seeks to establish a home lab as a foundation for learning as well as hands-on, practical application of the tools and software commonly used in the cybersecurity industry.
The initial setup, network configuration, virtual machine deployment, and overall infrastructure were guided by Corey Jones' tutorial:
Corey Jones' Guide: https://medium.com/h7w/ultimate-cyber-security-home-lab-with-proxmox-part-1-setting-up-the-network-2f70c91606ff

# Network Configuration and Setup
I will be using pfSense as the firewall and it will double as a gateway. Once installation of pfSense was completed, I configured the network gateways as shown in the image below:
![image](https://github.com/user-attachments/assets/6344a3d4-425b-44e0-a6b4-d3a4a918c961)

Network bridges and VLANs were then established to match the network interfaces in pfSense.
![image](https://github.com/user-attachments/assets/97d4f3ee-5596-4548-a99b-406b656fc60b)

Then, the interfaces must be assigned within pfSense so I used the pfSense web interface to do so. For my use cases, LAN and VLAN10-30 are the most important and most used interfaces.
![image](https://github.com/user-attachments/assets/cfe1d7e8-d332-4efe-9f3c-ff8cd30b1b27)

