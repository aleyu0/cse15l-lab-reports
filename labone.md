Our first lab for CSE 15L was interesting. Let me share with you what we did! 

# Meeting our peers
Firstly, we sat at our desks and met our peers. We introduced ourselves and had a quick conversation about people's majors and thoughts about our new course, CSE 15L. It was interesting to see my peers coming from different backgrounds and having different majors, and we still end up in the same course, and in the same lab session. 

# Setting up our CSE 15L accounts
We then moved on to setting up our accounts on the system which allows us to access the school servers remotely. The password changing website was buggy and required multiple trials, but we got there at the end. *Although I did change the my school account password...*

# Installing VS Code
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

```
Last login: Sun Jan  2 14:03:05 2022 from 107-217-10-235.lightspeed.sndgca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lwi23XX, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   23:25:01   0  0.08,  0.17,  0.11
ieng6-202   23:25:01   1  0.09,  0.15,  0.11
ieng6-203   23:25:01   1  0.08,  0.15,  0.11

Sun Jan 02, 2022 11:28pm - Prepping cs15lwi23
```

Voilà, we're in. 

# Testing out simple commands
Now that we're in for the first time, we can finally test out the commands that we were introduced to in this morning's lecture. These include:
* `cat <path 1> <path 2>` = prints out the contents of one or more files given by the paths
* `ls <path>` = lists all the files and folders in the given path
* `pwd` = "Print working directory" displays the current working directory
* `cd <path>` = "Change Directory” Used to switch the current working directory to the given path

*
