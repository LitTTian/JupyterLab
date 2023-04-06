## 文章目录
- 简介
- 基本
- 符运算
	- 算术运算符
	- 逻辑运算符
	- 赋值运算符
	- 格式化输出
	- 向量和矩阵
	- 其他
- 移动数据
- 计算
- 绘图
- 基础语法


## 简介
- GNU Octave is a high-level language primarily intended for numerical computations. It is typically used for such problems as solving linear and nonlinear equations, numerical linear algebra, statistical analysis, and for performing other numerical experiments. It may also be used as a batch-oriented language for automated data processing.

- GNU Octave是一种高级语言，主要用于数值计算。它通常用于求解线性和非线性方程、数值线性代数、统计分析等问题，以及进行其他数值实验。它也可以用作自动化数据处理的面向批处理的语言。

- 这只是做个简单入门，更多的功能可以看一下官方文档：octave.pdf

## 基本
1. 注释 %
	- 类似于C++的//和python的#
2. ans 用于存储输出结果
3. 如果你不喜欢输入行前缀，可以自定义修改PS1('你想改成的内容');
	- 这个不是永久的，你电脑重启之后他又恢复默认了。
4. help 帮助
	- 如果你忘了某一个语句的用法了，可以用这个查询。
	- 比如输入help eye就会显示eye的用法。
5. 多个语句同时执行用逗号分开即可。
	- 输入：`a=4, b=5, c=6`
	- 输出：`a = 4 b = 5 c = 6`
6.  `quit, exit` 可以关闭 Octave
7. `addpath('路径')`添加路径


## 符运算
### 算术运算符
- 加减乘除乘方
```Octave
>> 1+5
ans = 6
>> 1*5
ans = 5
>> 1/5
ans = 0.2000
>> 1-5
ans = -4
>> 5^2
ans = 25
```

### 逻辑运算符
- 等于 `==`
- 不等于 `~=`
- 或 `||`
- 与 `&&`
- 异或 `xor(a,b)`
- 大于等于 `>=`
- 大于 `>`
```octave
>> 1 == 1
ans = 1
>> 1 ~= 2
ans = 1
>> 1 && 2
ans = 1
>> 1 && 0
ans = 0
>> xor(1,1)
ans = 0
>> xor(1,2)
ans = 0
>> xor(0,1)
ans = 1
>> 1 >= 2
ans = 0
>> 1 < 2
ans = 1
```


### 赋值运算符
- `=` 赋值运算符
	- 语句后边加分号 不直接打印赋值语句
	- 语句后边不加分号 直接打印赋值语句
```octave
>>a=1   %a=1后边没分号，所以输入回车之后下一行会直接打印a=1
a = 1
>>a     %再输入a回车看看是否赋值成功
a = 1
>>b=2;  %b=2后边加上分号了，所以下一行不会直接打印b的赋值
>>b     %输入b回车，查看给b的赋值
b = 2   

>>c=pi
c = 3.1416 
```


### 格式化输出
- disp(x)：打印x的值
- disp(sprintf('%0.2f',c))：格式化输出保留两位小数，这个和C语言一样
- format long/short：对整数无影响，对小数输出格式有影响
```octave
>>disp(a)
1
>>disp(c)
3.1416
>>disp(sprintf('%0.2f',c))
3.14

>>format long
>>a
a = 1
>>c
c = 3.141592653589793
>>format short
>>a
a = 1
>>c
c = 3.1416
```

## 向量和矩阵
- 声明矩阵官方原话写的是：

>Vectors and matrices are the basic building blocks for numerical analysis. To create a new matrix and store it in a variable so that you can refer to it later, type the command
>octave:1> A = [ 1, 1, 2; 3, 5, 8; 13, 21, 34 ]
>Octave will respond by printing the matrix in neatly aligned columns.

- 用 `;` 表示该行结束（每行的元素个数得相同，不然会报错`vertical dimensions mismatch (axb vs pxq)`）

```octave
>>martix = [1,2,3;4,5,6;7,8,9]
martix =

   1   2   3
   4   5   6
   7   8   9
```

- 当然还有很多其他写法，虽然不规范也能声明矩阵，这里就不列举了。
- 声明行向量，各个元素之间不用加符号，或者加逗号。

```octave
>>vector=[1 2 3]
vector =

   1   2   3

>>vector = [4;5;6]
vector =

   4
   5
   6
```



### 其他特殊写法：
- `var = start:end` ，从start开始，步长为1，结束条件为当前值超过end
- `var = start:step:end` ，从start开始，步长为step，结束条件为当前值超过end
```octave
> v = 1:5
v =

   1   2   3   4   5

> m = 1:0.5:1
m = 1
octave:3> m = 1:0.5:5
m =

    1.0000    1.5000    2.0000    2.5000    3.0000    3.5000    4.0000    4.5000    5.0000
```

### ones() 和 zeros()
- ones(a,b) 生成a行b列只有1的矩阵
- 除了ones还有zeros，生成的元素都是0，但是没有twos、threes……

```octave
>>ones(2,3)
  ans =

	 1   1   1
	 1   1   1
```

### rand()生成随机数矩阵
- rand(a,b) 生成a行b列的0-1之间随机数的矩阵
```octave
>> rand(2,3)
ans =

   0.5008   0.4421   0.4220
   0.7027   0.3727   0.3048
```

### max()比较最值
- `max(rand(n),rand(n))`生成量个方阵，取其中较大值形成一个新方阵
- TODO
```octave
>> max(rand(4),rand(4))
ans =

   0.8759   0.5264   0.7545   0.5729
   0.7925   0.6617   0.9887   0.5250
   0.8629   0.4952   0.9278   0.3721
   0.9766   0.7445   0.9356   0.9053
```

### rand() 和 randn() 和 randi()

- `randn(a,b) `也是生成a行b列随机数矩阵，但是符合高斯分布（正态分布）。返回一个具有正态分布随机元素的矩阵，这些随机元素的平均值为零，方差为1。

- `randi()`
	- `randi(max,m,n)`：生成1~max之间的整数的m行n列矩阵
	- `randi([min,max],m,n)`：生成min~max之间的整数（min,max也是整数）的m行n列矩阵

```octave
>> randi(5,3,3)
ans =

   3   3   2
   5   4   5
   4   1   3
```

```octave
>> randi([5,10],5,5)
ans =

    9    6    6    8    6
   10    9    5   10    9
    5    7   10    8    8
   10    9    8    9   10
    6    6    9    6   10
```

### 用eye()生成单位阵
- eye(n) 生成n维单位矩阵
```octave
>> eye(5)
ans =

Diagonal Matrix

   1   0   0   0   0
   0   1   0   0   0
   0   0   1   0   0
   0   0   0   1   0
   0   0   0   0   1
```

### 矩阵截取
- A(rows, columns)：将矩阵A按rows和columns中的条件进行截取并返回新矩阵，一共有以下几种方式
	- `x:y`：将矩阵A的x~y行(或列)截取
	- `:` ：表示所有元素
	- `[a b c]`：表示abc三行(或列)
- 以上三种表示方法在矩阵别的方法中也能使用，比如赋值、打印

```octave
>> A = rand(5)
A =

   0.018339   0.569209   0.907383   0.207075   0.153661
   0.469141   0.379134   0.632806   0.949094   0.956941
   0.166895   0.374863   0.783764   0.957568   0.480624
   0.489357   0.912601   0.847389   0.598284   0.291636
   0.119078   0.143597   0.514801   0.811196   0.465625

>> B = A(1:2, 2:4)
B =

   0.5692   0.9074   0.2071
   0.3791   0.6328   0.9491
>> A([1 4 2], 3:4)
ans =

   0.9074   0.2071
   0.8474   0.5983
   0.6328   0.9491
```

### 矩阵拼接

- 横向拼接：`C = [A, B]` 或 `C = [A B]` 
- 纵向拼接：`C = [A; B]`  
	- 在矩阵右侧添加一列
```octave
>> A = [A,[2;4;5;1;2]]
A =

   0.018339   0.569209   0.907383   0.207075   0.153661   2.000000
   0.469141   0.379134   0.632806   0.949094   0.956941   4.000000
   0.166895   0.374863   0.783764   0.957568   0.480624   5.000000
   0.489357   0.912601   0.847389   0.598284   0.291636   1.000000
   0.119078   0.143597   0.514801   0.811196   0.465625   2.000000
```


### matrix(:) 列向量
- `A(:)` 将矩阵A中的所有元素放入一个列向量
```
氀愀 栀猀昀渀ힲ⺹>> A(:)
ans =

   0.018339
   0.469141
   0.166895
   0.489357
   0.119078
   0.569209
   0.379134
   0.374863
   ...
```






### 检测大小

- `size()`：检测矩阵的大小
	- `size(A)`：输出行数和列数
	- `size(A, type)`：type = 1输出行数，type = 2输出列数
- `length(A)`：返回行数和列数中较长的

```octave
>> A
A =

   0.018339   0.569209   0.907383   0.207075   0.153661   2.000000
   0.469141   0.379134   0.632806   0.949094   0.956941   4.000000
   0.166895   0.374863   0.783764   0.957568   0.480624   5.000000
   0.489357   0.912601   0.847389   0.598284   0.291636   1.000000
   0.119078   0.143597   0.514801   0.811196   0.465625   2.000000

>> size(A)
ans =

   5   6

>> size(A,1)
ans = 5
>> size(A,2)
ans = 6
>> length(A)
ans = 6
```

## 系统常用指令

### 变量操作
- 显示当前变量
	- `who`：显示目前所有变量
	- `whos`：显示目前所有变量和详细信息
```octave
>> who
Variables visible from the current scope:

A      C      ints   B      ans

>> whos
Variables visible from the current scope:

variables in scope: top scope

  Attr   Name        Size                     Bytes  Class
  ====   ====        ====                     =====  =====
         A           5x6                        240  double
         B           2x3                         48  double
         C           5x12                       480  double
         ans         1x1                          8  double
         ints        2x3                         48  double

Total is 207 elements using 824 bytes
```

- 删除变量 clear
	- `clear 变量名`：删除指定名称的变量
	- `clear`：删除所有变量
```octave
>> clear x
>> x
error: 'x' undefined near line 1, column 1
```


### 文件指令
- 用过其他命令行的应该能适应，octave也同样支持某些命令。

- pwd：列出当前目录
- cd xxx：进入xxx目录
- ls：列出当前目录信息
- `load('fname')` 或 `load fname` 加载文件：
	- featureA是一个列数为二的矩阵，使用load读取其中的数组并复制给同文件名的变量
```octave
>> load featureA
>> featureA
featureA =

2104  3
1600  3
2400  3
1416  2
3000  4
1985  4
1534  3
1427  3
1380  3
...
```
- save 文件名 变量; ：将变量保存到文件中，比如save data.txt num，把num变量保存到data.txt中（如果操作目录中没有这个文件会创建一个新文件，如果目录中有这个文件会重写）




## 矩阵的操作

### 矩阵的转置和对称
- `martix'`：返回martix的转置
```octave
>> A
A =

   0  -1  -2   0  -1  -1
   0  -1  -1   2  -1  -2
  -2   0   2   0   1   1
  -1  -2  -2   0   0   0
   2   2  -2   0  -2   2

>> A'
ans =

   0   0  -2  -1   2
  -1  -1   0  -2   2
  -2  -1   2  -2  -2
   0   2   0   0   0
  -1  -1   1   0  -2
  -1  -2   1   0   2
```
- `flipud(A)`：矩阵垂直对称，利用`flipud`，我们还可以实现矩阵水平对称：`flipud(A')'`

```octave
>>AA =

   6   6   9
   7   8   4

>> flipud(A)
ans =

   7   8   4
   6   6   9
   
>> flipud(A')'
ans =

   9   6   6
   4   8   7

>> A
A =

   6   6   9
   7   8   4

```

### 矩阵的运算
- 除了最开始提到的算术运算符，还有以下运算。
- 矩阵比较`>`，`A>B`或`A>n`：判读A中每个元素
- 矩阵乘法`*`， `A*B`：A的列数等于B的行数
- 矩阵除法`/`， `A/B`：A乘以B的逆
- 矩阵的幂`^`，`A^n`：矩阵A的n次幂
- `.`表示为矩阵中每个元素单独进行计算
	- 矩阵元素加`.+-`：已经被deprecated， 用`+-`代替
	- 矩阵元素乘`.*`:
		- `A.*B`：A和B必须同型，同位的数相乘
		-  `A.n`：A中每个元素乘以n
	- 矩阵元素除`./`:同元素乘
	- 矩阵元素幂`.^`：
		- `A.^B`：A和B必须同型，A中元素对应B中同位元素求幂
		- `A.^n`：计算A中每个元素的n次幂

```octave
>> A = randi(5, 2, 3)
A =

   5   4   4
   2   3   4

>> B = randi(5, 2, 3)
B =

   4   4   1
   1   1   5

>> A*B
error: operator *: nonconformant arguments (op1 is 2x3, op2 is 2x3)
>> A .* B
ans =

   20   16    4
    2    3   20
```


## 常用函数
### 对数和指数

- `log(n)`：log e 底 n
- `logm(n)`：log m 底 n​
	- m只能为数字，n可以是数字，可以是矩阵

```octave
>> log(10)
ans = 2.3026
>> log2(16)
ans = 4
>> A =

   1   3   1
   4   2   2

>> log(A)
ans =

        0   1.0986        0
   1.3863   0.6931   0.6931
```

- `exp(n)`：e的n次幂
```octave
>> exp(5)
ans = 148.41
>> exp(A)
ans =

    2.7183   20.0855    2.7183
   54.5982    7.3891    7.3891
```

### 绝对值函数

- `abs(n)`：求n(或n中每个元素)的绝对值
```octave
>> A = randi([-2,2], 5, 6)
A =

   0  -1  -2   0  -1  -1
   0  -1  -1   2  -1  -2
  -2   0   2   0   1   1
  -1  -2  -2   0   0   0
   2   2  -2   0  -2   2

>> abs(A)
ans =

   0   1   2   0   1   1
   0   1   1   2   1   2
   2   0   2   0   1   1
   1   2   2   0   0   0
   2   2   2   0   2   2
```





magic(n)生成n阶幻方，所谓幻方就是行、列、对角线加起来都是相同的值

octave:95> magic(4)
ans =

   16    2    3   13
    5   11   10    8
    9    7    6   12
    4   14   15    1

octave:96> magic(3)
ans =

   8   1   6
   3   5   7
   4   9   2
1
2
3
4
5
6
7
8
9
10
11
12
13
14
find(公式)

找到向量中符合的数据并返回其索引
a =

   1   5   3   4

octave:88> find(a<3)
ans = 1
octave:89> find(a>2)
ans =

   2   3   4
1
2
3
4
5
6
7
8
9
10
找到矩阵中符合的数据
C =

9    7    3    5
4    2    5   10
4    1    9   10

octave:114> [r,c]=find(C==1)
r = 3
c = 2
octave:115> [r,c]=find(C>7)
r =

   1
   3
   2
   3

c =

   1
   3
   4
   4

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
sum()求和prod()求积

c =

   1
   3
   4
   4

octave:117> sum(c)
ans = 12
octave:118> prod(c)
ans = 48
1
2
3
4
5
6
7
8
9
10
11
floor()向下取整ceil()向上取整

a =

   0.5000
   1.5000
   2.0000
   2.0000

octave:120> floor(a)
ans =

   0
   1
   2
   2
   
octave:121> ceil(a)
ans =

   1
   2
   2
   2


1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
max(矩阵)取最大值
如果是矩阵，那就显示每一列的最大值；如果是向量，那就只显示一个最大值

v=max(matrix)：将矩阵的最大值赋给v，不是硬性要求，v可以换别的名称
[v,i]=max(matrix)：将矩阵最大值及其位置赋值给v和i
max(max(matrix))：取得整个矩阵最大值
max(matrix(:))：取得整个矩阵最大值，这个是将矩阵转化成响亮之后再求最大值
c =

   2   1   4   1
   5   2   1   1
   1   1   5   4

octave:78> val = max(c)
val =

   5   2   5   4

octave:79> [val,ind]=max(c)
val =

   5   2   5   4

ind =

   2   2   3   3

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
max(矩阵,[],1/2) 取得矩阵每一行或者列的最大值形成一个向量

1 取每一列
2 取每一行
c =

   8   9   7   9
   9   3   9   5
   7   2   5   9
   7   5   6   5

octave:129> max(c,[],1)
ans =

   9   9   9   9

octave:130> max(c,[],2)
ans =

   9
   9
   9
   7

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
小练习：
生成一个幻方，然后测试其每行，每列，对角线之和都是同一个数

octave:131>  m = magic(5)     %生成一个5×5的幻方
m =

   17   24    1    8   15
   23    5    7   14   16
    4    6   13   20   22
   10   12   19   21    3
   11   18   25    2    9

octave:132> sum(m,1)          %每列相加都是65
ans =

   65   65   65   65   65

octave:133> sum(m,2)          %每行相加都是65
ans =

   65
   65
   65
   65
   65
   
octave:135> e=eye(5)          %生成一个单位矩阵
e =

Diagonal Matrix

   1   0   0   0   0
   0   1   0   0   0
   0   0   1   0   0
   0   0   0   1   0
   0   0   0   0   1

octave:136> result1 = e .* m   %单位矩阵同位相乘原矩阵，新矩阵只剩主对角线元素
result1 =

   17    0    0    0    0
    0    5    0    0    0
    0    0   13    0    0
    0    0    0   21    0
    0    0    0    0    9
octave:139> sum(result1(:))   %主对角线相加为65
ans = 65

octave:141> result2 = m .* flipud(e)
result2 =

    0    0    0    0   15
    0    0    0   14    0
    0    0   13    0    0
    0   12    0    0    0
   11    0    0    0    0

octave:142> sum(result2(:))   %副加为65
ans = 65

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
pinv()求逆矩阵

m =

   8   1   6
   3   5   7
   4   9   2

octave:145> pinv(m)
ans =

   0.147222  -0.144444   0.063889
  -0.061111   0.022222   0.105556
  -0.019444   0.188889  -0.102778
1
2
3
4
5
6
7
8
9
10
11
12
绘图
plot(A,B)A是横坐标向量，B纵坐标

octave:173> t=[-1:0.01:1];
octave:174> p1 = sin(2*pi*t);
octave:175> plot(t,p1)
1
2
3


octave:176> p2 = cos(2*pi*t);
octave:177> plot(t,p2)
1
2


画完一张图以后想要画另一张就会重新绘制，用hold on可以保留，在原图基础上继续画，并且会自动给你切换颜色。

octave:177> plot(t,p2)
octave:178> hold on
octave:179> plot(t,p1)
1
2
3


给横轴纵轴添加标签。

octave:183> xlabel('time')
octave:184> ylabel('speed')
1
2


添加图例

legend('cos','sin','y')
1


添加标题

title('my demo')
1


保存文件

print -dpng '文件名'
1
保存之后你的当前目录下边就会多出一个图片。如过你不知道当前目录是啥，输入pwd查看当前目录的路径。

如果你想同时生成多个图片，那在前边加上figure(n);则会按顺序生成图片。

octave:194> figure(1);plot(t,p1)
octave:195> figure(2);plot(t,p2)
1
2


合并显示图像subplot(n,m,index)，将图像分成n行m列，取index位置绘图。

octave:197> subplot(2,3,4)
octave:198> plot(t,p1)
octave:199> subplot(2,3,2)
octave:200> plot(t,p2)
1
2
3
4


改变纵横轴取值范围axis([横轴起始 终止 纵轴起始 终止])

octave:203> subplot(1,2,1)
octave:204> plot(t,p2)
octave:205> subplot(1,2,2)
octave:206> plot(t,p2)
octave:207> axis([0 1 -2 2])
1
2
3
4
5
下图两个是同一副图，右边是改变坐标轴范围之后的图像。



clf清空整幅图，close不用点右上角×关闭图像

矩阵可视化
imagesc()

a =

   8   1   6
   3   5   7
   4   9   2

octave:217> imagesc (a)
1
2
3
4
5
6
7


说个题外话，作为一个曾经的生物学生，我好像突然get到了我们以前的热图是怎么出来的。

octave:218> load 6feature.txt   % 还记得这组数据吗，就是我上边给的那两组数据的第一组。
octave:219> imagesc (X6feature)
1
2
画出来以后图像长这样，恩我真的get到热图怎么画的了。



现在让我们生成一个热图（假的，不是热图，看起来像而已）

octave:220> r = rand(5,50);
octave:221> imagesc (r)
1
2


colorbar添加比色的图例。

octave:223> colorbar
1


colormap gray使其变为灰度图

 colormap gray
1


基础语法
循环

for var = expression 
body 
endfor
1
2
3
while (condition) 
body 
endwhile
1
2
3
其实上边的endwhile，endfor还有下边的endif可以直接写为end
break、continue也可以用
判断

if (condition) 
    then-body 
endif
1
2
3
if (condition) 
    then-body 
elseif (condition) 
    elseif-body 
else 
    else-body 
endif
1
2
3
4
5
6
7
举个栗子

v =

   8    4    8    2    5
   7    4    6    1    3
  10    6    6    4   10
   6    6    8    8   10
   9    1   10    5    7

> for i = 1:5
>     for j = 1:5
>         if v(i,j)<5
>             continue
>         else
>             disp(v(i,j))
>         endif
>     endfor
> endfor
8
8
5
7
6
10
6
6
10
6
6
8
8
10
9
10
5
7

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
函数

普无返回值的函数
function name 
    body 
endfunctio
1
2
3
带返回值的函数
function [ret-list] = name (arg-list) 
    body 
endfunction
1
2
3
在octave中写函数：

>function say_hi(name)
> str = ['hello' name];
> disp(str)
> endfunction
>say_hi ('Sian')
helloSian
1
2
3
4
5
6
让octave使用外部的函数。

在当前目录或者path中放你的函数文件
文件名就是函数名
后缀.m
举个栗子
现在写一个函数show_matrix：



存放在path中，并且命名为show_matrix.m



回到octave中声明一个矩阵，看看是否能用该函数成功打印



再整一个带返回值的



## hist()直方图

- `hist(x)`：统计x在不同范围中的数据个数
- `hist(x,a)`：将范围(横坐标)分为a份