# 反汇编


* [函数调用汇编分析[1]- 函数调用规范(1)](http://www.hisnote.com/2013/06/19/%E5%87%BD%E6%95%B0%E8%B0%83%E7%94%A8%E6%B1%87%E7%BC%96%E5%88%86%E6%9E%90%E3%80%902%E3%80%91-%E5%87%BD%E6%95%B0%E8%B0%83%E7%94%A8%E8%A7%84%E8%8C%831/2/)
* [函数调用汇编分析[3]-实例分析1(值传递)](http://www.hisnote.com/2013/07/25/%E5%87%BD%E6%95%B0%E8%B0%83%E7%94%A8%E6%B1%87%E7%BC%96%E5%88%86%E6%9E%90%E3%80%903%E3%80%91-%E5%AE%9E%E4%BE%8B%E5%88%86%E6%9E%901%E5%80%BC%E4%BC%A0%E9%80%92/)

### 一.	每次进入main函数时均需执行以下指令：(用于建立新的函数的栈帧结构)
>函数B中的`ebp`用于存放上一层函数A的栈帧的基指 (上一层函数A的栈帧的栈顶地址值)，当由函数B进入到下一层函数C后，需将函数B的`ebp`压入函数B的栈帧顶部，并作为函数B的栈帧的栈顶(此时函数B的栈帧结束)，同时需将上一层函数B的栈帧的基指(上一层函数B的栈帧的栈顶地址值)`esp`赋值给`ebp`作为函数c的`ebp`。


| 汇 编 指 令 | 指令说明 |
|--------|--------|
|  push ebp    |  将上一函数A的栈帧(SF Stack Frame)的基指(栈顶地址值)ebp压入上一函数A的栈帧的顶部（作为上一函数A的栈帧的栈顶）      |
|  mov        ebp,esp      |   将上一函数A的栈帧的栈顶地址值（基址）esp赋值给ebp作为main函数的ebp     |
|  ebp      |    将上一函数A的栈帧(SF Stack Frame)的基指(栈顶地址值)ebp压入上一函数A的栈帧的顶部（作为上一函数A的栈帧的栈顶）    |

```C
#include<stdio.h>
int Add(int x, int y)
{
	int result;
	result=x+y;
    return result;
}
int main()
{
    int a=1,b=2,s;
    s=Add(a,b);
    printf("s=%d\n",a+b);//可以step into看一下printf函数的具体执行过程
    return 0;
}
```

