## linux notes

##### 1. Find

```bash
find $dir -name $name
grep something <somefile # < is STDIN, > is STDOUT
```

##### 2. find out path

```bash
type $var
which $var
pwd
```

##### 3. pipe

```bash
# find process
ps -a | grep $name
```

##### 4. Direct run remote cmd by ssh

```bash
ssh $remote_host "$bash_cmd"
```

##### 5. tmux and screen cmd

![Screen Shot 2018-08-14 at 12.12.12 AM](/Users/kai/Desktop/Screen Shot 2018-08-14 at 12.12.12 AM.png)

##### 6. STDIN, STDOUT, STDERR

```bash
grep something <somefile
grep something <somefile >resultfile 2>errorfile

#Say you want to redirect both STDOUT and STDERR to the same file. Then you cannot do. This redirects STDOUT (1) to the ‘resultfile’ and tells STDERR (2) to send the output to what STDOUT is set to (also ‘resultfile’).
grep something >resultfile 2>&1
```

##### 7. Sort, wc, awk, less, head, tail

```bash
grep
#Filters out lines with certain search words. “grep -v” searches for all lines that do not contain the search word.

sort
#Sort the output alphabetically (needs to wait until EOF before doing its work). “sort -n” sorts numerically. “sort -u” filters out duplicate lines.usel

wc
#Word count. Counts the bytes, words and lines. “wc -l” just outputs how many lines were counted.

awk
#A sophisticated language (similar to Perl) that can be used to do something with every line. “awk ‘{print $3}'” outputs the third column of every line.

sed (stream editor)
#A search/replace tool to change something in every line.

less
#Useful at the end of a pipe. Allows you to browse through the output one page at a time. (“less” refers to a similar but less capable tool called “more” that allowed you to see the first page and then press ‘Space’ to view ‘more’.)

head
#Shows the first ten lines only. “head -50” shows the first 50 lines.

tail
#Shows the last ten lines only. “tail -50” shows the last 50 lines. “tail -f” follows a certain file.
```

