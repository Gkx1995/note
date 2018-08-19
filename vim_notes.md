```bash
# MOVE
gg #first line
G #last line 
1234G #jump to line 1234
0 #head of a line
^ #first un-blank character of a line
$ #tail of a line
h # move left
j # move down
k # move above
l # move right
b or B # move to beginning of previous word
e or E # move to end of next word
) or ( # move forward/backward one sentence
} or { # move forward/backward one paragraph
```

```shell
# SEARCH
n, N # next/previous search
q/ # open a history window, you can edit a line of it and enter to perform it
/ , ? # forward/backword search
:1,10s/pattern/replace # search and replace the first match of each line in the first 10 line
:1,10s/pattern/replace/g # search and replace globally
:1,10s/pattern/replace/i # case-insensitive search and replace
```

```shell
# COPY & PASTE
v # select character
V # select whole line
ctrl v # select block, move cursor to the end of what you want to cut or copy
d # cut, stand for delete in vim

y # copy, stand for yank in vim
yw # copy word
yy # copy current line
y$ # copy from current character to the end of line
yG # copy from current line to end of file

dd, dw, dG, d$
x, cap x # delete char after cursor, delete char before cursor

p # paste after cursor
cap p # paste before cursor
```

```shell
# UNDO & REDO
u # undo
Ctrl u # redo
```

