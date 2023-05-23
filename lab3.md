
# Lab 3 - Daniil Katulevskiy A17481234

## Search a path

Command:  

```bash
find <dir> -ipath "<path>"
```

Explanation:  
Will search for all the files and directories with corresponding path pattern.
`-ipath` options makes find command treat slashes and dots as path elements instead of regex characters.

Used source [2](https://ss64.com/bash/find.html)

Example 1:  

```bash
find . -ipath "*/911report/*"
```

```bash
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```

Example 2:  

```bash
find . -ipath "*/Alcohol_Problems/*"
```

```bash
./technical/government/Alcohol_Problems/Session2-PDF.txt
./technical/government/Alcohol_Problems/Session3-PDF.txt
./technical/government/Alcohol_Problems/DraftRecom-PDF.txt
./technical/government/Alcohol_Problems/Session4-PDF.txt
```

## Find file by content

Command:  

```bash
find <dir> -exec grep -Hi <words> {} \;
```

Explanation:  
Substitute `<dir>` with directory of file, `<words>` with words you want to search files for.
It will execute grep command on every found file. -H option for grep allows to pring out both, file name and line content that was found. -i option for grep allows for case-insensitive search. Thus, this function will output `filename: line content` for every line that has a matching word.

Used source [3](https://askubuntu.com/questions/924593/run-command-with-args-multiple-time)

Example 1:  

```bash
find . -ipath "*/Alcohol_Problems/*" -exec grep -Hi multi-center {} \;
```

```bash
./technical/government/Alcohol_Problems/Session2-PDF.txt:To determine the best of the available screens, a multi-center
./technical/government/Alcohol_Problems/DraftRecom-PDF.txt:about the need for a large, multi-center trial in EDs.
./technical/government/Alcohol_Problems/Session4-PDF.txt:interventions. In his multi-center study, interventionists felt
./technical/government/Alcohol_Problems/Session4-PDF.txt:they change practice. He thought a successful multi-center trial
./technical/government/Alcohol_Problems/Session4-PDF.txt:multi-center studies. He also believed that research should have
```

Example 2:

```bash
find . -ipath "*/911report/*" -exec grep -H SVTS {} \;
```

```bash
./technical/911report/chapter-13.5.txt:Cressey to CSG, Threat SVTS, July 23, 2001.
./technical/911report/chapter-13.5.txt:teleconference system (SVTS). Thus, it is unclear whether the attendees met
./technical/911report/chapter-13.5.txt:face-to-face at the White House or held their meeting remotely via SVTS.
./technical/911report/chapter-13.5.txt:note, CSG SVTS agenda, Jan. 31, 2000.
```

## Find files within certain depth

Command:  

```bash
find <dir> -maxdepth <depth>
```

Explanation:  
Command will find all files within the given depth `<depth>` in the directory `<dir>`.

Used sources [2](https://ss64.com/bash/find.html), [3](https://askubuntu.com/questions/924593/run-command-with-args-multiple-time)

Example 1:  

```bash
find ./technical -maxdepth 1
```

```bash
./technical
./technical/government
./technical/plos
./technical/biomed
./technical/911report
```

Example 2:  

```bash
find ./technical -maxdepth 2 -type d
```

```bash
./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/biomed
./technical/911report
```

## Find files older than

Command:  

```bash
find <dir> -mtime <sign><days>
```

Explanation:  
This command will find files modified within the provided time period. Directory is defined by `<dir>`, time period is defined by `<sign>` and `<days>`. Sign is either +, -, or nothing. If it is a +, it will search for files modified more than `<days>` ago. If sign is a -, it will search for files modified less than `<days>` ago. If there is no sign, it will search for files modified exactly `<days>` ago.

Used source [1](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/#), [2](https://ss64.com/bash/find.html)

Example 1:  

```bash
find ./technical/911report -mtime +10
```

```bash
./technical/911report
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```

Example 2:  

```bash
find ./technical/911report -mtime -12
```

```bash
./technical/911report
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```

## Sources used

1. [`find` command arguments (geeksforgeeks)](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/#)
2. [Manual page (ss64)](https://ss64.com/bash/find.html)
3. [Xargs info (askubuntu)](https://askubuntu.com/questions/924593/run-command-with-args-multiple-time)
