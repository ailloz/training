This is where the value of the automation team really comes in.

So far, you see that there are a lot of tests, over a dozen or more different testing suites, each one tailored for a different testing purpose and component. 

In this section, we will go over how our tests are actually run, how often they run, and how and where they are run. This part can get a bit Dev-Opsi :) 

### Nightly Testing Environments (“Autotesters”)

1.  Every evening (~18:00) we’re running our tests on 3 different versions of Centra: 
    

1.  The stable version (“master-2”) - runs once a week
    
2.  The current version (“master-1”) - runs once a week
    
3.  The development version (“master”) - runs 5 times a week. 
    

3.  Each version (“build”) can be run on different environment configurations, so we’re testing several configurations as well.
    
4.  In the morning we go over the results to see what's the status of every build.
    
5.  Nightly reports are re ported to TestRail.
    
### TestRail

1.  TestRail is a test case management software; It’s what we use to store our nightly test results and also run our manual tests.
    
2.  Automated results are reported nightly through TestRail API and are added under each nightly tag, per environment name.
    
3.  Nightly report links are also posted in #testrail_nightly_report channel every morning.
