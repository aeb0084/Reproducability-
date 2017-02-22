# Reproducability-Stephen's Guest Lecture

###Anatomy of a script
- Recommended #! /usr/bin/env sh as the commadn line   
  - It works everywhere   
- Module block  
- Variable block  
- Commands   

###Environmental Variables 
- Used by more than one application 
  - $HOME, $PATH, $SHELL
###User Defined Variable 
- Defined by you 
  - can be anything; try not to use the environmental variables  
  - should be indicitive of what it stores; no special characters (underscrores work best)

###Setting Variables 
- can do it directly 
  - example: wd=$(HOME)/analysis_directory
- Setting them dynamically 
  - capture the output of the shell command 
  - files=(`ls $(input_dir) |grep sh$` )
    - looks for any file ending in sh

###Script to fix wrong file endings from .sh to .pl Example
```ruby
#find the files in the working directory: lets say theyre in input

#! /usr/bin/env sh

#########
#Module Block 
  module load something (none for this script)
############
#Variable Block 
  input_dir=input
  output_dir=output
## input / output files arrays
  files =(‘ls ${ input_dir } | grep sh$ ‘)
#takes the endings of sh and changes them to pl
  out_files =(‘echo ${ files [@]} | sed s/sh/pl/g ‘)
## parameter expansion 
## parameter / patten / string
  input_with_path =( "${ files [@]/#/ ${ input_dir }/}" ) 
  output_with_path =( "${ out_files [@]/#/ ${ out_dir }/}" )
########################
#Commands
## make the output dir
# -p tells it to create a directory even if it already exists, but not overwrite the previous one
  mkdir -p ${ out_dir }
## for loop
## use length to iterate in order to index input output arrays
  for ((i=0; i<${# input_with_path [@]}; i++)); do
  echo ${i}
  echo cp ${ input_with_path [${i}]} ${ output_with_path [${i}]}
done
# #####################
#Output from sed and parameter stuff
files =(‘ls ${ input_dir } | grep sh$ ‘)
awesome_script1.sh
awesome_script2.sh
awesome_script3.sh

out_files =(‘echo ${ files [@]} | sed s/sh/pl/g ‘)
awesome_script1.pl
awesome_script2.pl
awesome_script3.pl

input_with_path =( "${ files [@]/#/ ${input_dir }/}" )
input/awesome_script1.sh
input/awesome_script2.sh
input/awesome_script3.sh

output_with_path =( "${ out_files [@]/#/ ${ out_dir }/}" )
output/awesome_script1.pl
output/awesome_script2.pl
output/awesome_script3.pl
######
#Understanding the loop 
for ((i=0; i<${# input_with_path [@]}; i++)); do
  ${i}
  cp ${ input_with_path [${i}]} ${ output_with_path [${i}]}
done
echo ${i}

```
###For our Exercise

- modules 
  - blastn
  
- Variables
  - None Necessary Really 
  - But say that: "No Variables Necessary"
- Comment out evverything other than the database making and the final code that runs 
- Add comments to everything to make it understandable in six months


















