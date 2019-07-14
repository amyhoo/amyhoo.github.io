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

# openssl
```sh
# generate private key ,actually the .pem file include private and public
openssl genrsa -out rsa.pem 1024
# check the information of rsa.pem
openssl rsa -text -in rsa.pem
# output the public key
openssl rsa -in rsa.pem -pubout -out rsa.pub
# export the private key
openssl pkey -in rsa.pem -out rsa.key
openssl -in rsa.pem -out rsa.key
```

# variables
```sh 
# assign a variable indirect refer it 's text name 
function assign(){
 var_name=$1
 var_value=$2
 if [[ -z "$var_value" ]]
 then
    read -p "please input $var_name: " $var_name
 fi
 echo "${!var_name}"
}
```

# set maximum process pool for a bunch of processes
```sh
function checkAndWait(){
	num_process=$1
	prcesses=( `echo $@ | cut -d" " -f2-`)
	while(( ${#processes[*]} >= $num_process ))
	do 
		wait ${processes[0]}
		prcesses=( `echo ${processes[@]} | cut -d" " -f2-`)
	done
	echo ${process[@]}
}
```