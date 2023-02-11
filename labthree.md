# `Grep` commands
To find out what grep does, it would be helpful for us to ask for the manual in out command. So, after I have logged into my remote account through `ssh`, I asked for the manual through `man grep`. In this lab report, we will explore `-rl`, `-c`, `-n`, and `v` and use them in the the `./written_2` directory given from the skill demo data. 

#`grep -rl`
* `-l` - `Suppress  normal  output;  instead  print the name of each input file from which output would normally have been printed.  The scanning will stop on the first match.  (-l is specified by POSIX.)` essentially lists all of the matched produced by the other command.
* `-r` - `Read all files under each directory, recursively, following symbolic links only if they are on the command line.  This is equivalent to the -d recurse option.`

We use these two commands together as `-rl` so that that we recusrsively search for a pattern within the files in the subdirectories it is given. When grep finds, the files with the corresponding pattern, it will print out the list of the file paths. 

We are now going to try to use this with our data set. Let's try to identify any files that contain the keyword "Lucayans" in our directory.
```
$ grep -rl "Lucayans"
```
Grep will finds all the matches and outputs
```
written_2/travel_guides/berlitz2/Bahamas-History.txt
```
