## linux notes

##### 1. Find

```bash
find $dir -name $name
locate 
grep something <somefile # < is STDIN, > is STDOUT
grep -w word # match separate word
sudo lsof -iTCP -sTCP:LISTEN | grep mongo # find out port of what process is listening 
ls -d ???^[ABC]* # ? for a single character, [abc] for either a, b or c, ^ begin with something
ps -ef | grep mongo # find process
history 
!256 # history number and !num to re-exec it
```

##### 2. find out path

```bash
type $var
which $var
pwd
```

##### 3. pipe

```bash
ps -ef | grep mongo # find process
```

##### 4. Direct run remote cmd by ssh

```bash
ssh $remote_host "$bash_cmd"
```

##### 6. STDIN, STDOUT, STDERR

```bash
grep something <somefile
grep something <somefile >resultfile 2>errorfile

#Say you want to redirect both STDOUT and STDERR to the same file. Then you cannot do. This redirects STDOUT (1) to the ‘resultfile’ and tells STDERR (2) to send the output to what STDOUT is set to (also ‘resultfile’).
grep something >resultfile 2>&1
```

##### 7. count 

```bash
wc #Word count. Counts the bytes, words and lines. “wc -l” just outputs how many lines were counted.
head #Shows the first ten lines only. “head -50” shows the first 50 lines.
tail #Shows the last ten lines only. “tail -50” shows the last 50 lines. “tail -f” follows a certain file.
```

##### 8. chmod

```bash
# read 4, write 2, execute 1
# 7 = rwx, 6 = rw-, 5 = r-x, 4 = r--, 3 = -wx, 2 = -w-,1 = --x, 0 = ---
# a = all, u = user owner, g = group owner, o = other, 
chmod 540 file # user, group, other
chmod u+w file
```

##### 9. tar

```bash
tar -cvf name.tar /path/to/dir # compress
tar -xf name.tar # extrat file from tar
tar -xvzf name.tar.gz # unzip tar.gz
```

##### 10. tmux

```shell
tmux # open a new session
tmux new -s myname
tmux a  #  (or at, or attach)
tmux a -t myname
tmux ls
tmux kill-session -t myname
```

