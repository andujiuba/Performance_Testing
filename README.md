# Performance Testing

Part of the **AUTOMATION SERIES**: Gatling highlighted

**DIAGRAM FOR AUTOMATION W GATLING, AWS, CW, S3, DOCKER, JENKINS w links to repos**

## What is Perfromance Testing and why do we need it?
- ensures system reacts in a timely manner and serves needs
- maps out user experience 
- monitors cpu utilisation
- logs any downtime

**The ultimate goal of testing is to improve the user journey.**
We want to test every single step of the user journey and ensure that there are no obstacles.
- (img of the user journey)

Testing take a long time and is not a single step process 
- (img of iterative process against approach)
The best method is to start small then scale up the testing. It usually takes 6 to 12 weeks to fully test a system, so thorough testing is imperitive.

Testing can simulate *SQL injections* or *DDOS attacks* --> planning for the worst possible outcome. **LINKS**

## How to make an app highly available?
- using multiple avalablity zones
- diffreent regions have different vpcs 
- LOAD BALANCERS

## How to test
There are different types of testing, spike, soak, load and stress testing

- (img of graphs)

## What is a test environment?
It is the environment just before pubublication where you can perform tests that simulate the live app.

**PLAN:**
- performance testing
- load testing
- soak testing
- AWS Jenkins runs tests
- CloudWatch metrics
- use SNS/SQS
- build a job where Jenkins does testing for us

---

## Download and Install Java
![image](https://user-images.githubusercontent.com/88186581/138720374-e56c51a6-6d8d-4d21-b1fe-ea094d940b43.png)

https://devwithus.com/install-java-windows-10/

Check Java is installed with `java --version` in th terminal.

## Install IntelliJ and Scala
![image](https://user-images.githubusercontent.com/88186581/134367948-9c0c5961-82cb-4027-9cd4-a35e7e5d6623.png)

https://www.jetbrains.com/idea/download/#section=windows

Add Scala plugin

## Download Gatling
![image](https://user-images.githubusercontent.com/88186581/134368057-85266995-1166-4108-85e6-0072eb221b80.png)

https://gatling.io/open-source/#downloadgatling
https://www.blazemeter.com/blog/how-to-install-gatling-on-windows

Keep the gatling folder in the `Program Files` folder within `User`.

### Why Gatling? 
Gatling is used for performance testing and monitoring - it create tests in scala, gatling runs them and makes a series of graphs and charts to narrate how successful the test was.
This is why Gatling is so desirable --> it is an incredibly user-friendly and cohesive system. 

## Instal Maven (for Java)
![image](https://user-images.githubusercontent.com/88186581/134368130-9a233123-b24d-4518-882c-316703391daf.png)

https://mkyong.com/maven/how-to-install-maven-in-windows/

## Setting Up Performance Testing in Gatling

(**breakdown img/gif**)

Open IntelliJ in **Admin** mode and open a new projects within the Gatling folder.
The application that is provided in this exercise is given by Gatling to help visulaise and test out its functionalities and the interface.

(Gatling file directories
- bin: .bat batch file, .sh shell file
- conf: config for gatling project, recorder records http requests to any server you want to record
- lib: libraries available
- results: results/outcomes from tests after being run
- target: OOP, contains classes
- user files: resources and simlations, records actions requests tests)

1. `cd` into `bin` folder
2. Run `gatling.bat`(For Windows, if you are using a Mac or Linux machine, type in `gatling.sh`). If you have set up the env var and opened IntelliJ as Admin, you should get the response:
```
GATLING_HOME is set to "C:*LOCATION_OF_ENVIRONMENT_VARIABLE*"
JAVA = "java"
```
3. Choose the `computerdatabase.BasicSimulation` operation and enter the number when prompted
4. After `Select run description`, type in whatever name is appropriate --> I used *SRE Akunma Performance Testing* for this session
5. Requests and their outcomes will start to be printed in the terminal
  - Since there have been no changes to the project 
6. In the `results` file, find the file with the name provided in the descirption --> look up `index.html`
7. `index.html` provides a detailed report that we can see in the browser --> copy the **absolute file path** and paste in a browser
This is what you should see: **IMG OF GATLING PAGE W LABELS**
8. In `user-files` --> `simulations` --> `computerdatabase` --> `BasicSimulation` there is a breakdown of the series of tests the project is run with. The information given in index.html is based on these tests.

### *We will do this again, this time selecting an advanced simulation*

9. After running `gatling.bat`, choose the last simulation option prompted which should be titled: `computerdatabase.advanced.AdvancedSimulationStep05`
10. Add a description: *Sparta Advanced Performance Testing*
11. Open up the index page using the `index.html` file located within the selected simulation in the `results` file.
**IMG OF new user-file directory**
12. `user-files` --> `simulations` --> `computerdatabase` --> `advanced`, open the simulation that was just run.

Compare the different environments the two simulations are run in and look at the results that are given. Changing the pause times or the number of users at a time is the best way to test the resilience of the app.

*But how should we decide on the parameters that we measure the system against?* <br>
You can search the average response time for most websites and match it against the response time for own website.

Gatling provides us with two options: HAR file and HA Proxy

(**HAR and HA INFO**)

## Running Tests Based on Own Server
(**img of Jenkins main menu**)

1. Go onto your own web server (I am using the Jenkins Project used in ***SRE_Jenkins***)
2. Right-click on the web-page for your server and select `Inspect` (**IMG OF INSPECT POPUP**)
3. Go to `Network` --> there should be no activity
4. Click box to `Peserve log`
5. Click on the clear button on the left and then the recording button beside it
6. Back in IntelliJ, enter the `BasicSimulation` file in the `computerdatabase` folder and change the `.baseurl` code to your server
7. `cd` into `bin` again and run `recoder.bat` (or `recorder.sh` for Mac/Linux). You should see:
```
GATLING_HOME is set to "C:*LOCATION_OF_ENVIRONMENT_VARIABLE*"
JAVA = "java"
```
8. A new window will pop up. (**IMG OF POPUP**)
  - Recorder mode: HAR Converter
  - HAR File: TBD
9. We want to convert data from `recoder.bat` into a HAR file
10. Go back to the webpage of your server with the `Inspect` open --> make activity on page by logging in etc.
11. In `Network`, click the `Export HAR file` button located underneath the `Application` tab
12. Back in the Gatling Recorder window, add the new HAR file that was just recorded
  - Give it an appropriate Class Name (e.g. AkunmaSpartaTest)
  - Leave Output as it is
  - Click `Start` in bottom right corner
13. Go back to `simulations` under `user-files` --> you should find the new Class you just created (**IMG**)
14. You should see  everything that you did on the webpage while it was recorded (including all passwords entered, all pages loaded etc.)
15. Run `gatling.bat` and select the Class you created --> open the `index.html` file in the web browser and see the results

## Running Tests with Node App

1. Set up and run the app (see ***AMI repo***) and `ssh` into the VM
2. Add DB_HOST environment variable and `npm start`
3. Follow the same steps as above to record activity on app (steps **2-5**, then step **11**). Record:
    - Visiting fibonacci page
    - Going to and from home page
    - Visiting the /posts page
4. Convert the HAR files individually in `recorder.bat`
5. Run all with `gatling.bat`
Results: (**IMG**)
Changing the measurements: 


As you can see, increasing the number of users severely impacts the performance of the app. In order to combat this, autoscaling groups and load balancers are used when setting up the app (***link to terraform and AWS intro***).


---

## What should we be monitoring about our app?
### Internet Facing vs Internal
Internet facing --> RAM CPU load remaining disk space network load
Network traffic, CPU, etc. Automate reactions to situations

## Autoscaling Policies
The problem with autoscaling is that you will get charged for the max no. of instances that spin up --> there is need for a policy for min/max traffic load.

When creating an autoscaling group we provide a min and max no. of instances. When autoscaling kicks in and new instances spin up for the app. The load balancer attached to IG and VPC then balances node between instances. The load balancer redirectes traffic to active instances so no instance gets overwhelmed.

The autoscaling group automatically adjusts computaional resources when needed to, but it does not automatically reduce the resources, which is why we need to create a policy for this.

---

# CloudWatch

Part of the **AUTOMATION SERIES**: CW highlighted

**DIAGRAM FOR AUTOMATION W GATLING, AWS, CW, S3, DOCKER, JENKINS w links to repos**

**DIAGRAM FOR CW AND AUTOSCALING**
CW triggers event after observing the traffic
this is make sure user doesnt notice change in load
inastnace attached to autoscaling group

## Scaling Policies


## AWS Simple Notification Service (SNS)

### A2A
### A2P

## AWS Simple Queue Service (SQS)

