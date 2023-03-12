During the lab session in week 7, we performed a series of tasks with time restraint as we competed with other groups in our lab session. The tasks included the following:

1. Setup Delete any existing forks of the repository you have on your account
2. Setup Fork the repository
3. The real deal Start the timer!
4. Log into ieng6
5. Clone your fork of the repository from your Github account
6. Run the tests, demonstrating that they fail
7. Edit the code file to fix the failing test
8. Run the tests, demonstrating that they now succeed
9. Commit and push the resulting change to your Github account (you can pick any commit message!)

[Click here for the repository]([url](https://github.com/ucsd-cse15l-w23/lab7)).

Here is how someone who didn't cheat would complete the task:
1. Log into ieng6 using 
  * `ssh cs15lwi23aed@ieng6.ucsd.edu`
2. Clone your fork of the repository from your Github account 
  * `git clone <paste>` which would give this `git clone git@github.com:aleyu0/lab7.git`
3. Run the tests, demonstrating that they fail
  * `cd lab7` to enter the cloned repository
  * `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` achived by either copy pasting or using the <up> arrow to retrieve from history
  * `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` achived by either copy pasting or using the <up> arrow to retrieve from history
4.	Edit the code file to fix the failing test
  * `nano ListExample.java` to edit the java file
  * ctrl+w for search and edit the file
5.	Run the tests, demonstrating that they now succeed
  * `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` by using the <up> arrow
  * `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` by using the <up> arrow
6.	Commit and push the resulting change to your Github account
  * `git commit ListExamples.java -m “Updated”` to commit back to my branch
  * `git push` to push changed

As we found out, there was a way to speed this whole process, up by writing a bash script, which would perform all the tasks at one time, which reduces the time wasted typing out each command. 
 
