Our first lab for CSE 15L was interesting. Let me share with you what we did! 

# Setting up our CSE 15L accounts
Firstly we set up our remote course accounts. To set up our CSE 15L accounts, we visit [this site](https://sdacs.ucsd.edu/~icc/index.php]). Given the prompt, insert the last name and student ID at the bottom of the page to set the account password. You can also look up your account username using the account lookup, which would give you your username in the format *cs15lwi23XX*. When it's the first time the account is logged in, the website will prompt the user to reset password. 

<img width = "800" alt="Screenshot when logged in" src="https://user-images.githubusercontent.com/83614302/214489565-0f0e09f5-ce4b-4f51-a2c8-d8d47f8ff474.jpeg">


The chosen password must follow certain rules given. You can also use the randomly generated sequence of characters and symbols (but remember to note that password down). It is also worth remembering to tick the checkbox which prevents the password from being changed from the normal school account. 

For a step-by-step tutorial on how to change your password, see [here](https://docs.google.com/document/d/1hs7CyQeh-MdUfM9uv99i8tqfneos6Y8bDU0uhn1wqho/edit). 

# Installing VS Code
<img width="1000" alt="Screenshot of VSCode" src="https://user-images.githubusercontent.com/83614302/211950659-fa783185-dfa3-4047-8922-bd1e50cdd238.png">

Next, we were instructed to install visual studio code, git for windows and bash for windows. Since, I had already installed VS Code previously, I did not have to perform this task. Since Macs have git and bash built-in, I did not have to install git and bash. See below for download links for future reference. 

[VS Code Download](https://code.visualstudio.com/) (Mac or Windows)

[Git for Windows Download](https://code.visualstudio.com/)

[Instructions for downloading Bash for Windows](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal/50527994#50527994)

[Bash for Windows Download](https://git-scm.com/download/win)

I proceeded to opening a new window on VS Code and opened the terminal. To do this, open Visual Studio Code, find "Terminal" at the top of the screen, then on the drop-down menu, click "New Terminal". It should look like something like the following.

<img width="280" alt="Screenshot of vscode terminal" src="https://user-images.githubusercontent.com/83614302/214486054-63ffb90d-14fd-4c43-b07c-3be1bc55fa4f.png">

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

<img width="550" alt="Schermata 2023-01-11 alle 17 00 04" src="https://user-images.githubusercontent.com/83614302/211950775-9d068b5f-2b20-40f2-aa81-d7d4d05a0bdf.png">


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
This lab was enjoyable as I learnt how to access the course account remotely on my own laptop and to navigate it, which will be very helpful for future work!
