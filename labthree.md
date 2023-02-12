# `Grep` commands
To find out what grep does, it would be helpful for us to ask for the manual in out command. So, after I have logged into my remote account through `ssh`, I asked for the manual through `man grep`. In this lab report, we will explore `-l`, `-c`, `-n`, and `-v` and use them in the the `./written_2` directory given from the skill demo data. 

## `grep -l`
* `grep -l` - `Suppress  normal  output;  instead  print the name of each input file from which output would normally have been printed.  The scanning will stop on the first match.  (-l is specified by POSIX.)` essentially lists all of the matched produced by the other command.
* `grep -r` - `Read all files under each directory, recursively, following symbolic links only if they are on the command line.  This is equivalent to the -d recurse option.`

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

## `grep -c`
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
* `grep -n` - `Prefix each line of output with the 1-based line number within its input file.  (-n is specified by POSIX.)` displays the number of the lines in which the given pattern/keyword is found in a file. 

Let's test this out by searching for the word "heritage" in the `chA.txt` in the `Castro/` directory/ 
```
$ grep -n "heritage" chA.txt 
```
We will get the following output: 
```
19:La Adelita is more than a romantic image to modern-day Chicanas. She continues to symbolize feminine independence, integrity, the fight for justice, and a proud heritage. Because the major influx of Mexican immigration into the United States was during the Mexican Revolution, many Chicanos and Chicanas grew up hearing stories about soldaderas and La Adelita from relatives, parents, and grandparents. In the late 1960s Chicanas who joined the Brown Berets de Aztlán, a political pseudomilitary youth group, often dressed as Adelitas, wearing rebozos (shawls) and bandoliers crisscrossed over their chests.
107:Mexicans were a majority through most of the nineteenth century, and Tucson had a bicultural spirit that was unique in the Southwest. A Mexican middle class ran some of the largest businesses, held political offices, became artists or intellectuals, funded private and public education, and created a prosperous Mexican society envied by other communities of the Southwest, with elegant theaters like the Teatro Carmen and Spanish-language newspapers. Tucson’s proximity to Mexico, especially Sonora, permitted Tucsonenses to remain close to their Mexican heritage. According to Thomas Sheridan, “This Mexican elite represented a local florescence of Latin American civilization in Arizona, its society and culture linking Tucson with the finest traditions of both Mexico and Spain” (3). Although there was a strong Mexican middle class, many Chicanos were working class, such as butchers, barbers, and later railroad workers. The railroad arrived in southern Arizona on March 20, 1880, and this changed society in Tucson forever.
```
Showing that the word is is present on line 19 and 107. 

We can also apply the recursive search to this command, to search for a keyword in files within directories, and grep print find the file and line that those keywords are mentioned. 

Let's try looking for the word "money" in the entire `Castro/` directory.
```
$ grep -rn "money" Castro/
```
which outputs 
```
Castro/chL.txt:42:Cruising involves driving very slowly up and down city streets, such as Mission Street in San Francisco, Whittier Boulevard in Los Angeles, and King and Story Roads in San Jose, California. The objective of cruising is to socialize, to see and be seen, to give others the opportunity to admire one’s car and to admire the other cars; consequently the driving must be very slow, muy despacito. Driving a great customized car, beautifully painted, is a unique experience for the low rider. Cruising slowly and smoothly, sitting low in the driver’s seat, glancing out at the street, nodding the head slightly when being recognized, all these make up an experience only a Chicano low rider who has invested lots of time and money in his car can appreciate. Cruising is often compared to the custom of promenading around a plaza, referred to as el paseo in many Latin American and Mexican cities. In this sense, the low-rider car becomes a cultural vehicle, as represented by the artist Gilbert Lujan in his series titled “Cultural Vehicles.”
Castro/chP.txt:62:A custom, often expressed only after it occurs, of giving a little extra when making a transaction or closing a bargain. For instance, when buying candy, the vendor may add one extra piece, de pilón, to surprise and make a child happy. John Bourke writes about an ancient custom in Mexico still used in the late nineteenth century: a merchant kept a tin cylinder for each customer, and after each purchase he’d drop a bean into it. After the total number of beans reached sixteen or eighteen, the customer was given six cents in money or goods. This was the pilón, a type of dividend given to the client for purchasing from the same merchant.
```
showing us that the word "money" can be found in `chL.txt` on line 42 and `chP.txt` on line 62.

## `grep -v`
* `grep -v` - `Invert the sense of matching, to select non-matching lines.  (-v is specified by POSIX.)`, will print out the lines that do not include the specified keyword/pattern. 

We can try to look for a line that doesn't include a space in `ch1.txt`:
```
$ grep -v " " ch1.txt
```
this will print out:
```




“Yes.”


```
Notice how it doesn't return the line number anymore, but instead only the contents of that line. We have got a bunch of returns (empty lines) and one line that only says `"Yes."`. We can ask for the line number by changed the `-v` to `-vn`:
```
$ grep -vn " " ch1.txt
```
giving us:
```
1:
2:
3:
4:
61:“Yes.”
146:
147:
148:
```
this way we know that lines 1, 2, 3, 4, 146, 147 and 148 are empty lines and the line with one single word is located on line 61. 

#Sources
For this lab report, I used the bash manual through `man grep`, the CSE 15L website, and the GeekforGeeks website. In addition, some information were provided by ChatGPT. All commands were tested on the ieng6 remote server. The data in which the commands were tested (`written_2/` directory) was provided by https://anc.org/data/oanc/download/, a free and open corpus of English text samples.
