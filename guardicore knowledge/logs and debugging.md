- Every Centra component creates log files that can be very helpful during debugging. See these main logs and where they are located:
1.  Agent (Linux + Windows)
	- gc-guest-agent.log: Reveal agent.
	- gc-enforcement-agent.log/ deception server):
	- guardicore.hp_vm.log : Shows all information about the HPVM.
	- To verify HPVM is up, search for GGGGG (a big GO sign).
	- Logs location: /var/log/guardicore
	
##### Playground
- Through the tester playground you can access the Centra API directly. management_client has access to client.py methods.
	- Running playground can be done from : Enforcement.
	- gc-deception-agent.log: Redirection to honeypot (HPVM).
	- gc-detection-agent.log: FIM and OSQuery (Insight).
	- Logs location:
		- Linux: /var/log/
		- Windows: C:\ProgramData\Guardicore\logs (windows 2008+).
		- Windows 2000/2003: C:\Program Files\Guardicore\logs

2.  Aggregator:
	- Many logs, all logs are prefixed with aggregator (but also mitigation).
	- Best strategy is to grep (or zgrep)
	- mitigation.worker.* responsible to send the aggregated data to the mgmt.
	- Logs location: /var/log/guardicore

3.  Mgmt:
	- gc-cluster-cli health: Services health on the mgmt.
	- Most important log: rest-server.*.log
	- Errors in Centra's bell icon will be shown in the corresponding service / rest-service log.
	- Best strategy is to grep (or zgrep)
	- Logs location: /var/log/guardicore

4. HPVM (Honeypot virtual machine)
	- pycharm after you have cloned the guardicore repository. Instructions and code are in `tests/qa/tools/playground/playground.py`