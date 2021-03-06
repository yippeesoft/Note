#Lua Note
___

## 0.Ticks
1. do ... end 可以在控制台中插入临时变量
2. dofile 执行
3. loadfile 加载
4. `--[[  --]]`   -------------多行注释
5. `--`   						单行注释


##1. 类型
1. nil
2. boolean
3. number
4. string
5. table
6. function
7. userdata 
8. thread


note：

* `type（x）` 查看x的类型
* \#a a的大小
 
##2.表达式
1. 算术表达式

	1. \+  
	2. \-
	3. \*
	4. /
	5. %
	6. ^
	
2. 关系表达式
> <,  > ,>=,<=, == , ~=
3. 逻辑表达式
	* and
	* or
	* not
	
	and 和or 都是用“短路求职”，也就是说它们只会在需要的时候才会去计算和评估第二值。

	print(4 and 5)   --------------------"5"

	print(0 and 5)   --------------------"5"  0也是true

	print（nil and 4）------------------- nil

4. 字符串连接
	`..`
 	print("wer" .. "45")  -------------wer45
5. 优先级
	* ^,-(一元)
	* not, # ,
	* \*, /, %,
	* \+, -
	* <,>,<=,>=,~=,==
	* and
	* or
6. table构造
	<pre>
	a = {}
	a= {x = 10,y = 20}
	print(a.x)  -------------10
	print(a[x]) --------------nil
	</pre>

##3 语句
### 3.1
 	1. 局部变量 local  i=1
	2. 全局变量 i=1
### 3.2 结构
##### 3.2.1 if then else
	* if a < 0 then a = 0 end
	* if a < b then return a else return b end
	* if line > maxlines then
			showage()
			line = 0
	  end
	* if op == "+" then
		r = a + b
	  elseif op == "-" then
		r = a - b
	  elseif op == "*" then
		r = a * b
	  else
		error("")
	  end

#####3.2.2 while
	* local i = 1
	  while a[i] do
		print(a[i])
		i = i + 1
	  end
	* a = 10
	  while a >= 0 do
		print(a)
		a = a-1
	  end
##### 3.2.3 repeat
<pre>
	repeat
		line = io.read()
	until line ~=""
	print(line)
</pre>
##### 3.2.4 for
<pre>
	for i = 10, 1,-1 do print(i) end
	其中 -1 为步长
</pre>
### 4 break return

### 5 函数
* 冒号操作符： o.func(o,x)  <==>  o::func(x)
  冒号操作符使调用o.func时将o隐含地作为函数的第一个参数

#####5.1 多重返回值 multiple results
	* s,e = string.find("hello world, lua","lua")

<pre>
***********************************
function foo()
 return 2,4
end
x,y = foo();     -----> x = 2,y = 4
x,y = foo(),20   -----> y = 20
x,y,z = foo(),20 -----> z = nil
***********************************
</pre>

##### 5.2 变长参数 （...）
<b>
<pre>
function add(...)
	local s = 0
		for i,v in ipairs{...} do
			s = s + v
		end
    return s
end
print(add(4,4,10,25,12))   --> 54
</pre>
</b>

#####5.3 具名实参 named argus

 。。。。

###6 深入函数
* a = function(x) return 3*x end

#####6.1 闭合函数
#####6.2 非全局的函数 non-global function
#####6.3 尾调用

### 7协同程序 coroutine
	与线程的区别是 线程是并发的，协同程序只是同一时间单一执行的

#### 7.1 basic
#### 7.2 pipe  filter
#### 7.3 iterator
#### 7.4 non-preemptive


----
##8.<font color="#00ff00">TABLE</font>

1. <font color="#ff0000">创建table in c++</font>
<PRE>
> `void lua_createtable (lua_State *L, int narr, int nrec);`
<CODE>
Creates a new empty table and pushes it onto the stack. 
The new table has space pre-allocated for <b>narr</b> <font color="#0000ff">array elements</font> and <b>nrec</b> <font color="#0000ff">non-array elements. </font>
This pre-allocation is useful when you know exactly how many elements the table will have. 
Otherwise you can use the function <B><font color="#0000ff">lua_newtable</font></B>. 
</CODE>
</PRE>

2.lua 语言创建table
> 
<PRE>
t = {}    -- construct an empty table and assign it to variable "t"
print(t)
</PRE>

>  
>  2.1  Tables as arrays
<pre>
> t = { 1,1,2,3,5,8,13 }
> print( t[1] )
1
> print( t[0] )
nil
> print( t[4] )
3
</pre>

<font color="#ff00">equal to</font>
<pre>
> t = {}
> t[1]=1 t[2]=1 t[3]=2 t[4]=3 t[5]=5 t[6]=8 t[7]=13
</pre>
2.2 size of table
> 
 #t

2.3 遍历
> 
<pre>
> for i,v in ipairs(t) do print(i,v) end
	1       1
	2       1
	3       2
	4       3
	5       5
	6       8
	7       13
	8       21
</pre>
<font color="#ff00">equal to</font>
<pre>
> for i=1,# t do
	print(i,t[i])
	end
</pre>

2.4 Tables as dictionaries

<pre>
    > t = { apple="green", orange="orange", banana="yellow" }

<font color="#ff00">is the same as:</font>

    > t = { ["apple"]="green", ["orange"]="orange", ["banana"]="yellow" }

</pre>

2.5 Mixed table constructors

<pre>
1. > t = { 2,4,6, language="Lua", version="5.1" }

<font color="#0000ff">
Here we have an array of numbers followed by some dictionary values.
We can use our Lua table library functions to output the contents of the table.
</font>
2. > for k,v in pairs(t) do print(k,v) end
    1       2
    version 5.1
    3       6
    language        Lua
    2       4
    > for i,v in ipairs(t) do print(i,v) end
    1       2
    2       4
    3       6
</pre>


2.6 demo
<pre>
> tablekey = {1,2,3}                     -- create a table with a variable referencing it
> a = { [tablekey]="yadda" }             -- construct a table using the table as a key
> for k,v in pairs(a) do print(k,v) end  -- display the table elements
table: 0035F2F0 yadda
> = a[tablekey]                          -- retrieve a value from the table
yadda
> print(tablekey)              -- the table value is the same as the key above
table: 0035F2F0
</pre>




3.FAQs

1.  how to nest tables 
<pre>
<font color="#777777">
I want to create a table like

myTable = {
    [0] = { ["a"] = 4, ["b"] = 2 },
    [1] = { ["a"] = 13, ["b"] = 37 }
}
using the C API?

My current approach is

lua_createtable(L, 0, 2);
int c = lua_gettop(L);
lua_pushstring(L, "a");
lua_pushnumber(L, 4);
lua_settable(L, c);
lua_pushstring(L, "b");
lua_pushnumber(L, 2);
lua_settable(L, c);

to create the inner tables in a loop. Before, this loop, I use

lua_createtable(L, 2, 0);
int outertable = lua_gettop(L);

to create the outer table for 2 numeric slots.

But how can I save the inner tables to the outer table?
</font>
<font color="#ff0000">Answers</font>
</pre>
<pre><code>
#include < stdio.h >
#include "lua.h"
#include "lauxlib.h"
#include "lualib.h"

int main()
{
    int res;
    lua_State *L = lua_open();
    luaL_openlibs(L);

    lua_newtable(L); /* bottom table */

    lua_newtable(L); /* upper table */

    lua_pushinteger(L, 4);
    lua_setfield(L, -2, "four"); /* T[four] = 4 */
    lua_setfield(L, -2, "T");  /* name upper table field T of bottom table */
    lua_setglobal(L, "t"); /* set bottom table as global variable t */

    res = luaL_dostring(L, "print(t.T.four == 4)");
    if(res)
    {
        printf("Error: %s\n", lua_tostring(L, -1));
    }

    return 0;
}
</code>
</pre>

The program will simply print true.

If you need numeric indices, then you continue using <font color="#ff0000">lua_settable</font>:
<pre><code>
#include <stdio.h>
#include "lua.h"
#include "lauxlib.h"
#include "lualib.h"

int main()
{
    int res;
    lua_State *L = lua_open();
    luaL_openlibs(L);

    lua_newtable(L); /* bottom table */

    lua_newtable(L); /* upper table */

    lua_pushinteger(L, 0);
    lua_pushinteger(L, 4);
    lua_settable(L, -3);  /* uppertable[0] = 4; pops 0 and 4 */
    lua_pushinteger(L, 0);
    lua_insert(L, -2); /* swap uppertable and 0 */
    lua_settable(L, -3); /* bottomtable[0] = uppertable */
    lua_setglobal(L, "t"); /* set bottom table as global variable t */

    res = luaL_dostring(L, "print(t[0][0] == 4)");
    if(res)
    {
        printf("Error: %s\n", lua_tostring(L, -1));
    }

    return 0;
}

</code>
</pre>


2. another

> 	table, 作为Lua中的重要类型, 为数据管理提供了许多便利. 我们可以用C++, 在Lua上下文(Lua_State)中注册table, 以便lua程序可以方便的和C++进行交互.

先来看一段C++代码:
<pre>
<code>
`lua_State* pLuaState = luaL_newstate();
luaL_openlibs(pLuaState); 
lua_createtable(pLuaState, 0, 1);
lua_pushcclosure(pLuaState, CallBack, 0);
lua_setfield(pLuaState, -2, "Add");
lua_setfield(pLuaState, LUA_GLOBALSINDEX, "Math");`
</code>
<pre>

> 
这里, 我创建了一个Lua table(lua_createtable), 并将C++函数CallBack以"Add"为键值,
注册到新的table中, 然后将table作为全局变量Math注册到当前的上下文中.这样, 我在lua代码中就可以这样写:
`print(Math.Add(1100,10))`
这条语句, 通过执行Math表中的Add, 从而调用到C++中的CallBack函数.
当我们不再需要这个table的时候, 我们使用以下的语句, 将table的引用减少.

> 
`lua_pushnil(pLuaState);`
`lua_setfield(pLuaState, LUA_GLOBALSINDEX, "Math");`

这两条语句相当于lua中的 Math = nil, 这样, GC就可以回收table和function的资源了.

下面附上完整的C++代码:
<pre>
#include < lua.hpp >
 
#pragma comment(lib, "lua51.lib")
 
int CallBack(lua_State* pLuaState)
{
    int a = luaL_checkint(pLuaState, 1);
    int b = luaL_checkint(pLuaState, 2);
 
    lua_pushnumber(pLuaState, a + b);
 
    return 1;
}
 
int _tmain(int argc, _TCHAR* argv[])
{
    lua_State* pLuaState = luaL_newstate();
    luaL_openlibs(pLuaState);
 
    lua_createtable(pLuaState, 0, 1);
    lua_pushcclosure(pLuaState, CallBack, 0);
    lua_setfield(pLuaState, -2, "Add");
    lua_setfield(pLuaState, LUA_GLOBALSINDEX, "Math");
 
    if (luaL_loadfile(pLuaState, "test.lua") ||
        lua_pcall(pLuaState, 0, 0, 0))
    {
        printf("%s\n", lua_tostring(pLuaState, -1));
        lua_pop(pLuaState, 1);
        lua_close(pLuaState);
        return 0;
    }
 
    lua_pushnil(pLuaState);
    lua_setfield(pLuaState, LUA_GLOBALSINDEX, "Math");
 
    if (luaL_dostring(pLuaState, "print(Math.Add(100, 10))"))
    {
        printf("%s\n", lua_tostring(pLuaState, -1));
        lua_pop(pLuaState, 1);
        lua_close(pLuaState);       // 这里加断点调试, 查看控制台输出结果
        return 0;
    }
 
    lua_close(pLuaState);
    return 0;
}
</pre>
























