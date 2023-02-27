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
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
```
<img width="100%" alt="Screen Shot 2023-02-26 at 20 32 38" src="https://user-images.githubusercontent.com/83614302/221474870-ef5b0e51-aae4-4983-85fe-d91762ddfb9e.png">

As you can see, there is one failure.

## Edit the code file to fix the failing test
We can go to the text editor built-in to bash `nano ListExamples.java`

<img width="50%" alt="Screen Shot 2023-02-26 at 20 34 37" src="https://user-images.githubusercontent.com/83614302/221475128-9019d6d4-d245-41d5-8713-b86525b8c49c.png">

We would usually look for the bug, but since we know what the bug is, we can simple do `<control>+w` and input `while(index2 < list2.size()) {`. This will set our cursor near the position we need to be. We can then use arrow keys `<down>``<down>``<right>``<right>``<right>``<right>``<right>``<right>``<right>``<right>`. 
Press the `<backspace>` one time and type `2`. 

<img width="50%" alt="Screen Shot 2023-02-26 at 20 40 24" src="https://user-images.githubusercontent.com/83614302/221475809-f8aaeb6d-e56a-4c1e-8027-8a542024c1ef.png">

Now to save, we use `<control>+x`. When prompted, press `y`. The press `<enter>`

<img width="50%" alt="Screen Shot 2023-02-26 at 20 42 17" src="https://user-images.githubusercontent.com/83614302/221476054-a26a36de-ea32-45be-99a5-244d536c64ee.png">

This would bring you back to the original terminal. 

## Run the tests, demonstrating that they now succeed
To test the code, we compile again. Since we compiled before we can just use the arrowkeys `<up>``<up>``<up>``<enter>`. The to run test, do the same thing: `<up>``<up>``<up>``<enter>`. This would give us the expected output of all tests passed. 

<img width="100%" alt="Screen Shot 2023-02-26 at 20 44 11" src="https://user-images.githubusercontent.com/83614302/221476289-d2a499d3-81bb-46c8-b50f-8567cbcbcd8c.png">

## Commit and push the resulting change to your Github account
Now, to commit, we will enter `git commit ListExample.java -m "Updated"`. To push the commit, we simple enter `git push`.

<img width="100%" alt="Screen Shot 2023-02-26 at 20 46 55" src="https://user-images.githubusercontent.com/83614302/221476625-f2ee1ee9-a6c7-41c7-b231-a35636907151.png">

We can check if we did this correctly by going onto github and refreshing the fork page. We can see that our code if not one commit ahead of the original branch. 

<img width="100%" alt="Screen Shot 2023-02-26 at 20 48 34" src="https://user-images.githubusercontent.com/83614302/221476812-31a64d80-d3f1-44d2-8c83-b3088571bd13.png">

We can also see that our code has been updated. 

<img width="100%" alt="Screen Shot 2023-02-26 at 20 49 00" src="https://user-images.githubusercontent.com/83614302/221476857-f494ea91-efdc-42e6-8c92-e766813f3cc4.png">

