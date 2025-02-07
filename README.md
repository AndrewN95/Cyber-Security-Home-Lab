# Cyber Security Home Lab

This project seeks to establish a home lab as a foundation for learning as well as hands-on, practical application of the tools and software commonly used in the cybersecurity industry.
The initial setup, network configuration, virtual machine deployment, and overall infrastructure were guided by Corey Jones' tutorial:
Corey Jones' Guide: https://medium.com/h7w/ultimate-cyber-security-home-lab-with-proxmox-part-1-setting-up-the-network-2f70c91606ff

# Network Configuration and Setup
I used pfSense as the firewall and it will double as a gateway. Once installation of pfSense was completed, I configured the network gateways as shown in the image below:

![image](https://github.com/user-attachments/assets/6344a3d4-425b-44e0-a6b4-d3a4a918c961)

Network bridges and VLANs were then established to match the network interfaces in pfSense.

![image](https://github.com/user-attachments/assets/97d4f3ee-5596-4548-a99b-406b656fc60b)

Then, the interfaces must be assigned within pfSense so I used the pfSense web interface to do so. For my use cases, LAN and VLAN10-30 are the most important and most used interfaces. I first deployed a Kali Linux virtual machine on the LAN interface an headed over to the pfSense web interface to configure the network.

![image](https://github.com/user-attachments/assets/cfe1d7e8-d332-4efe-9f3c-ff8cd30b1b27)

After interfaces were assigned, the new virtual machines will need IP addresses. PfSense has a DHCP service, which I enabled for all interfaces except VLAN20 as that will be handled by the Windows Server 2022 which will be established as a domain controller.

![image](https://github.com/user-attachments/assets/d626938b-ac55-4014-b99f-e0840585fccc)

Since this project required clustering due to insufficient resources, I had to make use of VXLAN to allow pfSense to communicate with the second node in the cluster and thus provide the entire node with IP addresses. I named the VXLAN bridge vxnet and added the bridge to pfSense along with all the other virtual machines that I wanted behind the firewall.

![image](https://github.com/user-attachments/assets/b3c7254e-40de-4ff9-a657-8c67c27596a0)

# Virtual Machine Deployment
The network is correctly configured and working so I moved onto deploying the Windows machines. The first was Windows Server 2022. This machine acts as a domain controller and provides Active Directory, DHCP, and DNS for its users.

![image](https://github.com/user-attachments/assets/cd9cb826-f268-47d2-a17f-b4b165fb29da)

Created a couple of user accounts, one for myself with admin privileges. 

![image](https://github.com/user-attachments/assets/afeb4b73-54c4-4109-9ca0-bb29e67ba915)

After the Windows machines were deployed, vulnerable web applications were next on the list. First, I installed docker using a script from the guide. Then, I installed portainer as a docker container. This allowed me to view and manage other containers through a web interface. I then installed the vulnerable web applications shown below.

![image](https://github.com/user-attachments/assets/cb781e36-3161-4e5b-9ace-dd35b64aa86d)

The last virtual machine I deployed was Wazuh. I installed Wazuh by using the import function of Proxmox and from the OVA provided by the wazuh documentation: [https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html](url)
Once Wazuh was finished installing, I started the virtual machine and then followed the agent installation documentation to install an agent on the Windows 10 machine. The image below is the web interface from Kali Linux which does not have an agent installed yet.

![image](https://github.com/user-attachments/assets/3e277c48-86ad-4224-81f9-f3c2febb81c6)
