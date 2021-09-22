# Performance Testing


performance testing:
ensures system reacts in a timely manner and serves needs
user experience: 
cpu utilisation
downtime

The ultimate goal of testing is to improve the user journey.

We want to test every single step og the user journey (img of the user journey)

Testing take a long time and is not a single step process (img of iterative process against approach)
Start small then scale up testing
Usually takes 6 to 12 weeks to fully test


how to make app highly available?
using multiple avalablity zones
diffreent regions have different vpcS LOAD BALANCERS
different types of testing, spike, soak, load

# ***ask kieron what his question was***

Test environment
env just before pub,
where you can perform tests
identical to live app

## Download and Install Java

https://devwithus.com/install-java-windows-10/

## Install IntelliJ and Scala

## Download Gatling
why gatling? used for performance testing and monitoring - create tests in scala, gatling runs them and makes a series of graphs and charts to narrate how successful the test was


## Instal Maven (for Java)

https://mkyong.com/maven/how-to-install-maven-in-windows/

---
**Rough notes**
What should we be monitoring about our app?
internet facing vs internal
internet facing -- RAM CPU load remaining disk space network load
Network traffic, CPU, etc. Automate reactions to situations

Get charged for max no. of instances that spin up --. need a policy for min/max policy,
when reating an autoscaling we provide a min and max no of instances
when autoscalinf kicks in new instances spin up
app load balancer attached to ig and vpc
when traffic increases node is balances between instances
#lod balancer redirectes traffic to active instances so no instance gets overwhelmed
as automatically ajusts computaional resources

4 types of performance testing: load, stress, spike, soak

**DIAGRAM FOR CW AND AUTOSCALING**
CW triggers event after observing the traffic
this is make sure user doesnt notice change in load
inastnace attached to autoscaling group


**DIAGRAM FOR AUTOMATION W GATLING, AWS, CW, S3, DOCKER, JENKINS**
