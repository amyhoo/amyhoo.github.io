---
categories: os
tags: [linux]   
---

# function
```sh
#use return ,only for int 
function func1(){
	local retcode=0	
	local _tables=() # local array 
	return $retcode	
}
#show 0
echo $retcode

#echo
function func2(){
	local retcode=0	
	echo "retcode is $retcode "	
}
#show retcode is 0
result=`func2`
echo $result

#save return array in input param
function func3(){
	local _retVar=(1,2,3)
	local retcode=0
	eval "$1='$returnVar'"
	return $retcode
}
#receive array in input param
function fun4(){
	declare -a data_list=("${!1}") 
}
```

# loop
```sh
#files in directory
for file_path in $1/*.*
do
done

#read line in file

for line in `cat filename`
do 
	echo ${line}
done

while read -r line
do
	echo $line
done < filename

#read element in array
for data in "${data_list[@]}"
do
	echo $data
done
```
# filter ,column
```sh
#awk 
var=`echo $line|awk -F[,] '{print $1","$2}'`
data_list=(`printf '%s\n' "${datas_list[@]}"|awk '{print $1}'`)
#cut
var=`echo $line|cut -d: -f2`
#filter line
grep "format" filename
echo ${data_list[@]} | grep "format" 
```

# database
```sh
sql="select * from table1"
data_list=(`db2 -x $sql`)
```

# str format
```sh
#output the array with delimiter
dataStr=`printf ",'%s'" "${data_list[@]}"`
#compare with reg
$datastr=~[0-9]* 
#sub string
str='1.2.3'
${str#*.} #2.3 remove the first . and left
${str##*.} #3 remove the last . and left
${str%.*} #1.2 remove the last . and right
${str%%.*} #1 remove the first . and right 
```

# params
```sh 
#-t param1 -s param2 -d param3 k
while getopts ":t:s:d:k" opt
do
    case $opt in
        t)
        target=$OPTARG
        ;;
        s)
        source=$OPTARG
        ;;
        d)
        dest=$OPTARG
        ;;
        k)
        ;;
        ?)
        echo "error"
        exit 1;;
    esac
done
shift $(($OPTIND-1))
```