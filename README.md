<img width="973" height="239" alt="image" src="https://github.com/user-attachments/assets/2fb60abc-33c6-4efe-b9d4-301f0ce0067a" />

Nearing my RHCE milestone, which gravitates toward the DevOps space, this project provides a brief example of network automation. It can take years to become a strong network professional and years to become a strong Linux administrator; having both skill sets together is relatively rare. I’ve been fortunate to build experience in both. One cannot automate what isn't understood, and an end goal of DevOps philosophy is the automation of infrastructures.

This [video](https://www.linkedin.com/posts/xaviar-cordova_nearing-the-rhce-milestone-that-gravitates-activity-7352073878589886465-ZSk7?utm_source=share&utm_medium=member_desktop&rcm=ACoAACk3cLwBKFBtRW6pPZQ1kww2NCrJqsy4TqU) demonstration shows my Ansible playbook configuration for three switches in a production-style lab. Once we identified our cores & distributions switches, we nested them under a parent inventory group called "switches" to allow deployment of configurations to all layer 2 devices or to targeted subsets of our network. Since these are devices derived off the IOS and an special module needed to allow the correct network interactions, I put those essential parameters as "all" in group_vars to apply to future devices in any of our playbooks. 

Following best practices for reusability, I created a role named switchprep that applies VLANs 1–8 with descriptions on all switches. This provides a very effective labeling scheme to standardize VLAN creation across the network — something Cisco VTP isn't capable of, and that Juniper lack altogether. The role also enables LLDP on every port using variables, which if done manually  on each switch would've taken hours to complete. 

<img width="265" height="249" alt="image" src="https://github.com/user-attachments/assets/3dc970e8-9328-461e-b713-d21ca8500fc0" />

At the distribution layer, I assign VLANs to access ports based on each host’s needs. For example, Bob and Alice are both physically connected to GigabitEthernet 2 on the west and east switches. But Bob is a residential client on VLAN 2, while Alice is a business user who requires both data (VLAN 3) and voice (VLAN 4) for a call center. To accomplish this, I define host-specific variables that the Ansible loops reference when applying configuration. East switch has a voice key pair so it'll have it applied to the ports assigned for it, while the task will skip West and proceed to setting the ones instead like nonprofits.
<img width="920" height="444" alt="image" src="https://github.com/user-attachments/assets/06ca2e99-d5e6-41c1-96fc-f286a51f1f7a" />


