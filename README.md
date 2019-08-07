# C++学习记录
记录知识盲点

## 1. 基础知识

### 1.1 信息的储存单位
* 位（bit,b)
> 数据的最小单位，表示一位二进制信息
* 字节(byte,B)
> 八位二进制数字组成（1byte=8bit）

### 1.2 R进制缩写
* 二进制：BIN
* 八进制：OCT
* 十进制：DEC
* 十六进制：HEX

### 1.3 R进制->十进制
各位数字与它的权相乘，其积相加
> 例：二进制的1111<sub>2</sub>转换成十进制  
1×2<sup>3</sup>+1×2<sup>2</sup>+1×2<sup>1</sup>+1×2<sup>0</sup>=8+4+2+1=15<sub>10</sub>

### 1.4 十进制整数->R进制整数
除以R取余
> 例：十进制的68<sub>10</sub>转换成二进制  
68/2=34(余数0）  
34/2=17(余数0）  
17?2=8(余数1）  
……  
1/2=0(余数1）  
低位->高位  
得：1000100<sub>2</sub>

### 1.5 十进制小数->R进制小数
乘以R取整
> 例：十进制的0.3125<sub>10</sub>转换成二进制  
0.3125×2=0.625  
0.625×2=1.25  
0.25×2=0.5  
0.5×2=1.0  
高位->低位  
得：0.0101<sub>2</sub>

### 1.6 模数
n位二进制整数的模数为2<sup>n</sup>  
n位小数的模数为2

### 1.7 补数
一个数减去另一个数（加一个负数）  
等于第一个数加第二个数的补数
> 例：8+(-2)=8+10(mod 12)=6

### 1.8 反码的计算规则
1. 负整数：  
原码符号位不变（仍是1）  
其余各位取反（0变1，1变0）
> 例：X=-1100110  
X<sub>原</sub>=11100110  
X<sub>反</sub>=10011001
2. 正整数：原码就是补码

### 1.9 补码的计算规则
反码：作为中间码  
> 负数补码=反码+1  
正数补码=原码

## 2. C++基础知识

### 2.1 标识符
程序员声明的单词，它命名程序正文中的一些实体

#### 标识符的构成规则
* 以大写字母、小写字母活下划线开始
* 可以由以大写字母、小写字母、下划线或数字0~9组成
* 大写字母和小写字母代表不同标识符
* 不能是C++关键字或操作符

### 2.2 整数常量

#### 十进制
若干个0~9的数字，但数字部分不能以0开头，正数前边的正号可以省略

#### 八进制
前导0 +若干0~7的数字

#### 十六进制
前导0x +若干个0\~9的数字以及A\~F的字母（大小写均可）

#### 后缀
* 后缀L（或l）表示类型至少是long
* 后缀LL（或ll）表示类型是long long
* 后缀U（或u）表示unsigned类型

### 2.3 浮点数常量
#### 一般形式
> 例：12.5，-12.5等

#### 指数形式
整数部分和小数部分可以省略其一
> 例：0.345E+2，-34.4E-3

#### 默认形式
为double型，如果后缀F（或f）可以使其成为float型
> 例：12.3f

### 2.4 转义字符
* \a 响铃
* \n 换行
* \t 水平制表符
* \v 垂直制表符
* \b 退格
* \r 回车
* \f 换页
* \\ \
* \" "
* \' '
* \? ?

### 2.5 字符串常量
* 一对双引号括起来的字符序列
* 在内存中按串中字符的排列次序顺序存放，每个字符占一个字节
* 在末尾添加'\0'作为结尾标记

> 例：  
> "CHINA" C H I N A \0  
> "a" a \0  
> 'a' a

#### 字符串前缀类型
* u char16_t Unicode16字符
* U char32_t Unicode32字符
* L wchar_t 宽字符
* u8 UTF-8（仅用于字符串字面常量） char

### 2.6 变量初始化方式
* int a=0
* int a(0)
* int a={0}
* int a{0}

> 使用大括号的方式被称为列表初始化，此时不允许信息的丢失。例如用double值初始化int变量，就会造成数据丢失

### 2.7 符号常量
#### 定义语句的形式
* const 数据类型说明符 常量名=常量值
* 或 数据类型说明符 const 常量名=常量值

> 例：const float PI=3.1415926

* 符号常量在定义时一定要初始化，在程序中间不能改变其值

### 2.8 运算符与表达式
#### 逗号运算符和逗号表达式
* 格式：表达式1,表达式2
* 求解顺序及结果
    * 先求解表达式1，再求解表达式2
    * 最终结果为表达式2的值

> 例：a=a\*5,a\*4，最终结果为60

#### 条件运算符与条件表达式
* 一般形式
    * 表达式1?表达式2:表达式3
    * 表达式1必须是bool类型

* 执行顺序
    * 先求解表达式1
    * 若表达式1的值为true，则求解表达式2，表达式2的值为最终结果
    * 若表达式1的值为false，则求解表达式3，表达式3的值为最终结果

#### sizeof运算符
* 语法形式：sizeof(类型名) 或 sizeof 表达式
* 结果值：“类型名”所指定的类型，或“表达式”的结果类型所占的字节数

> 例：sizeof(short)  
> sizeof x

#### 位运算符
1. 按位与（\&）
    * 运算规则：将两个运算量的每一个位进行逻辑与操作
    * 用途举例1：将某一位置0，其他位不变

    > 例：将char型变量a的最低位置0：a=a\&0xfe
    
    * 用途举例2：取出指定位

    > 例：有char c; int a; 取出a的低字节，置于c中：c=a\&0xff

2. 按位或（\|）
    * 运算规则：将两个运算量的每一个位进行逻辑或操作
    * 用途举例：将某些位置1，其他位不变
    
    > 例：将int型变量a的低字节置1：a=a\|0xff

3. 按位异或（\^）
    * 运算规则：对应位形同则为0，不同则为1
    * 用途举例：使特定位翻转（与0异或保持原值，与1异或取反）
    
    > 例：要使01111010低四位翻转：01111010\^00001111，得01110101

4. 按位取反（\~）
    * 运算规则：单目运算符，对一个二进制数按位取反
    
    > 例：  
    > 025：0000000000010101  
    > \~025：1111111111101010

5. 移位（<<、>>）
    * 左移运算（<<，相当于乘以2）：左移后，低位补0，高位舍弃
    * 右移运算（>>，相当于除以2）：右移后，低位舍弃，高位（无符号数补0，有符号数补“符号位”）

#### 数据类型的转换
1. 隐含转换
    * 一些二元运算符（算术运算符、关系运算符、逻辑运算符、位运算符和赋值运算符）要求两个操作数的类型一致
    * 在算数运算和关系运算中，如果参与运算的操作数类型不一致，编译系统会自动对数据进行转换（即隐含转换），基本原则是将低类型的数据转换为高类型的数据

2. 显式转换
    * 显式类型转换的作用是将表达式的结果类型转换为类型说明符所制定的类型
    * 语法形式：
    
    > C:类型说明符(表达式)  
    > C:(类型说明符)表达式  
    > C++:类型转换操作符<类型说明符>(表达式)
    
    * 类型转换操作符：
    
    > const_cast、dynamic_cast、reinterpret_cast、static_cast  
    > 例：int(z), (int)z, static_cast\<int\>(z)三种完全等价

### 2.9 常用I/O流类库操纵符

| 操纵符名 | 含义 |
| :-: | :-: |
| dec | 数值数据采用十进制表示 |
| hex  | 数值数据采用十六进制表示 |
| oct | 数值数据采用八进制表示 |
| ws | 提取空白符 |
| endl | 插入换行符，并刷新流 |
| ends | 插入空字符 |
| setsprecision(int) | 设置浮点数的小数位数（包括小数点） |
| setw(int) | 设置域宽 |

> 例：cout<<setw(5)<<setsprecision(3)<<3.1415;

### 2.10 控制语句
* break语句

> 使程序从循环体和switch语句内调出，继续执行逻辑上的下一条语句。不宜用在别处

* continue语句

> 结束本次循环，接着判断是否执行下一次循环

* goto语句

> 使程序的执行流程跳转到语句标号所指定的语句。不提倡使用

### 2.11 自定义类型
#### 类型别名：为已有类型另外命名
* typedef 已有类型名 新类型名表

> 例：typedef double Area, Volume;  
> typedef int Natural;  
> Natural i1,i2;  
> Area a;  
> Volume v;  

* using 新类型名=已有类型名

> 例：using Area=double  
> using Volume=double

#### 枚举类型
* 定义方式：将全部可取值一一列举出了
* 语法形式（不限定作用域）：enum 枚举类型名 {变量值列表}

> 例：enum Weekday {SUN,MON,TUE,WED,THU,FRI,SAT}

* 枚举元素是常量，不能对它们进行赋值。不能写复制表达式：SUN=0
* 元素默认值，依次为：0,1,2,……
* 可以在声明时另行指定枚举元素的值

> 如：enum Weekday {SUN=7,MON=1,TUE,WED,THU,FRI,SAT}

* 枚举值可以进行关系运算
* 整数值不能直接赋值给枚举变量。如需要将整数赋值给枚举变量，应进行强制类型转换
* 枚举值可以赋给整型变量

#### auto类型与decltype类型
* auto：编译器通过初始值自动推断变量的类型

> 例：auto val=val1+val2  
> 如果val1+val2是int类型，则val是int类型

* decltype：定义一个变量与某一表达式的类型相同，但并不用该表达式初始化变量

> 例：decltype(i)j=2  
> 表示j以2作为初始值，类型与i一致

## 3. 函数
* 函数：定义好的，可重用的功能模块
* 定义函数：将一个模块的算法，用C++描述出来
* 函数名：功能模块的名字
* 函数的参数：计算所需要的数据和条件
* 函数的返回值：需要返回的计算结果

### 3.1 函数定义的语法形式
类型标识符 函数名(形式参数表)
{
语句序列
}

* 形式参数表：
    * \<type1>name1,\<type2>name2,...\<typen>namen  
    * 是被初始化的内部变量，寿命和可见性仅限于函数内部  
* 类型标识符
    * 表示返回值类型，由return语句给出返回值
    * 若无返回值，写void，不必写return语句

### 3.2 函数的调用
* 调用函数前需要先声明函数原型
* 声明格式：类型标识符 被调用函数名(含类型说明的形参表)
* 调用格式：函数名(实参列表)
* 嵌套调用：在一个函数的函数体中，调用另一函数
* 递归调用：函数直接或间接调用自身

### 3.3 函数的参数传递
* 在**函数被调用**时才分配形参的储存单元
* 实参可以使**常量**、**变量**或**表达式**
* 实参**类型必须**与形参**相符**
* 值传递是传递参数值，即**单向传递**
* 引用传递可以实现**双向传递**
* 常引用作参数可以保障实参数据的安全

### 3.4 引用类型
* 引用(&)是**标识符的别名**
* 定义一个引用时，必须同时对它进行初始化，使它指向一个已存在的对象

> 例：int i, j;  
> int &ri = i; //定义int引用ri，并初始化为变量i的引用  
> j = 10;  
> ri = j; //相当于i = j

* 一旦一个引用被初始化后，就不能改为指向其他对象
* 引用可以**作为形参**（双向传递）

### 3.5 含有可变参数的函数
* C++标准中提供了两种主要的方法
    * 如果所有的实参类型相同，可以传递一个名为initializer_list的标准库类型
    
    > ininitializer_list是一种标准库类型，用于表示某种特定类型的值的数组，该类型定义在同名的头文件中  
    
    * 如果实参的类型不同，我们可以编写可变参数的模板

#### initializer_list的使用方法
* initializer_list是一个类模板
* 使用模板时，我们需要在模板名字后面跟一对尖括号，括号内给出类型参数。

> 例：initializer_list<string> ls; //initializer_list的元素类型是string  
> initializer_list<int> li; //initializer_list的元素类型是int

* initializer_list比较特殊的一点是，其对象中的元素永远是常量值，我们无法改变initializer_list对象中元素的值
* 含有initializer_list形参的函数也可以同时拥有其他形参

#### initializer_list使用举例
* 在编写代码输出程序产生的错误信息时，最好统一用一个函数实现该功能，使得对所有错误的处理能够整齐划一。然而错误信息的种类不同，调用错误信息输出函数时传递的参数也会有不相同
* 使用initializer_list编写一个错误信息输出函数，使其可以作用域可变数量的形参

### 3.6 内联函数
* 内联函数声明时使用关键字inline
* 编译时在调用处用函数体进行替换，节省了参数传递，控制转移等开销

#### 注意
* 内联函数体内不能有循环语句和switch语句
* 内联函数的定义必须出现在内联函数第一次被调用之前
* 对内联函数不能进行异常接口声明

### 3.7 constexpr（常量表达式）函数
* constexpr修饰的函数，在其所有参数都是constexpr时，一定返回constexpr

> 例：constexpr int get_size(){return 20;}  
> constexpr int foo = get_size(); //正确：foo是一个常量表达式

### 3.8 函数重载
* C++允许功能相近的函数在相同的作用域内以相同函数名声明，从而形成重载。方便使用，便于记忆。

#### 注意事项
* 重载函数的形参必须不同：**个数**不同或**类型**不同
* 编译程序将根据实参和形参的类型及个数的最佳匹配来选择调用哪一个函数
    * 编译器不以**形参名**来区分
    * 编译器不以**返回值**来区分
* 不要将不同功能的函数声明为重载函数，以免出现调用结果的误解、混淆

### 3.9 C++的系统函数
* C++的系统库中提供了几百个函数可供程序员使用，例：
    * 求平方根函数（sprt）
    * 求绝对值函数（abs）
* 使用系统函数是要包含相应的头文件，例：
    * cmath
