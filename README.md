# SYN Flood Attack Using Metasploit
**Aim:** To provide an educational demonstration of a SYN flood DoS attack using Metasploit in a controlled environment, offering users hands-on experience in identifying network vulnerabilities and understanding the impact of SYN floods on system resources.

**Objectives:**
1. To explain the mechanics of SYN flood attacks and their effects on network resources.
2. To guide the use of Metasploit and nmap for vulnerability scanning and attack execution.
3. To demonstrate traffic analysis with Wireshark to identify SYN flood patterns.
4. To reinforce ethical hacking principles by demonstrating attacks in a secure, authorized setting.
5. To increase awareness of DoS attack defenses and mitigation strategies.

# Requirements
1. Victim Machine: A machine running Ubuntu Linux, configured as the target system for the attack.
2. Attacker Machine: A machine running Kali Linux, equipped with tools necessary for launching the attack.
3. Tools: Metasploit Framework for attack deployment, nmap for port scanning, and Wireshark for traffic analysis.


# Step 1:  Identify the IP Addresses of the Victim and Attacker Machines
To successfully execute the attack, the IP addresses of both the attacker and victim machines must be noted.

# On the Victim Machine (Ubuntu)

1. Open the terminal on the Ubuntu machine.
2. Enter the command:

   ***ifconfig***

3. Locate and write down the machine’s IP address, which typically appears under inet in the output (e.g., 192.168.x.x).

# On the Attacker Machine (Kali Linux)

1. Open the terminal on the Kali machine.
2. Enter the command:
  
   ***ifconfig***

3. Write down the IP address of the attacker machine for later use.

# Step 2: Scan the Victim Machine for Open Ports
The goal is to verify which ports on the victim machine are open and accessible, as certain ports (e.g., SSH or HTTP) are often the primary targets for SYN flood attacks.

1. On the Attacker Machine in the terminal, type:

   ***nmap [Victim’s IP Address]***

2. Review the output to confirm that the necessary ports are open on the victim machine. You should see open status on ports such as 22 (SSH) or 80 (HTTP).

# Step 3: Launch Metasploit on the Attacker Machine
The Metasploit Framework is an open-source platform used for developing, testing, and executing exploit code against target systems.

1. In the terminal on the Attacker Machine, launch Metasploit by entering:
  
   ***msfconsole***

2. Wait until the console fully loads, displaying the **msf6>** prompt, indicating that Metasploit is ready to receive commands.

# Step 4: Search for SYN Flood Exploits in Metasploit
Metasploit provides various modules to simulate different types of network attacks. We will search for an auxiliary module designed specifically for a SYN flood DoS attack.

1. At the **msf6>** prompt, enter:
  
   ***search syn***

This command will display a list of SYN-based exploits and payloads.

2. Further refine the search by typing:
  
   ***search syn flood***

3. Among the results, locate and confirm the module **auxiliary/dos/tcp/synflood**, which is specifically crafted for launching SYN flood attacks.

# Step 5: Select the SYN Flood Auxiliary Module
Now, configure Metasploit to use the SYN flood module.

1. Type the following command to select the SYN flood module:
  
   ***use auxiliary/dos/tcp/synflood***

2. After selection, the Metasploit prompt will change to **msf6 auxiliary(dos/tcp/synflood) >**, indicating that you’re now operating within the SYN flood module.

# Step 6: Configure the SYN Flood Module’s Options
You’ll need to configure specific parameters, such as the target IP address and spoofed IP address, for the attack to be effective.

1. To view configurable options, type:

   ***show options***

This will display a list of required settings, including **RHOST** (Remote Host) for the victim’s IP and **SHOST** (Spoof Host) for the spoofed IP address.

2. Set the **RHOST** option to the Victim Machine’s IP:
  
   ***set RHOST [Victim’s IP Address]***

3. Set the **SHOST** option to a random IP address within the network range to act as a spoofed IP. This will mask the attacker’s true IP and simulate traffic from multiple sources. For instance:

   ***set SHOST 192.168.0.125***

# Step 7: Initiate the SYN Flood Attack
With the configurations in place, it’s time to launch the SYN flood.

1. Run the configured module:

   ***run***

2. This will begin sending a high volume of SYN packets to the victim’s open ports, causing them to hold half-open connections. The flood of these partial connections eventually exhausts the target’s resources, leading to a denial of service.

# Step 8: Monitor System and Network Impact
Observe the attack’s effects by monitoring resource usage on the victim machine and analyzing network traffic on the attacker machine.

On the Victim Machine

1. Launch the System Monitor tool in Ubuntu to observe system resource utilization (CPU, memory, network):
  
   ***gnome-system-monitor***

2. You may notice a significant increase in CPU and network usage as the machine struggles to handle the influx of SYN packets.

On the Attacker Machine

1. Open Wireshark to capture and analyze the network traffic generated by the SYN flood:
  
   ***wireshark***

2. Set filters to isolate the SYN packets or to view the traffic between the attacker and victim machines. Notice the pattern of repeated SYN packets, indicating the flood of requests overwhelming the target.

# Conclusion and Clean-Up
The SYN flood attack demonstration is complete. Ensure that you:
- Terminate the attack by closing the Metasploit console.
- Analyze and document any observed results.
- Restore normal operation on both machines by restarting network services if needed.

This exercise has demonstrated how a SYN flood attack can disrupt a system’s resources, providing valuable insights into network defense and traffic analysis for mitigation strategies.

Remember: Always respect ethical boundaries and use this knowledge to improve cyber security, not to harm or disrupt others.

#

**Legal Disclaimer:** *This guide is for educational purposes only and must be used within authorized, controlled environments. Unauthorized use of these methods on systems or networks without explicit, written consent from the rightful owner is illegal and may violate local and international laws. The authors disclaim all liability for any misuse that results in unauthorized access, damage, or disruption, and users assume full responsibility for compliance with applicable laws.*
