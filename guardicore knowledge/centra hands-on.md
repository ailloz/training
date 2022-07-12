1. [ ] Labeling
	1. [ ] Create a new label (Centra->Reveal->Labels) named Agent:EvenNumber with criteria of names that either end with 2 or end with 4. Do the same for Agent:OddNumber and 1 or 3.
	2. [ ] Add label groups which will include these two labels 
	3. [ ] Try deleting the OddNumber label 
	4. [ ] Create a new dynamic label with criteria of full ip (100.100.102.211)
	5. [ ] Add the ip to one of the agents and verify the agent appears in the new dynamic label 
2. [ ] Reveal
	- This feature is what helps us to see traffic in the data-center.  
	- In order to “feel” the feature, we will create some traffic and play with it in order to see how it works.  
	- The traffic can then be ‘visualized’ in a map.  
	- These are the things we will be doing:
		1. [ ] Generate internal/external traffic in the datacenter
		2. [ ] Install Interesting application to you choice (that perform network traffic) and examine how it looks in the Datacenter view
		3. [ ] Define a simple segmentation policy and create an incident
		4. [ ] Check out the UI
		5. [ ] Reveal -> Data Center
		6. [ ] Network Log
	- How to do it:
		1. [ ]  Make a number of  connections to ports 5555, 6666, 7777, 8888 between the attackers/servers using netcat. For example:
			1. [ ] On Server1: nc -l -p 8888
			2. [ ] On Attacker1: nc 172.17.0.2 8888
			3. [ ] Make some connections to the internet (for example wget [www.ynet.co.il](http://www.yent.co.il), wget [www.evil.xyz.com](http://www.evil.msn.com))
		2. [ ] Login to the UI and check out the reveal map (Reveal -> Saved Maps):
			1. [ ] Create a new saved map with connections from the past 5 hours
			2. [ ] Open the saved map. can you make sense of what’s going on there? Retrace your steps and see how they look on the map (Double click the nodes to get all the way down to the process level)
			3. [ ] Filter out only connections to the internet
			4. [ ] Filter out connections from Attacker1
			5. [ ] Filter out connections from IP 100.100.100.11
			6. [ ] Filter out connections from one of the labels you've created earlier
			7. [ ] Exclude connections on  port 8888
			8. [ ] Change the grouping option to hosts. 
			9. [ ] Verify all of the connections appears in the network log 
			10. [ ] Follow the logs flow for one of the reported connections (Agent to Mgmt)
3. [ ] Deception
- Deception is a feature that redirects suspicious traffic to a “honeypot” VM in order make the attackers think they are actually attacking a real server in the data-center, while allowing Guardicore to collect data about the attackers and their attack vector.  
- In order for you to simulate a simple “attack” and experience this we to generate some connections that would create incidents as well
-   Create incidents:
    

-   Perform a “lateral movement” attack and a network scan
    

-   Linux Services: SSH FTP MySQL
    
-   Windows Services: SMB RDP
    

-   Perform Failed connection to existing host (TCP redirection)
    

(drop the traffic by iptables, so the host won’t answer it) 

-   Perform Failed connection to non existing host (ARP redirection)
    

(this might take several attempts to different ips. Ask why!)

-   Add a bypass inspection rule and do another attack
    

-   Check out the UI:
    

-   Centra->Activity->Redirections Log
    
-   Centra->Incidents
    
-   Security Dashboard
    

  
You may follow these instructions to create such incidents and experience it for yourself:

Incident #1:

-   From Attacker1 connect to 100.100.100.187  (try to guess the passwords)
    
-   Check out the server you’ve reached – what’s its name? run some basic commands (ifconfig, netstat)… Get creative :) 
    

  

Incident #2:

-   From Attacker1 connect to 100.100.100.197
    
-   Add a user, add it to the sudo group and test it.
    

-   adduser <username>
    
-   su - <username>
    
-   sudo ls -la /root
    

  Incident #3:

-   Connect to  Attacker2
    
-   Download Nmap
    

-   apt-get install nmap
    

-   Run a scan: 
    

-   nmap -sV 100.100.100.100-105
    

  

Now it’s time to connect to the UI:

Go to https://<your_env_number>.thin.env:8000

1.  Explore the redirection log (Centra->Activity->Redirections Log)
    

1.  Filter out IP 100.100.100.87. How many DPs reported network activity? What’s the difference between the reports?
    
2.  Filter out activity from Attacker2. What do you see?
    

3.  Explore the incidents screen (Centra->Incidents->All Incidents)
    

1.  Do you recognize the attacks you made? What happened as a result of the scan? 
    
2.  Filter out the incidents that were tagged as “Human”
    
3.  Clear previous filters and filter out High severity incidents, dive into them:
    

1.  see the detailed play by play vs the summary
    
2.  check out the different tabs
    

5.  Follow the logs flow (Agent to Mgmt)
    

  

### Reputation: 

-   configure Q-server to “q.guardi” and perform connections to “[http://www.evil.msn.com](http://www.evil.msn.com)”
    
-   try a few more connections and see what reputation-incidents are created
    

### Policy: 

The Policy pages are where a customer configures all the rules for his data-center.  
In general, rules can either be “allow”, “alert”, “block”.  
There are several more rule types that are based on those 3 rules, feel free to explore them yourself in the application.  
  
In order for you to get a feeling of this feature, you can practice the following:

-   Create a new alert rule in segmentation screen (Centra->Policy->Segmentation Rules) with source label Agent:OddNumber, destination label Agent:EvenNumber and destination port 6666 TCP. Publish the rule.
    
-   Create a new block rule from any to internet on port 12345 TCP
    
-   Publish the rules and verify :
    

-   Agent received the relevant policies 
    
-   Follow the logs flow (Mgmt to Agent)
    

-   Make  a connection (with nc) between OddNumber and EventNumber machines which are in the labels.
    
-   Make a connection between any machine to the internet on port 12345 tcp 
    
-   Make a connection between any machine to the internet on port 12345 udp
    
-   Verify all of the connections appears in the network log 
    
-   Create a new map and verify all connections appears in it .
    
-   Revert the last revision before adding the rule in stage A.
    
-   Verify that the relevant agents received the relevant policies.
    

### Orchestration Data: 

-   Check out Centra-> Assets
    
-   look at Orchestration page in a nested and non-nested env. what’s the difference?
    

### File Integrity Monitoring (FIM)

-   ([Omri Ossie](mailto:omri.ossie@guardicore.com) is our FIM master - feel free to ask for help) 
    
-   Define FIM template 
    
-   Verify it looks legit 
    
-   Change the protected file content. See what happens
    

### Component Monitoring:

-    Perform basic component maintenance checks for the management/aggregators/deception server and agents:
    

-   Learn about [monicore](https://guardicore.atlassian.net/wiki/spaces/MGMT/pages/33980455/Monicore+v2)
    
-   Reboot the components 
    
-   Check their status
    
-   Start/stop services
    

-   Check out the UI:
    

-   admin->Detection/Collectors/Aggregators/Agents
    
-   system log (alarm bell on the top right)
    

-   Explore the assets screen (Centra-> Assets):
    

-   Which assets are at risk?
    
-   Dive into Attacker1 and Attacker2, check out the different tabs and verify the relevant label appears in the asset page.
    

  

### RBAC (Role Based Access)

RBAC allows for multiple users with different roles and permissions.  
You can play around with it and see it in action.

-   Choose one role (or more) from here : [link](https://docs.google.com/spreadsheets/d/1awauWJQAwRr-z3jmdq0F4OgFJYNP-KvhDl1Gf-KIcBU/edit#gid=0)
    
-   Verify the Permissions for this role in the ui
    

  

### Explore Centra

Now that you have played around with Centra, created some connection flows, looked at some maps and created some rules, it’s time to play around more and do some ‘free exploration’.  
Search for pages / features / buttons that you are not familiar with and feel free to ask questions about them. 

  

### Look at a real live Centra in action

Check out a real production env - [https://cus-1801.cloud.Guardicore.com](https://cus-1801.cloud.guardicore.com)

Full details here:  [GC-Mgmt-Production](https://guardicore.atlassian.net/wiki/spaces/DEVOP/pages/30933126/GC-Mgmt-Production)

  

### Testing Deployment:

-   Rebuild your environment to the previous recommended tag (the recommended tag is stable version). Use Job 3 in the regular (pink) jenkins
    
-   Run the sanity and the simulation sanity jobs on your env
    

  
  

### Install Centra From Scratch:

-   Get the latest centra deployment Guide
    
-   Read the following documentation page: 
    

-   [Setup wizard](https://guardicore.atlassian.net/wiki/spaces/COL/pages/360513666/Setup+wizard)
    
-   [Test-Drive Lab Details](https://guardicore.atlassian.net/wiki/spaces/TESTING/pages/1557725233/Test-Drive+lab+environment)
    
-   [Test Drive Setup (for RC)](https://guardicore.atlassian.net/wiki/spaces/TESTING/pages/1557989130/Test-Drive+RC+Lab+Setup+Local+Guardicore+vCenter)
    

-   Follow instructions in above documents while working closely with @Boris 
    

### Patch And Upgrade

-   Build your first Centra Patch !(you can use the next stable tag - or latest)
    
-   Upgrade the system