
                                           * PARSING DATA IN BASH *

      Parsing, syntax analysis, or syntactic analysis is the process of analysing a string of symbols,
      either in natural language, computer languages or data structures, conforming to the rules of a
      formal grammar. In the follow examples we will use the UNIX 'ifconfig' command as example.

![pic](http://i64.tinypic.com/205qy50.png)

      The 'ifconfig wlan0' presents many information about the current interface in use, but lets say
      we only need to 'extract' the ip address from ifconfig command and store that info into one bash
      variable (for scripting) or into a logfile for later review, its when 'parsing' its helpfull ..
      This article will show easy examples using bash commands like: GREP, CAT, AWK, CUT, HEAD, TAIL, etc.


<br /><br />

### Article Glossario
[1] [Parsing data with GREP](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#grep)<br />
[2] [Parsing data with HEAD](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#head)<br />
[3] [Parsing data with TAIL](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#tail)<br />
[4] [Parsing data with CAT](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#cat)<br />
[5] [Parsing data with AWK](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#awk)<br />
[6] [Parsing data with CUT](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#cut)<br />
[7] [Parsing data with TR](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#tr)<br />
[8] [Parsing data with SED](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#sed)<br />


---

<br /><br />

### GREP

      grep searches the input files or commands for lines containing a match to a given pattern list.
      When it finds a match in a line, it copies the line to standard output (by default), or whatever
      other sort of output you have requested with grep command options (switch's).

<br />

- Print **All** the lines that contains the **'inet'** expression<br />

      ifconfig wlan0 | grep "inet"

![pic](http://i66.tinypic.com/2uoi0sz.png)

- Colorize the **matching** expression<br />

      ifconfig wlan0 | grep "inet" --color=auto

![pic](http://i67.tinypic.com/vht43l.png)


- Print only the lines with **'inet'** in them (only perfect matches)<br />

      ifconfig wlan0 | grep -w "inet"

![pic](http://i66.tinypic.com/25kraxc.png)

- Print only the **1º line** containing the **'inet'** expression<br />

      ifconfig wlan0 | grep -m 1 "inet"

![pic](http://i67.tinypic.com/95sy91.png)

- print only the matching expression (**not the line**)<br />

      ifconfig wlan0 | grep -o "inet6"

![pic](http://i68.tinypic.com/2vijvhx.png)
**HINT:** grep -o switch can be used to **check** if the suplied expression exists (in scripting)<br /><br />


- **Invert** the sence of matching (**delete all matching lines** that contains the expression)<br />

      ifconfig wlan0 | grep -v "inet"

![pic](http://i67.tinypic.com/2upeloz.png)


<br /><br />

                                               * EXERCISES *

**EXERCISE1:** Print only the line that contains **'RX packets'** expression<br />
With everything we have learn until now, how do you print only the line that contains the RX packets expression?<br />

**EXERCISE2:** Print only the line that contains your **'mac address'**<br />
With everything we have learn until now, how do you print only the line that contains your mac address?<br />

[?] [exercise1 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise1)<br />
[?] [exercise2 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise2)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### HEAD

      By default, ‘head’ command reads the first 10 lines of the file. If you want to read more or less
      than 10 lines from the beginning of the file then you have to use ‘-n’ option with ‘head’ command.
      In the next example we are using 'grep' command to displays all lines that contains the 'X' expression.

![pic](http://i68.tinypic.com/nfr43c.png)

<br />

- Print the **'first line'** that contains the expression **'X'** using **head -n** switch<br />

      ifconfig wlan0 | grep "X" | head -n 1

![pic](http://i66.tinypic.com/2wbz22b.png)

- Print the first **'two lines'** that contains the expression **'X'** using **head -n** switch<br />

      ifconfig wlan0 | grep "X" | head -n 2

![pic](http://i66.tinypic.com/15hna6h.png)

<br /><br />

                                               * EXERCISES *

**EXERCISE3:** Print the **4 lines** that contains the **'X'** expression using **head -n** switch<br />

[?] [exercise3 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise3)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### TAIL

      By default, ‘tail’ command reads the last 10 lines of the file. If you want to read more or less
      than 10 lines from the ending of the file then you have to use ‘-n’ option with ‘tail’ command.
      In the next example we are using 'grep' command to displays all lines that contains the 'X' expression.

![pic](http://i68.tinypic.com/nfr43c.png)

<br />

- Grab the first **'two lines'** (head -n 2) that contains the expression **'X'** and print the **last line** (tail -n 1)<br />

      ifconfig wlan0 | grep "X" | head -n 2 | tail -n 1

![pic](http://i65.tinypic.com/2nc14t5.png)

- Grab the first **'3 lines'** (head -n 3) that contains the expression **'X'** and print the **last line** (tail -n 1)<br />

      ifconfig wlan0 | grep "X" | head -n 3 | tail -n 1

![pic](http://i63.tinypic.com/2j29mab.png)

- Grab the first **'3 lines'** (head -n 3) that contains the expression **'X'** and print the **last two lines** (tail -n 2)<br />

      ifconfig wlan0 | grep "X" | head -n 3 | tail -n 2

![pic](http://i68.tinypic.com/2w4l0g8.png)
**HINT:** we are displaying the **last two lines** (tail -n 2) that **'head -n 3'** command have filter previously.<br /> 

<br /><br />

                                               * EXERCISES *

**EXERCISE4:** Print **only the line** that contains the **'TX errors'** expression with the help of **'tail -n'** switch<br />

[?] [exercise4 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise4)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### CAT

      cat is a standard Unix utility that reads files sequentially, writing them to standard output.
      The name is derived from its function to concatenate files. In this section we will use 'article'
      file to demonstrate parsing technincs. The demonstration file can be downloaded from the link above.

![pic](http://i65.tinypic.com/73mr1w.png)
[+] [demonstration file of 'parsing data in bash' (article demo file)](https://gist.github.com/r00t-3xp10it/c3f7cbf1ca73f8d7ce24d17af39738a8)

<br /><br />

- Read **article** file and print a line **[ only if ]:** the whole line matches your suppied regex<br />

      cat article | grep -x "This line will be displayed .."

![pic](http://i68.tinypic.com/34zzn08.png)

- Print **all lines** that contains the **ERROR** expression<br />

      cat article | grep "ERROR"

![pic](http://i68.tinypic.com/znwor9.png)

- Store all **ERROR** lines from article file into another logfile<br />

      cat article | grep "ERROR" >> new_logfile.log

![pic](http://i66.tinypic.com/2a0nuhk.png)

<br /><br />

                                               * EXERCISES *

**EXERCISE5:** Write only the line that contains **192.168.1.69** expression into a new logfile<br />
With everything we have learn until now, how do you write only the line that contains the **192.168.1.69** expression?<br />

[?] [exercise5 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise5)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### AWK

      Awk breaks each line of input passed to it into fields. By default, a field is a string of consecutive
      characters delimited by whitespace, though there are options for changing this. Awk parses and operates
      on each separate field. This makes it ideal for handling large text files, logfiles or databases.

![pic](http://i64.tinypic.com/205qy50.png)

<br />

- Grab the **1º line** that contains the **'inet'** expression AND print the **2º field**<br />

      ifconfig wlan0 | grep -m 1 "inet" | awk {'print $2'}

![pic](http://i67.tinypic.com/118mypy.png)

- Grab the **1º line** that contains the **'inet'** expression AND print **1º field + 2º field**<br />

      ifconfig wlan0 | grep -m 1 "inet" | awk {'print $1,$2'}

![pic](http://i64.tinypic.com/fn4wsj.png)

- Grab the **1º line** that contains the **'inet'** expression AND print **3º field + 4º field**<br />

      ifconfig wlan0 | grep -m 1 "inet" | awk {'print $3,$4'}

![pic](http://i65.tinypic.com/15qxgz6.png)

<br />

- AWK -F switch (awk -F [ delimiter ])<br />

      Sometimes the separator its not space nor tab, in this situation we can use awk -F switch
      to chose our 'delimiter' char and print the field we want. In the next example we will
      extract the 2º field of our mac address using awk -F switch with (:) as delimiter char.

<br />

      ifconfig wlan0 | grep -w "ether" | awk {'print $2'} | awk -F: {'print $2'}

![pic](http://i67.tinypic.com/fvwk10.png)

- Store your IP address into one bash **variable** for later use (scripting)<br />

      parse_data=`ifconfig wlan0 | grep -m 1 "inet" | awk {'print $2'}`
      echo my ip: $parse_data

![pic](http://i68.tinypic.com/if5p8m.png)

<br /><br />

                                               * EXERCISES *

**EXERCISE6:** Extract only the string **:f629:** from your inet6 interface using **awk -F** switch<br />
![pic](http://i68.tinypic.com/slp79u.png)

[?] [exercise6 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise6)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### CUT

      The cut command in UNIX is a command for cutting out the sections from each line of files and writing
      the result to standard output. It can be used to cut parts of a line by byte position, character and field.
      Basically the cut command slices a line and extracts the text.

![pic](http://i64.tinypic.com/205qy50.png)

      In the follow examples we will use -c (char possition) or -d (delimiter) cut switchs to be habble
      to print on stdout the string we need. The -c switch allow us to print one character or a group of
      characters based on is possition in the line. And the -d switch allow us to chose a cut delimiter.
      Also remmenber that in delimiter use (cut -d) the empty space(s) counts as one character space.

<br />

- Grab the line that contains **'flags'** expression and print all char(s) starting in possition **18** until **49**<br />

      ifconfig wlan0 | grep -w "flags" | cut -c 18-49

![pic](http://i68.tinypic.com/fn4gnp.png)

- Grab the line that contains **'inet'** expression and print char(s) based on is **possition** in the line<br />

      ifconfig wlan0 | grep -w "inet" | cut -c 10,11,12,56,57,59

![pic](http://i63.tinypic.com/21afo1g.png)

<br /><br />

                          * This next section will describe the use of cut -d switch *

      IP address parsed    :    192        .        168        .         1         .        71
      Delimiter description: [field 1][delimiter][field 2][delimiter][field 3][delimiter][field 4][field 5]

<br />

- Grab the line that contains **'inet'** expression, print **2º field** (awk) and print **1º field** of delimiter<br />

      ifconfig wlan0 | grep -w "inet" | awk {'print $2'} | cut -d '.' -f1

![pic](http://i66.tinypic.com/dzcgg7.png)


- Grab the line that contains **'inet'** expression, print **2º field** (awk) and print **2º field** of delimiter<br />

      ifconfig wlan0 | grep -w "inet" | awk {'print $2'} | cut -d '.' -f2

![pic](http://i65.tinypic.com/23iwbpk.png)


- Grab the line that contains **'inet'** expression, print **2º field** (awk) and print from **1º to 3º field** of delimiter<br />

      ifconfig wlan0 | grep -w "inet" | awk {'print $2'} | cut -d '.' -f1,2,3

![pic](http://i68.tinypic.com/ixeh61.png)

<br /><br />

                                               * EXERCISES *

**EXERCISE7:** Extract only the string **prefix** from your inet6 interface using **cut -c** switch<br />

[?] [exercise7 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise7)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### TR

      tr is an UNIX utility for translating, or deleting, or squeezing repeated characters.
      It will read from STDIN and write to STDOUT. In the next example we are using 'ifconfig'
      command and 'tr' to delete numbers, leters, expressions, empty spaces and tab spaces.

![pic](http://i64.tinypic.com/205qy50.png)

<br />


- **Delete** from stdout characters ('5' and '.') using **'tr -d'** switch<br />

      ifconfig wlan0 | tr -d '5' | tr -d '.'

![pic](http://i64.tinypic.com/rktvmd.png)

- **'tr'** can also be used to remove **'new line paragraphs'** using \n (paragraph)<br />

      ifconfig wlan0 | tr -d '\n'

![pic](http://i63.tinypic.com/rc7z49.png)

- Delete **empty spaces** between lines (tr -d ' ')<br />

      ifconfig wlan0 | tr -d ' '

![pic](http://i65.tinypic.com/8y6hph.png)

- Replace (tr -s) **'empty spaces'** between lines by a **'tab space'**<br />

      ifconfig wlan0 | tr -s ' ' '\t'

![pic](http://i63.tinypic.com/2isxzjc.png)

- Replace (tr -s) **'inet'** between lines by **'HALO'**<br />

      ifconfig wlan0 | tr -s 'inet' 'HALO'

![pic](http://i67.tinypic.com/24wzrro.png)<br />
**HINT:** The word to be substitute must match the same number of chars that the one beeing substitued

<br />

- Delete **'new line paragraphs'** (tr -d '\n') and replace (tr -s '\t' ' ') **'tab spaces'** by nothing<br />

      ifconfig wlan0 | tr -d '\n' | tr -s '\t' ' '

![pic](http://i63.tinypic.com/24enepv.png)

- Delete **'new line paragraphs'**, replace **'tab spaces'** by nothing and **delete empty spaces**<br />

      ifconfig wlan0 | tr -d '\n' | tr -s '\t' ' ' | tr -d ' '

![pic](http://i65.tinypic.com/2rp2p9g.png)

<br /><br />

                                               * EXERCISES *

**EXERCISE8:** Delete **All** this chars: [.][:][,][<][>][ ( ][ ) ][=] and **empty spaces** from ifconfig wlan0 stdout ..<br />


[?] [exercise8 soluction](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#exercise8)<br />
[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### SED

      sed is a stream editor. A stream editor is used to perform basic text transformations on an input stream
      (a file, or input from a pipeline). While in some ways similar to an editor which permits scripted edits
      (such as ed), sed works by making only one pass over the input(s), and is consequently more efficient.
      But it is sed's ability to filter text in a pipeline which distinguishes it from other types of editors.

![pic](http://i64.tinypic.com/205qy50.png)

                         sed [switch] '[flag]/[old text]/[new text]/[flag]' [filename]

                                sed -i    -   save changes into file
                                sed -e    -   sed regex switch
                                sed s/    -   sed substitution flag
                                sed /g    -   sed substitution global flag
                                sed '2d'  -   sed delete line possition flag
                                sed '2s/' -   sed substitution line possition flag

<br /><br />

- Replace **'team'** by **'RedTeam'** from stdout<br />

      echo "Wellcome to SSA team" | sed 's/team/RedTeam/'

![pic](http://i67.tinypic.com/2ngbvr6.png)

- Replace [s/] **All** [/g] occurencies of **'inet'** by **'obfuscated'** from stdout<br />
 
      ifconfig wlan0 | sed 's/inet/obfuscated/g'

![pic](http://i64.tinypic.com/n70dxz.png)

- Delete the **2º line** display from stdout<br />

      ifconfig wlan0 | sed '2d'

![pic](http://i67.tinypic.com/4idfya.png)

- Delete the **1º and 4º line** displays from stdout<br />

      ifconfig wlan0 | sed '1d;4d'

![pic](http://i68.tinypic.com/23ubgus.png)

- Delete the **1º line** and from **5º until 8º line** displays from stdout<br />

      ifconfig wlan0 | sed '1d;5,8d'

![pic](http://i68.tinypic.com/4grrwp.png)

- Execute **multiple** sed commands or **regex** using sed -e switch<br />

      ifconfig wlan0 | sed -e 's/netmask/obfuscated/; s/inet/cia/g; s/bytes/badsum/g'

![pic](http://i65.tinypic.com/9qkc9e.png)

<br /><br />

                                     * sed file system operations *

![pic](http://i65.tinypic.com/73mr1w.png)

<br />

- Replace **'will'** in 2º line by **'will not'** from stdout<br />
 
      cat article | sed '2s/will/will not/'

- Delete lines **2º and 3º** from stdout<br />

      cat article | sed '2,4d'

- Delete **2º line** from article file and **save** file [-i]<br />

      cat article | sed -i '2d' article

- Delete **3º and 4º line** from article file and **save** file [-i]<br />

      cat article | sed -i '3d;4d' article

<br /><br />

      #!/bin/sh
      myvar="10101010"
      echo "Shantys variable is: $myvar"
      pause 3

[Download 'test.sh' into your working directory (pwd)](https://gist.github.com/r00t-3xp10it/f78aa02026e25c407d8ec5fd92eaed9a)<br />

      # execute test.sh
      chmod +x test.sh && ./test.sh
      
      # Use SED -i to replace text inside test.sh
      sed -i 's/10101010/hello world/' test.sh

      # print and run test.sh
      cat test.sh && echo "" && ./test.sh

<br />

[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br />

### REGEX


- delete last 3 chars from string<br />

      v1=`ifconfig | grep "broadcast" | awk {'print $6'}`
      v2=`echo ${v1::-3}`
      echo $v2

![pic](http://i67.tinypic.com/2ypajyf.png)


- remove everything after the final [.]<br />

      IP="192.168.1.71"
      parse=`echo ${IP%.*}`
      echo $parse

![pic](http://i64.tinypic.com/2i1fuyw.png)

- check for empty variable declarations<br />

      var=""
      if [ -z "$var" ]; then
        echo "The variable declaration its empty .."
      else
        echo "Data: $var"
      fi


- check for NOT empty variable declarations<br />

      var="hello"
      if ! [ -z "$var" ]; then
        echo "The variable declaration its NOT empty .."
      else
        echo "The variable declaration its empty .."
      fi


- FOR loops<br />

      for i in 1 2 3 4 5
      do
      echo "Looping ... number $i" && sleep 1
      done

![pic](http://i64.tinypic.com/2a6qki8.png)


- join variable with text

      var=sun
      echo $varshine     # $varshine is undefined (empty string)
      echo ${var}shine   # displays the word "sunshine"
      echo ${var}spot    # displays the word "sunspot"

![pic](http://i64.tinypic.com/34njqc2.png)

[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />

---

<br /><br /><br /><br />

                                          * EXERCISES SOLUCTIONS *

### EXERCISE1:

![pic](http://i66.tinypic.com/28hziac.png)

### EXERCISE2:

![pic](http://i65.tinypic.com/2vcc12o.png)

### EXERCISE3:

![pic](http://i66.tinypic.com/jqhmoo.png)

### EXERCISE4:

![pic](http://i67.tinypic.com/2hwd2ls.png)

### EXERCISE5:

![pic](http://i63.tinypic.com/e64xs3.png)
![pic](http://i63.tinypic.com/24v0787.png)

### EXERCISE6:

![pic](http://i63.tinypic.com/dpbnmf.png)

### EXERCISE7:

![pic](http://i67.tinypic.com/978hs4.png)

### EXERCISE8:

![pic](http://i67.tinypic.com/2dbkmzq.png)

---

<br /><br /><br />

[0] [article glossario](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#article-glossario)<br />
[1] [Parsing data with GREP](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#grep)<br />
[2] [Parsing data with HEAD](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#head)<br />
[3] [Parsing data with TAIL](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#tail)<br />
[4] [Parsing data with CAT](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#cat)<br />
[5] [Parsing data with AWK](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#awk)<br />
[6] [Parsing data with CUT](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#cut)<br />
[7] [Parsing data with TR](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#tr)<br />
[8] [Parsing data with SED](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/bash/parsing_data_in_bash.md#sed)<br />

---

<br /><br />

**Special Thanks:** shanty damayanti,
#### SuspiciousShellActivity - RedTeam @2018
