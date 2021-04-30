### Makefile简要教程

makefile: 工程管理器，用于管理复杂的project，有利于梳理多个文件之间的关系
		它会自动判别修改过的文件，自动编译修改过的文件即可
例如：
	main.c 依赖与 main.o tool1.o tool2.c
	tool1.o 依赖于 tool1.c 
	tool2.o 依赖于 tool2.c
main.c内容如下:

```cpp
#include<stdio.h>
#include"tool1.h"
#include"tool2.h"
int main()
{
	mytool1();
	mytool2();

	return 0;
}
```

tool1.h（tool2.h类似）内容如下：

```cpp
#ifndef TOOL1_H__
#define TOOL1_H__

void mytool1();

#endif
```

tool1.c(tool2.c类似)内容如下:

```cpp
#include<stdio.h>
#include "tool1.h"
void mytool1()
{
        printf("tool1 print\n\n");
}
```

第一个版本的Makefile:

```
mytool:main.o tool1.o tool2.o
        gcc main.o tool1.o tool2.o -o mytool
main.o:main.c
        gcc main.c -c -Wall -g -o main.o
tool1.o:tool1.c
        gcc tool1.c -c -Wall -g -o tool1.o
tool2.o:tool2.c
        gcc tool2.c -c -Wall -g -o tool2.o

clean:
        rm *.o mytool -rf
```

语法格式为:
target:依赖的文件
Tab键 执行的操作

第二个版本的改进:

```
OBJS=main.o tool1.o tool2.o
CC=gcc
CFLAGS+=-c -Wall -g

mytool:$(OBJS)
        gcc $(OBJS) -o mytool
main.o:main.c
        $(CC) main.c $(CFLAGS) -o main.o
tool1.o:tool1.c
        $(CC) tool1.c $(CFLAGS) -o tool1.o
tool2.o:tool2.c
        $(CC) tool2.c $(CFLAGS) -o tool2.o

clean:
        $(RM) *.o mytool -rf
```

我们可以引入变量OBJS ,变量值用$(变量)表示，可以简化内容

第三个版本的改进:

```
OBJS=main.o tool1.o tool2.o
CC=gcc
CFLAGS+=-c -Wall -g

mytool:$(OBJS)
        gcc $^ -o $@
main.o:main.c
        $(CC) $^ $(CFLAGS) -o $@
tool1.o:tool1.c
        $(CC) $^ $(CFLAGS) -o $@
tool2.o:tool2.c
        $(CC) $^ $(CFLAGS) -o $@

clean:
        $(RM) *.o mytool -rf
```

$^指的是执行上述所依赖的文件
$@指的是生成前面的目标文件target

第四个版本改进：

```
OBJS=main.o tool1.o tool2.o
CC=gcc
CFLAGS+=-c -Wall -g

%.o:%.c
        $(CC) $^ $(CFLAGS) -o $@

mytool:$(OBJS)
        gcc $^ -o $@

clean:
        $(RM) *.o mytool -rf
```

写成函数格式 %是通配符。。。