# Lab Report 4

## Log into ieng6 server
On bash enter `ssh cs15lwi23xyz@ieng6.ucsd.edu`
Since we already se out computer as a trusted device when we set up the SSH keys, we do not need to enter the password.

<img width="50%" alt="Screen Shot 2023-02-26 at 19 58 12" src="https://user-images.githubusercontent.com/83614302/221471046-f50edb57-5108-4bd8-8ce8-5a928bdc724d.png">

## Clone your fork of the repository from your Github account
To clone our repository, we first go the forked repository on Github. Click on the green `Code` button, then `ssh`. We copy this address. 

<img width="100%" alt="Screen Shot 2023-02-26 at 20 26 33" src="https://user-images.githubusercontent.com/83614302/221474220-8c7e8545-4434-405d-b756-6a9024097348.png">

So now we enter `git clone git@github.com:aleyu0/lab7.git` in bash.

## Run the tests demonstrating that they fail
We now change our directory the cloned directory. `cd lab7`.

To perform the test, we need to compile the tester file and implementation files using
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
```
and then run the test using 
```
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples
```


## Edit the code file to fix the failing test

## Run the tests, demonstrating that they now succeed

## Commit and push the resulting change to your Github account
