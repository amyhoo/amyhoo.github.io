---
categories: language
tags: [python, devOps]    
---
# message
>## print chromatic message to screen with different level alert labeled by keywords 
>## use logging function to print msg, because we can easily control complicated message,such as we check the signal what level msg should be output  

```sh
f_msg(){
	# red : fatal ,error; yellow : warning; green: success; blue: checking;
	level=$1
	# what function about the script block
	type=$2
	# the subject 
	title=$3
	# the action of the subject
	action=$4
	
	case $level in
	 error)
	 	echo -e "\033[31m $type $title $action \033[0m";;
	 success)
	 	echo -e "\033[32m $type $title $action \033[0m";;
	 warning)
	 	echo -e "\033[33m $type $title $action \033[0m";;
	 checking)
	 	echo -e "033[34m $type $title $action \033[0m";;
	 *) ;;
	esac	
	}	
	
```
# use comment, empty line to make content readily
>## use different pattern of comment to different part of shell script

# use function for duplicated usage 
>## as all languages ,we use function to make program more neat
>## besides, use function during the complicated process,make the more important main progress stand out 	
 
# record important step of process
>## for a procession , you should output message to record the critical step and rollback.



 

 
