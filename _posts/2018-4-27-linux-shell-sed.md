---
categories: os
tags: [linux]  
---
# sed command pattern
sed is good line operation
## sed "[-reinf] [acidps]"
# sed action [acids prw]
```sh
#delete
cat data.txt | sed '1,5d'
echo data.txt | sed '1,$d'
#insert
cat data.txt | sed '2a hello\min'
# replace line
cat data.txt | sed '2c hello min'
# replace content with new
cat data.txt | sed 's/old/new/g'
cat data.txt | sed 's/[ /t]*//g' #clear all space or tab
cat data.txt | sed 's/^[ /t]*|[ /t]*$' #clear the first and last space or tab
# only show match
cat data.txt | sed '^#'
```

# sed params [reinf]
```sh
# directly edit file
sed -i '2d' data.txt
# only show the edited line on screen
sed -n '2d' data.txt
# multi line
sed -e '2d' -e '3a hello' data.txt
```