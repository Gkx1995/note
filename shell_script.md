```shell
# sha-bang
#!/bin/bash
#!/bin/zsh
# print all things when running
!x

# quoting variables in bash script
# spacing around the square brackets is very IMPORTANT!
color = $1
then 
	echo "empty color variable!"
if [ "$color" = "blue" ]
then
	echo "it is blue"
elif [ "$color" = "red" ]
then 
	echo "it is red"
else
	echo "do not know color"
fi
```

```zsh
-n "$val" #true if string not empty
-eq, -ne, -gt, -lt, -ge, -le
-d # true if "file" is a directory
-f # true if "file" is a regular file
-r # existing and readable
-w # existing and writable
-x # existing and executable
```

```zsh
# while loop
echo "Enter a five-digit ZIP code"
read ZIP

# -v return true if pattern not found,
# > /dev/null 2>&1, do not display output
while echo $ZIP | egrep -v "^[0-9]{5}$" > /dev/null 2>&1
do
	echo "you must enter a valid ZIP code"
	echo "Enter a five-digit ZIP code"
	read ZIP
done

echo "Thank you!"

# for loop
for var in a b c d
do
	echo "$var"
done

# case statement
color = "red"
case $color in
red)
	echo "red";;
blue)
	echo "blue";;
white|yellow)
	echo "while or yellow";;
esac
```

