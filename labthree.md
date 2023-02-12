# `Grep` commands
To find out what grep does, it would be helpful for us to ask for the manual in out command. So, after I have logged into my remote account through `ssh`, I asked for the manual through `man grep`. In this lab report, we will explore `-rl`, `-c`, `-n`, and `v` and use them in the the `./written_2` directory given from the skill demo data. 

## `grep -rl`
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

To prove this works, we can check the outputed file path.
```
$ cat written_2/travel_guides/berlitz2/Bahamas-History.txt
```
<img width="100%" alt="Screen Shot 2023-02-11 at 3 02 26 PM" src="https://user-images.githubusercontent.com/83614302/218284742-9a9d6f4e-9bd9-47f4-9391-7075f7a81641.png">

As you can see, Lucayans appears in this document as highlighted. 

We now try this command with a keyword that occurs in multiple files. 
```
grep -rl "Italy"
```
This would putput:
```
.git/index
written_2/non-fiction/OUP/Castro/chP.txt
written_2/non-fiction/OUP/Fletcher/ch2.txt
written_2/non-fiction/OUP/Fletcher/ch9.txt
written_2/non-fiction/OUP/Rybczynski/ch2.txt
written_2/travel_guides/berlitz1/HistoryFrance.txt
written_2/travel_guides/berlitz1/HistoryGreek.txt
written_2/travel_guides/berlitz1/HistoryIstanbul.txt
written_2/travel_guides/berlitz1/HistoryItaly.txt
written_2/travel_guides/berlitz1/HistoryMadeira.txt
written_2/travel_guides/berlitz1/HistoryMallorca.txt
written_2/travel_guides/berlitz1/IntroItaly.txt
written_2/travel_guides/berlitz1/IntroLasVegas.txt
written_2/travel_guides/berlitz1/WhatToItaly.txt
written_2/travel_guides/berlitz1/WhereToEgypt.txt
written_2/travel_guides/berlitz1/WhereToFWI.txt
written_2/travel_guides/berlitz1/WhereToFrance.txt
written_2/travel_guides/berlitz1/WhereToGreek.txt
written_2/travel_guides/berlitz1/WhereToIstanbul.txt
written_2/travel_guides/berlitz1/WhereToItaly.txt
written_2/travel_guides/berlitz1/WhereToMadrid.txt
written_2/travel_guides/berlitz2/Algarve-History.txt
written_2/travel_guides/berlitz2/Athens-History.txt
written_2/travel_guides/berlitz2/Athens-WhatToDo.txt
written_2/travel_guides/berlitz2/Barcelona-WhereToGo.txt
written_2/travel_guides/berlitz2/California-WhereToGo.txt
written_2/travel_guides/berlitz2/Canada-History.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
written_2/travel_guides/berlitz2/Costa-History.txt
written_2/travel_guides/berlitz2/CostaBlanca-History.txt
written_2/travel_guides/berlitz2/Crete-WhereToGo.txt
written_2/travel_guides/berlitz2/CstaBlanca-WhereToGo.txt
written_2/travel_guides/berlitz2/Paris-WhereToGo.txt
written_2/travel_guides/berlitz2/Portugal-History.txt
written_2/travel_guides/berlitz2/Portugal-WhatToDo.txt
```
If we wanted to inport these outputs into a `.txt` file, we simply add `> results.txt` at the end, which would create a file which includes the output. 

## `grep -rc`
* `grep -c` - `Suppress  normal  output;  instead  print  a  count of matching lines for each input file.  With the -v, --invert-match option (see below), count non-matching lines.  (-c is specified by POSIX.)` will output a number indicating the number of times a given pattern/keyword apprears in a file. We can extend this functionality to find the number of occurances of the a keyword in a directory by using `-rc`.

We can try this out by looking for the number of times the word "The" is mentioned in the file `ch1.txt`.
```
$ grep -c "The" ch1.txt
```
we get an output of `60`. 

We can also try to find how many times "The" is used in the `Berk` directory in different files. 
```
$ grep -rc "The" Berk/
```
and we get the following output
```
Berk/CH4.txt:66
Berk/ch1.txt:60
Berk/ch2.txt:67
Berk/ch7.txt:42
```
which indicates that "The" occurs in `ch1.txt` 60 times, in `ch2.txt` 67 times, in `CH4.txt` 66 times, and in `ch7.txt` 42 times.

## `grep -n`

