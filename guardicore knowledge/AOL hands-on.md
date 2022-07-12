- After you have your Agent Operations Lab talk, the best way to understand how things work is to practice writing some new tests. 
- Look here for options for running the tests -  
- [Agent Operations Lab Wiki](https://guardicore.atlassian.net/wiki/spaces/TESTING/pages/1912932089/Agent+Operations+Lab)
- [ ] Let’s start by creating a new tests module. Add a python script file under guardicore\tests\agents\agent_operations_lab_scenarios named test_training_aol.py (or any other name starting with test_).
- [ ] Add this at the top of your file -
	```
	import pytest
	import logging

	log = logging.getLogger(__name__)
	pytestmark = pytest.mark.training
	``` 
	- The last line will mark all the tests as training - so you can target them later.
- [ ] You’ll also need to add a matching configuration in - guardicore\tests\agents\agent_operations_lab\agent_operations_lab\plugin.py
- [ ] Under pytest_configure, add another configuration 
	```
	config.addinivalue_line("markers", "training: "mark to group Training tests.")
	```
- [ ] Let’s add the first test -
	```
	@pytest.mark.run(order=1)
	@pytest.mark.possible_tested_os(os=[AllocationOS.UBUNTU_16])
	def test_install_agent_default_profile(test_machine: ClonedMachine):
		log.info(f"Testing machine {test_machine}")
	```
- This is the minimal setup you’ll need. Now you can use Management Utils, Traffic Generator, or any other fixture to make actions.
- [ ] To see usage examples take a look at:
	```
	guardicore\tests\agents\agent_operations_lab_scenarios\examples
	```
- [ ] Try to add the following scenarios (and make them dependent) -
	1. [ ] Install an Agent, and get the Agent’s version
	2. [ ] Add an installation profile, and add a policy rule (for a random port)
	3. [ ] Use a supporting machine to create traffic, and then validate it appears in the Network Log on Management
	4. [ ] Uninstall the Agent, and make sure Agent Missing flag appeared on the Management
- [ ] When you’re done, run the tests on Jenkins and look at the output (HTML, log, JUnit).
