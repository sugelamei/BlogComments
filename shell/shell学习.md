# shell命令的使用 #
----------
## 一. 脚本样式 ##
脚本以#!/bin/bash 开头（指定解析器）。


          #/bin/bash
    
       echo  "hello word" 

----------


## 二.脚本的执行方式 ##

       sh hello.sh
      
      bash hello.sh
 
     ./hello.sh  (必须具有可执行权限)



**注意：sh 和bash执行方式，本质上是bash解析器帮你执行，因此不需要执行权限，./hello.sh执行方式，本质是脚本自己执行，所以需要执行权限**

----------

##  三.多命令处理  ##

    #!/bin/bash
	cd /home/file
	touch wxc.txt
	echo  " i love you ">>wxc.txt
 

----------

## 四.shell中的变量 ##

#### 1. 常用系统变量  ####

 		$HOME    
		$PWD
		$SHELL
		$USER
####  2. 自定义变量 ####
 
-  定义变量 ：变量=值（等号2边不能有空格）
- 撤销变量 unset 变量
- 声明一个静态变量：readonly 变量，注意：不能unset

#### 3.   变量定义的规则 ####
       
- 变量名字可以由字母、数字和下划线组成，但是不能以数字开头，环境变量名建议为大写。
- 等号2边不能有空格。
- 在bash中，变量默认类型都是字符串类型，不能直接进行数值运行。
- 变量的值如果有空格，需要使用双引号或者单引号括起来。
- 可以把变量提升为全局环境变量，可供其他shell 使用     export  环境变量

####   4.特殊变量  ####

- $n   :n为数字，$0代表改脚本名称，$1-$9代表第一到第九个参数，十以上的参数需要用大括号包含，如${10}

- $#:获取所有输入参数个数，常用于循环

- $*:这个变量代表命令行中所有的参数，它把所有的参数看做一个整体

- $@:这个变量代表命令行中所有的参数，它把每个参数区别对待

- $?:最后一次执行命令的返回状态，如果这个变量的值为0，证明上一个命令正确执行，如果这个变量的值为非0，则证明上一个命令执行不正确。

##  五.运算符  ##

- “$((运算式))”或"[运算式]"
- expr +，-，\*,/,%   加，减，乘，除，取余（注意：expr需要有括号）


## 六.条件判断  ##
> 基本语法

        [condition] )(注意condition前后要有空格)

> 常用判断条件
     
      
- 两个整数间的比较      = 字符比较


>       -lt  小于（less than）
>       -le 小于等于 （less  equal）
>       -eq 等于 （equal）
>       -gt 大于（greater than）
>       -ge 大于等于 （greater equal）
>       -ne  不等于 （Not equal）


- 按照文件权限进行判断

>         -r 读（read） 
>         -w 写 （write）
>         -x 执行（execute）

- 按照文件类型进行判断

>        -f 文件存在并且是一个常规的文件
>       -e文件存在（existence）
>       -d 文件存在并是一个目录（directory）


- 多条件判断

>     && ：表示前一条命令执行成功时，才执行后一条命令
>     ||：表示上一条命令执行失败后，才执行下一条命令
   



## 七.流程控制 ##

#### 1.if判断 ####
      
       基本语法
  
     if [ 条件判断式 ]  ；then
        
         程序

     fi

      或者



  
	if [ 条件判断式 ]

    		then

		程序

	fi



> 注意事项：

       [ 条件判断式 ]中括号和条件判断表达式之间必须有空格

       if 后要有空格


      		 #!/bin/bash
   
  			 if [ $1 -eq 1 ]

  			 then  
  			  echo   "one"

  			elif [ $1 -eq 2]

  			then  
			   echo  "two"
 			 fi

####  2.case 语句 ####

> 基本语法

          case $变量名  in 
        
         “值1”）
 	
		如果变量的值等于值1，则执行程序1
		;;

 	     “值2”）
 	
		如果变量的值等于值2，则执行程序2
		;;
        
           *)
           
  		如果变量的值都不是以上值，则执行此程序
 
           ;;
		esac

> 注意事项：
      	case行尾必须为单词 “in”  ，每一个模式匹配必须以右括号“)”结束
		双分号“;;”表示命令序号结束，相当于java中的break
  		最后的“*)”表示默认模式，相当于java中的default
       
		 !#/bin/bash
		  
		case   $1 in
		   		 
		1)
		  echo "man"
		;;
			2)  
		echo  "women"
		  ;;
		 *)
		 echo   "renyao"
			;;
		 esac
    
     
#### 3.for循环 ####

> 基本语法
           
  		
		    for（（初始值;循环控制条件;变量变化））
    			
    			do
    						
    				程序
    			
    			done



		        #!/bin/bash
			
				
		   	 s=0
				
			for((i=0;i<100;i++))
			
				do
					s=$[$S+$i]	
			
		   done


			echo $s

----------
    
		for  变量 in  值1 值2  值3...
 			
			do
				程序
				
			done

            
           #!/bin/bash
			
			for i in $*
			
			do
				echo $i

			done 

			for j in $@
			
			do
				echo $j

			done 


> 注意事项：“$*”  表示一个整体
                     ”$@“ 表示单个

  #### 4.while 循环 ####

> 基本语法
       
			  while[条件判断式]
			
			   do
			  		程序
				done

----------

				#!/bin/bash
				   s=0
				   i=0
				   while[ $i -le 100 ]
				
				do 
				          s=$[$i + $s]
				 	    i=$[$i + 1]
				done

----------


## 	七.read  读取控制台参输入  ##

> 基本语法

		
		      read (选项)(参数)
		       
		    选项：
		 
				-p：指定读取值时的提示符
		  		-t：指定读取值时的等待的时间（秒）
		
		   参数：指定读取值的变量名

		    #/bin/bash
			read -t  7  -p  "Enter   you name"  NAME
		   echo   $NAME



## 八.函数 ##

#### 系统函数 ####



> 		basename [string/pathname][suffix]

	   	功能描述：basename 命令会删除掉所有的前缀包括最后一个('/')字符，然后将字符串显示出来
		选项：suffix为前缀，如果suffix被指定了，basename会将string或者pathname中的suffix去掉。





>         dirname    文件的绝对路径
			
		功能描述 ：从给定包含绝对路径的文件名中去除文件名（非目录的部分），返回剩余的部分（目录的部分）

         
####  自定义函数 ####
   
      
> 基本语法



			   [function] funname[()]
			{
			
			Action；
			
			[return int;]
			
			}
			
			funname

> 经验技巧 ：
			

			必须在调用函数之前先声明函数，shell脚本是逐行执行的，不会像其他语言一样先编译。
 			函数的返回值，只能通过$?系统变量获得，可以显示加：return 返回，如果不加，将以最会一条命令的运行结果作为返回值，return 后跟数值n（0-255）

			
			#!/bin/bash
 			
			function  sum()
			{
				s=0;
				s=$[$1 + $2]
				echo $s
			}


			read -p  "input   P1： " P1
			read -p  "input   P2： " P2

			sum $P1 $P2




## 八.Shell 工具（重点） ##

####      cut ####

>         cut的工作就是“剪“，具体来说留是在文件中负责剪切数据用的。cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段输出。

> 基本用法

		cut  [选项参数] filename

		说明：默认分隔符是制表符
    		
		-f：列号，提取第几列
  		-d:分隔符，按照指定的分隔符分割列

 
     cut cut.txt|grep guan| cut -d " " -f 1

 
#### sed ####

> sed是一个流编辑器，它是一次处理一行内容。处理时，把当前处理的行储存在临时缓冲区中，称为“模式空间”，接着用sed 命令处理缓冲区的内容，处理完后，把缓冲区的内容打印出来，接着处理下一行，直到文件末尾。文件内容并没有改变，除非你使用重定向储存输出。


> 基本语法

  sed[选项参数]  ‘command’    filename

   选项参数：
      		-e： 直接在指令列模式上进行sed的动作编辑

  命令功能描述：
				
			a:新增，a的后面可以接字符串，在下一行出现
			d：删除
			s;查找并替换


				sed “2a mei nv” sed.txt
				sed "/wo/d" sed.txt
                        sed "s/wo/ni/g"sed.txt

                         注意:g 表示global ，全部替换


#### awk ####

> 一个强大的文本分析工具，把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行分析处理。

> 基本用法

    awk[选项参数] ‘patternl{action1} patternl{action2}...' filename
      
		   pattern:表示AWK在数据中查找的内容，就是匹配模式
		  action：在找到匹配内容时所执行的一系列命令。

选项参数：
             
           -F :指定输入文件拆分隔符
		-v:赋值一个用户定义变量


 注意：只有pattern匹配才会执行action
          BEGIN在所有数据之前执行，END在所有数据执行之后执行
   

> awk的内置变量

              FILENAME：文件名
              NR：已读的记录数
              NF：浏览记录的域的个数（切割后，列的个数） 

#### sort ####

> 基本语法

             sort(选项)(参数)


           选项：
		-n：依照数值的大小排序
  		-r ：以相反的顺序来排序
 		-t：设置排序时所用的分隔字符
		-k：指定需要排序的列

   		参数：指定待排序的文件列表