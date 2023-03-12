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

[Click here for the repository](https://github.com/ucsd-cse15l-w23/lab7).

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
 
[See lab report 4 for more details.](https://aleyu0.github.io/cse15l-lab-reports/labfour.html)

As we found out, there was a way to speed this whole process, up by writing a bash script, which would perform all the tasks at one time, which reduces the time wasted typing out each command. 
Using chat, GPT, I was able to write a bash script, which would do all of the above processes and one go. All I would need to do is to save the bash script `task.sh` in the repository on the ieng6 server, then run `task.sh` in bash.
```
#!/bin/bash

# Log into ieng6
ssh cs15lwi23aed@ieng6.ucsd.edu

# Clone the forked repository from GitHub
git clone git@github.com:aleyu0/lab7.git

# Change to the cloned directory
cd lab7

# Run the tests and demonstrate that they fail
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples

# Overwrite ListExamples.java to fix the failing test
echo "import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
}
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }
}" > ListExamples.java

# Run the tests and demonstrate that they now succeed
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples

# Commit and push the changes to GitHub
git add ListExamples.java
git commit -m "Updated ListExamples.java"
git push
```
The only difference made from a bad script instead of manually, doing the tasks, would be when editing the ListExample.java file, where the basket will override the file with the text, whilst when doing it manually, it will require a text editor and going through the code to find the error.

Alternatively, there is another method in which the other group used, which was to write a one line command, which includes all of the commands needed. 
```
ssh cs15lwi23aed@ieng6.ucsd.edu && git clone git@github.com:aleyu0/lab7.git && cd lab7 && javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples && echo -e "import java.util.ArrayList;\nimport java.util.List;\n\ninterface StringChecker { boolean checkString(String s); }\n\nclass ListExamples {\n\n // Returns a new list that has all the elements of the input list for which\n // the StringChecker returns true, and not the elements that return false, in\n // the same order they appeared in the input list;\n static List<String> filter(List<String> list, StringChecker sc) {\n List<String> result = new ArrayList<>();\n for(String s: list) {\n if(sc.checkString(s)) {\n result.add(0, s);\n }\n }\n return result;\n }\n\n // Takes two sorted list of strings (so "a" appears before "b" and so on),\n // and return a new list that has all the strings in both list in sorted order.\n static List<String> merge(List<String> list1, List<String> list2) {\n List<String> result = new ArrayList<>();\n int index1 = 0, index2 = 0;\n while(index1 < list1.size() && index2 < list2.size()) {\n if(list1.get(index1).compareTo(list2.get(index2)) < 0) {\n result.add(list1.get(index1));\n index1 += 1;\n }\n else {\n result.add(list2.get(index2));\n index2 += 1;\n }\n}\n while(index1 < list1.size()) {\n result.add(list1.get(index1));\n index1 += 1;\n }\n while(index2 < list2.size()) {\n result.add(list2.get(index2));\n index2 += 1;\n }\n return result;\n }\n\n\n}" > ListExamples.java && javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples && git commit ListExamples.java -m "Updated" && git push
```
     
Overall, I enjoyed this live because competition is fun.
