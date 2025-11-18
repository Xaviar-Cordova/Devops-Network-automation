<img width="973" height="239" alt="image" src="https://github.com/user-attachments/assets/2fb60abc-33c6-4efe-b9d4-301f0ce0067a" />



This video demonstration shows my playbooks configuration of 3 switches for production use. Once we identified the cores & distributions switches, we nested them under a parent group "switches" to allow deployment of configurations to all layer 2 devices or a certain part in our network. Since these are devices derived off the IOS and an special module needed to allow the correct network interactions, I put those essential parameters as "all" in group_vars to apply to future devices in any of our playbooks. As it is best practice to re-use tasks when possible, I created a couple tasks as a role "Switchprep" where I apply vlan 1-8 with description added on all switches. something VTP in Cisco isn't capable of, and Juniper can't mass deploy VLANs at all. I also enabled LLDP on every port via variables within my role, which for a manual project deployment would've taken hours to accomplish. 
<img width="265" height="249" alt="image" src="https://github.com/user-attachments/assets/3dc970e8-9328-461e-b713-d21ca8500fc0" />


For my Distro layer, I wish to assign VLANs to access ports, but each host will have its unique needs. For instance, Bob and Alice are physically on Gigaethernet port 2 on the west & east switch, respectively. But Bob is on vlan 2 as he is a residential client, while Alice uses vlan 3 and 4 since she is a business owner of a call center. As there are multiple ports & To accomplish this, I created host variables that my loop logic can refer to that apply changes when a key matches in them. east switch has a voice key pair so it'll have it applied to the ports assigned for it, while the task will skip West and proceed to setting the ones instead like nonprofits.<img width="920" height="444" alt="image" src="https://github.com/user-attachments/assets/06ca2e99-d5e6-41c1-96fc-f286a51f1f7a" />


