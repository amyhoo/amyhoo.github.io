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

# the variables
## shell variable have different levels
### 1. system variables : 
	defined in system profile or your profile, which would load into your environment variables in each shell.
	
### 2. environment variables: 
	all local shell scripts would share the variables, which can be easily polluted and also generate much complex, because your script refer something generate by other any scripts. you almost have no control on this.
	the format would be capital words joined by "_" :CAPITAL_CAPITAL 

	but sometimes we also define constant use this format ,in order to distinguish  we can and prefix "_" as constant: _CAPITAL_CAPITAL
### 3.global variables:
	default variables defined in your script, 
	I suggest your can distinguish this kind variable by define with different format,such as Capital first words and joined by "_": Capital_Capital
	
### 4.local variables:
	defined with prefex local, this kind variable can differentiate itself by using typical define format
	lower case words and joined with "_" (even you put put prefix with "_" ): _word_word, word_word
	
## using environment variables
```
I suggest environment variables shouldn't be intermediate data storage between two scripts. I once encounter this problem, so much scripts use environments, which is not defined by your script. as the scripts become more and more, it become very complicated to maintain.

the variable using principle: the variable should define in the range according its meaning.

so on, if there is common constant variable which would be used by most scripts, you can define them as environment variables

but if some variables which just used transfer information between two function ,or pipeline, it is not a good decision to export them, you use the variable by its own range of meaning
```

## global variables
```
you can use global variables as data between two functions, as those variables are all kept by your script. you are aware about their usage.
sometimes you need some flexibility about your work flow, such as there are several stage s1 s2 s3 s4 s5;  workflow1 is s1->s2->s5, workflow2 is s2->s4,and so on.  there are too many combination about steps. you can use global variable as a control of your work flow instead write all the possible workflow .

those kindly like using environment variables to conduct information among cooperated modules,but environment variable is bad solution to do this because it is hard to maintain.

those intermediate variable serve as premise for each step, if the premise are fulfilled , you don't care how the premise is achieved,so each step is somewhat independent without apparent call with other steps.you can control each steps separately, make sure the variables you generated from the former step can offer the premise for the next step, which can make the process flow. those steps rely on data relation not direct call
```

## local variables
```
I think to make shell script more modularization is write function would rely on the parameters.
in this way, you can decouple your code and re-assemble it as what your want.just copy the function to anywhere would work.no need rely on global variables and environment variables.
```
 

 
