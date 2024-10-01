<h1>SIEM Lab Writeup</h1>

<h2>Goal for the project</h2>
My goal was to use Wazuh to establish my own Security Information and Event Management (SIEM) Lab. This document contains all the steps I took and what would need to be done to recreate this lab. By doing this, I would be able to learn more about what a Security Operations Center (SOC) is and how it functions. By engaging with my SIEM to trigger security warnings, I will also be able to apply my existing skills and pick up new ones in Kali Linux. To do this, I'll be using two distinct virtual machines: one for the dashboard and another for the SIEM to be triggered.
<br />

<h2>What is a SIEM Lab?</h2>

Security experts and students utilize SIEM tools in a controlled setting called a SIEM lab to monitor, identify, and react to cybersecurity threats. Usually, it entails configuring systems and tools to gather, store, and examine logs from a variety of devices, including servers, firewalls, endpoints, and apps. Without affecting actual systems, it enables training, testing, and experimentation with security data and configurations. This can be useful for training, tool familiarization, and compliance. Many of these tools, such as Wazuh, include a compliance standard to allow easier implementation in a controlled environment. This can ensure that any implementations on a system can be deduced as safe and implemented on the main system. Wazuh in this instance, Elastic, and Splunk are a few instances of SIEM labs. 

<h2>Project walk-through:</h2>

<h3>Install Wazuh:<h3> 
  
To install Wazuh Dashboard enter the following in command into the command prompt of your preferred operating system. 
- curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

Once the installation is complete an output at the bottom of the command line will demonstrate how to access the dashboard and how to log in. To access the dashboard, you would navigate to https://[your_local_ip] and log in with the default credentials that it provides. Once logged in you will be met with this screen.
<p align="center">
<br/>
<img src="https://i.imgur.com/dpuFiuq.png" height="80%" width="80%" alt="Screenshot 1"/>

<p align="center">
Figure 1: The default Wazuh dashboard that is presented to the user once logged in.
<br />

<h3>Installing Agents:<h3>

It can be overwhelming to look at first, but the first step will be to create an agent to start monitoring endpoints. To do this, navigate to Server Management then Endpoints Summary and you will be able to create a new agent on this screen. After choosing what package and optionally naming the agent you will be given a command to run on another virtual machine. The command will look like this but will vary slightly depending on what operating system the client is using. In this case, I am running a Debian AMD64 Linux machine.
- wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.9.0-1_amd64.deb && sudo WAZUH_MANAGER=[local_ip] WAZUH_AGENT_GROUP=[local_group_name] WAZUH_AGENT_NAME= [local_name] dpkg -i ./wazuh-agent_4.9.0-1_amd64.deb
  
All sections in brackets will vary according to the information that you provide. Once that is run on your client machine, or virtual machine in this case, the agent needs to be started. The following commands can be run to start the agent.
- sudo systemctl daemon-reload
- sudo systemctl enable wazuh-agent
- sudo systemctl start wazuh-agent

Once the agent is installed and turned on it should appear on the endpoint summary on the Wazuh dashboard. The screenshots provided is what an agent will appear as the Wazuh. <p align="center">
<br/>
<img src="https://i.imgur.com/zbkGlXD.png" height="80%" width="80%" alt="Screenshot 2"/>

<p align="center">
Figure 2: The agent has been added to the endpoints section.
<br /><p align="center">
<br/>
<img src="https://i.imgur.com/RJrQwhT.png" height="80%" width="80%" alt="Screenshot 3"/>

<p align="center">
Figure 3: The agent has been added to the dashboard.
<br />

<h3>What I learned:<h3>
I can install and operate Wazuh. I was able to better visualize and comprehend what was happening by creating graphs and charts out of several of the alerts and compliances. It was difficult for me to set up because I had never used a software like this before. I ran into a challenge with my virtual machines sharing an IP address. I resolved the issue by setting up Network Address Translation (NAT) on the virtual machines. This process was new to me and something that I had to learn and adapt to.


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
