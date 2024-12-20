# DAY1-变量

## 1.变量

**C语言的数据类型关键字**

| 最初 K&R 给出的关键字 | C90标准添加的关键字 | C99标准添加的关键字 |
| --------------------- | ------------------- | ------------------- |
| int                   | signed              | _Bool （布尔型）    |
| short                 | void                | _Complex（复数）    |
| long                  |                     | _Imaginary(虚数)    |
| unsigned              |                     |                     |
| char                  |                     |                     |
| float                 |                     |                     |
| double                |                     |                     |

> **声明**（declaration）：在使用变量（variable）之前，必须对其进行声明（为编译器所作的描述）。
>
> 声明的方式为：数据类型 + 变量名 命名规则：可以用小写字母，大写字母，数字和下划线（_）来命名。**名称的第一个字符必须是字符或下划线，不能是数字**，变量通过赋值获得值

## 2.数据类型

关键字创建的类型，按计算机的存储方式可分为两大基本类型：**整数类型** 和 **浮点数类型**

#### 位，字节和字

> **位，字节和字**
>
> **位（bit）：**最小的存储单元，也称比特位。可以存储 0 或 1（或者说，位用于存储“开”或“关”）
>
> **字节（byte）：**1 byte = 8 bit 既然 1 位可以表示 0 或 1，那么 1 字节就有 256 （2^8）种 0/1 组合，通过二进制编码（仅用 0/1 便表示数字），便可表示 0 ~ 255 的整数或一组字符。（*以后会详细讲解*）
>
> **字（word）：**是设计计算机时给定的自然存储单位。对于 8 位 的微型计算机（如：最初的苹果机），1 字长 只有 8 位，从那以后，个人计算机的字长增至 16 位，32位，直至目前的 64位。计算机字长越大，其数据转移越快，允许访问的内存越多。

#### 整数与浮点数

浮点数的科学计数法表示：3.16E+007 表示 3.16 * 10^7(3.16乘以10的七次方)。007 表示 10^7；+ 表示 10 的指数 7 为正数。

其中，E 可以写成 e；表示正次数时，+ 号可以省略；007也可以省略为7。即：3.16e7。

#### 整数与浮点数的区别：

- 整数没有小数部分，浮点数有小数部分
- 浮点数可以表示的范围比整数大
- 对于一些算术运算（如，两个很大的数相减），浮点数损失的精度更多
- 因为在任何区间内都存在无穷多个实数，所以计算机的浮点数不能表示区间内的所有值。浮点数通常只是实际值的近似值。（例如，7.0 可能被存储为浮点值 6.99999）
- 过去，浮点数运算比整数运算慢。不过现在许多CPU都包含了浮点数处理器，缩小了速度上的差距

### 2.1整型

#### 有符号整数和无符号整数

> **有符号整数**如果为**零或正数**，那么最左边的位（符号位，只表示符号，不表示数值）为 **0** ；如果为**负数**，则符号位为 **1**。如：最大的 16 位整数（2个字节）的二进制表示形式是 01111111 11111111，对应的数值是 32767（即：2^15 - 1）
>
> **无符号整数** 不带符号位（最左边的位是数值的一部分）。因此，最大的 16 位整数的二进制表示形式是：11111111 11111111（即：2^16 - 1）
>
> 默认情况下，C语言中的整型变量都是有符号的，也就是说最左位保留符号位。若要告诉编译器变量没有符号位，需要把他声明成 unsigned 类型。

#### 整数的类型

> short int
>
> unsigned short int
>
> int
>
> unsigned int
>
> long int
>
> unsigned long int

```c
#include <stdio.h>
#include <math.h>
int main(){
    unsigned int result = pow(2,32)-1;//pow函数用于计算2的31次方
    printf("result = %u\n",result);
    return 0;
}
```

**注释**：申明无符号整型可以存储最大的32位整数

```c
#include <stdio.h>
int main(){
    int i;
    char a;
    float k = 3.14;
    i = 1;
    a = 'l';
    printf("int is %d bytes\n",sizeof(int));
    printf("short int is %d bytes\n",sizeof(short int));
    printf("long int is %d bytes\n",sizeof(long int));
    printf("char is %d bytes \n",sizeof(char));
    printf("float is %d bytes \n",sizeof(float));
    printf("double is %d bytes \n",sizeof(double));
    printf("i is %d bytes \n",sizeof(i));
    //sizeof(表达式)查询所占字节数
    // signed 带符号修饰int的可以signed int i = -1；unsigned为不带符号不可以进行左述定义
    return 0;
}
```

**C语言允许通过省略单词 int 来缩写整数类型的名称。**

例如：unsigned short int 可以缩写为 unsigned short ；而 long int 可以缩写为 long。

C程序员经常省略 int 。

**32位机器整数类型**

| 类型           | 最小值               | 最大值               |
| -------------- | -------------------- | -------------------- |
| short          | -32768( - 2^15 )     | 32767(2^15 -1 )      |
| unsigned short | 0                    | 65535 (2^16 - 1)     |
| int            | - 2147483648(- 2^31) | 2147483647(2^31 - 1) |
| unsigned int   | 0                    | 4294967295           |
| long           | - 2147483648         | 2147483647           |
| unsigned long  | 0                    | 4294967295           |

可以看出，32位机器上，int 与 long的大小是一样的，都是 4 个字节。

16位机器上，int 与 short 大小是一样的，都是 2 个字节。

64位机器上，与 32 位机器不同的是，long 是 8 个字节。

- **十进制**常量包含 0 ~ 9 的数字，但是不能以 0 开头

  15 255 32767

- **八进制**常量包含 0 ~ 7 的数字，必须要以 0 开头

  017 0377 077777

- **十六进制**常量包含 0 ~ 9 的数字 和 A ~ F 的字母，总是以 0x 开头

  0xf 0xff 0x7fff

```c
#include<stdio.h>

int main(void) {

	int x = 100;

	printf("decimal = %d	octonary = %o	hexadecimal = %x \n", x, x, x);
	printf("decimal = %d	octonary = %#o	hexadecimal = %#x \n", x, x, x);
	return 0;
}
```

输出：

```c
decimal = 100   octonary = 144  hexadecimal = 64
decimal = 100   octonary = 0144 hexadecimal = 0x64
```

16进制常量的字母可以大写也可以小写

### 2.2浮点型

C语言提供了三种浮点类型，对应着不同的浮点格式：

- `float`:单精度浮点数
- `double`：双精度浮点数
- `long double`：扩展精度浮点数

#### 浮点数常量

浮点常量可以有多种写法。例如，下面这些写法都表示数 57.0

57.0 57. 57.0e0 5.7e1 5.7e+1 .57e2 570.e-1

浮点常量必须包含**小数点或指数**

**默认情况下，浮点常量都以双精度的形式存储。**换句话说，当 C语言的编译器在程序中发现常量 57.0 时，它会安排数据以 double 类型变量的格式存储在内存中。

如果只需要单精度，可以在常量末尾加上 `F`或`f`（如 57.0F）；如果想以 long double 格式存储，在常量尾加上 `L`或 `l`(如 57.0L)

而且在写代码的过程中可以将0进行缩写，如 0.567 可以写为 .567

### 2.3字符型

```c
#include <stdio.h>
int main(){
    char a ='a';
    printf("%c %d",a,a);
    return 0;
}
//a 是97 A是65
```

根据ASCII码表，**C语言把字符当作小整数进行处理**。

所有字符都是以二进制形式进行编码的。

#### 有符号字符 和 无符号字符



**有符号字符**`signed char`：取值范围：-128 ~ 127

**无符号字符**`unsigned char`: 取值范围：0 ~ 255

可移植性技巧：不要假设 char 类型默认为 signed 或 unsigned 。如果有区别，用 signed char 和 unsigned char 代替 char 。

#### 算数类型

**整数类型** 和 **浮点类型** 统称为 **算数类型**。以下为 C89 中对算数类型的分类

- 整数类型
  - 字符类型（char）
  - 有符号整型（signed char, short int, int, long）
  - 无符号整型（unsigned char, unsigned short int, unsigned int, unsigned long int）
  - 枚举类型
- 浮点类型（float，double，long double）

```c
#define   _CRT_SECURE_NO_WARNINGS //不安全函数解决
#include <stdio.h>
int main(){
    char fish[6] = {'f','i','s','h','c','\0'};
    char ch1[] = "Stick to it will be something"; //vs无法打印,除非头文件追加第一行内容
    char name[6];
    name[0]= 'f';
    name[1]='i';
    name[2]='s';
    name[3]= 'h';
    name[4]='c';//5是从零开始计算即0-4
    name[5]='\0';//告诉编译器字符串终止
    printf("%s\n",name);
    printf("%s\n",fish);
    printf("%s\n",ch1);
    return 0;
}

```

#### 字符串定义的语法

```c
1.char name[num] = {'a','b','c','d','e'....,'\0'};
2.char name[num];
name[num] = 'char';
3.char ch[] = "string";
```

### 3.常量

```c
#include <stdio.h>
#define AGE 18
//常量的定义，不适用；隔开，而且常用大写字母来定义命名
int main(){
    printf("his age is %d",AGE);
    return 0;
}
```

