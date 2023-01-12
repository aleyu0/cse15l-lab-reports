Our first lab for CSE 15L was interesting. Let me share with you what we did! 

# Meeting our peers
Firstly, we sat at our desks and met our peers. We introduced ourselves and had a quick conversation about people's majors and thoughts about our new course, CSE 15L. It was interesting to see my peers coming from different backgrounds and having different majors, and we still end up in the same course, and in the same lab session. 

# Setting up our CSE 15L accounts
We then moved on to setting up our accounts on the system which allows us to access the school servers remotely. The password changing website was buggy and required multiple trials, but we got there at the end. *Although I did change the my school account password...*

# Installing VS Code
<img width="1470" alt="Schermata 2023-01-11 alle 15 30 10" src="https://user-images.githubusercontent.com/83614302/211950659-fa783185-dfa3-4047-8922-bd1e50cdd238.png">

Next, we were instructed to install visual studio code, git for windows and bash for windows. However, I had already installed VS Code previously, and since I use a Mac, I did not have to install git and bash. I proceded to opening a new window on VS Code and opened the terminal. 

# Accessing the course account remotely
Through the terminal, we logged into the course account. In order to do so, the following commands were used:

```
ssh cs15lwi23XX@ieng6.ucsd.edu
```
*the XX is replaced with our account username. 

The following text was shown as it was our first time accessing the server. 
```
⤇ ssh cs15lwi23XX@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Password:
```
We answered yes to the first prompt, and then entered our password that we set up previously for the password prompt. When everything goes well, we will see the following output:

<img width="618" alt="Schermata 2023-01-11 alle 17 00 04" src="https://user-images.githubusercontent.com/83614302/211950775-9d068b5f-2b20-40f2-aa81-d7d4d05a0bdf.png">


Voilà, we're in. 

# Testing out simple commands
Now that we're in for the first time, we can finally test out the commands that we were introduced to in this morning's lecture. These include:
* `cat <path 1> <path 2>` = prints out the contents of one or more files given by the paths
* `ls <path>` = lists all the files and folders in the given path
* `pwd` = "Print working directory" displays the current working directory
* `cd <path>` = "Change Directory” Used to switch the current working directory to the given path
* `mkdir` = make a new directory
* `..` = allows to go back directory
* `~` = returns to home directory

Using the above, we tried navigating the directories. 

<img width="405" alt="Schermata 2023-01-11 alle 17 00 57" src="https://user-images.githubusercontent.com/83614302/211950900-80351c6c-4b98-412f-86d2-f9d17b49f0d5.png">

We then logged out by typing `exit`.

# Conclusion
This lab was fun, and I learnt to access the course account remotely on my own laptop and to navigate it! 
