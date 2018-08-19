```bash
# MOVE
gg #first line
G #last line 
1234G #jump to line 1234
0 #head of a line
^ #first un-blank character of a line
$ #tail of a line
H # move left
J # move above
K # move down
L # move right
```

```shell
# SEARCH
n # repeat and search down
N # repeat and search up
q/ # open a history window, you can vim a line of       it and enter to perform it
```

```shell
# COPY & PASTE
v # select character
V # select whole line
ctrl v # select block, move cursor to the end of what you want to cut or copy
d # cut, stand for delete in vim
y # copy, stand for yank in vim
p # paste after cursor
cap p # paste before cursor
```

