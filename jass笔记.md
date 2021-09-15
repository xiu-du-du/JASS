# jass

#### 函数表达式

````jass
    function 函数名 takes 参数1，参数2...(nothing) returns 返回值(nothing)
        // init_body
        call BJDebugMsg("hello YDWE")
        call BJDebugMsg("hello world")
    endfunction
````

#### T转J

````jass
//定义动作函数
function fun1 takes nothing returns nothing
	if (GetTriggerPlayer()==Player(0)) then //条件
		//发送文本信息“hello world”
		call DisplayTextToPlayer(Player(0),0,0,"hello world") 
	endif
endfunction

//事件
function InitTrig_______u takes nothing returns nothing
	local trigger a = CreateTrigger()  //通过CreateTrigger() 创建一个局部触发a
	call TriggerRegisterPlayerChatEvent( a,Player(0),"1",true) //注册聊天事件
	call TriggerAddAction(a,function fun1) //把动作函数添加进a触发
	set a=null //排泄：设置a=空，优化清空内存。
endfunction
````



#### 变量和数据类型

##### 基础数据类型

````
integer-整数型

real-实数型，例如：0.1 ， 0.111

 boolean-布尔型

string-字符串

handle-数据指针型，用来指向内存中的一个数据地址。

code-函数指针型，用于指向内存中的函数地址
````

##### 其他类型

````
unit（单位）
group(单位组) 
item(物品) 
location(点) 
等等......
这些数据类型的定义，使用同以上几种是一样的。
````



##### 全局变量声明

````jass
globals
	string str="全局变量名"
	integer int=10
endglobals
````

##### 局部变量声明

````jass
local string str1="局部变量"
local integer int1=10
````

##### 区别

> 全局变量任何地方都可以调用，局部变量只能在当前作用域使用。

> 全局变量容易冲突，局部变量不会。

> 局部变量容易排泄，全局变量可能会引起报错。

##### 用途

> 如果在很多个函数内都需要调用，就使用全局变量。如果在多人模式下，一般使用局部变量，这样不容易产生冲突，易于排泄。

#### jass类型

> 打开文件：YDWE或WE编辑器目录\jass\system\ht\common.j

#### jass 命名规则

1. 必须是字母开头 
2. 可以有 a-z 或 A-Z
3. 可以有 0-9
4. 可以有 下划线

#### loop循环语句

````jass
function test takes nothing returns nothing
    local integer i=0 //设置一个整数变量
    loop              //开始循环
        exitwhen i>10  //i>10就结束
        call DisplayTextToPlayer(Player(0),0,0,I2S(i)) 
        set i=i+1		//每次循环i都加1
    endloop				
endfunction

function InitTrig_______u takes nothing returns nothing
	local trigger a = CreateTrigger()  //通过CreateTrigger() 创建一个局部触发a
	call TriggerRegisterPlayerChatEvent( a,Player(0),"1",true) //注册聊天事件
	call TriggerAddAction(a,function test) //把动作函数添加进a触发
	set a=null //排泄：设置a=空，优化清空内存。
endfunction
````

##### 慎用：全局变量被两个函数同时循环的时候，会产生冲突！

#### if语句

| ==          |
| ----------- |
| !=          |
| >=          |
| <=          |
| <           |
| >           |
| x>y and x<i |
| x>y or x<i  |
| x>y not x<i |

##### if表达式

````jass
function test takes nothing returns nothing
    local integer i=GetRandomInt(1,101) //创建一个随机数
    call BJDebugMsg(I2S(i))  //查看随机数
    if i>=10 and i<=30 then  //设置当 i大于10 并且 i小于30 的条件
        call BJDebugMsg("a") //执行动作 输出聊天信息“a”
    elseif 34<i and i<50 then //设置当 i大于34 并且 i小于50 的条件
        call BJDebugMsg("b")  //执行动作 输出聊天信息“b”
    else					  //如果不满足上面两种条件
        call BJDebugMsg("c")  //执行动作 输出聊天信息“c”
    endif
endfunction
````

