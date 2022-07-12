1. [ ] Write your first tests on AOL. For reference see test_monitoring_enforcement_sanity
	- [ ] Policy related test:
		- [ ] choose two machines
		- [ ] create an allow rule between them (over a random port)
		- [ ] perform a connection - make sure it was allowed
		- [ ] create and override-block rule between them over the same port
		- [ ] perform a connection - make sure it was blocked
		- [ ] perform a connection on a different port - make sure it was allowed.
2. [ ]  Write test using traffic generator:
	- [ ] Preparation: create two Linux hosts in the same network (HostA and HostB).
	- [ ] Use traffic generator deploy API to deploy traffic generator on both hosts.
	- [ ] Test UDP connectivity from HostA to HostB.
	- [ ] Test ICMP connectivity from HostB to HostA.
3. [ ]  Get to know PEL
	- [ ] Take a look on PEL [design](https://guardicore.atlassian.net/wiki/spaces/TESTING/pages/1741291766/PEL+-+Policy+enforcement+lab)
	- [ ] Take a look on README (tests/pel/README.md)
	- [ ] Create PEL env by running  ‘prepare` step from [Jenkins](https://jenkins.guardi/job/Policy_Enforcement_Lab_v2/) 
	- [ ] See your env on [GCP](https://console.cloud.google.com/compute/instances?project=guardicore-26097118&instancessize=50)
	- [ ] Run tests on existing env with Jenkins Job.
	- [ ] Execute tests locally (see README)
	- [ ] To be able to do that, allow ssh from your public IP. Add rule [here](https://console.cloud.google.com/networking/firewalls/list?project=guardicore-26097118). 
	- [ ] Add a new test: block a specific port and make sure it is blocked, make sure the agent blocks only that port.
	- [ ] Destroy your environment by executing “main.py” locally.