---
layout: post
title:  "C++的标准库"
tags:C++(standard-library)
---
# 今天是关于学习C++的标准库的相关内容

<h3>STRING</h3>

```c++
#include<iostream>
#include<string>
using namespace std;
int main(){
  string s;
  cin>>s;    
  //当有字符出现后遇空白（空格符，换行符，制表符）便终止
  //如输入”sdjajsd  1321weia“  输入的结果将只会为sdjajsd
  cout<<s<<endl;
  return 0;
}

```
string的empty()函数

```c++

string s;
while(getline(cin,s)){//每次都一行
	if(!s.empty()){    //去掉空行
		cout<<s<<endl;
	}
}
return 0;
```
string的size()函数

```c++
string s;
while(getline(cin,s)){
	if(s.size()>80){  //当一行中的字符超过80时才读出
		cout<<s<<endl;
	}
}
return 0;
```
###### 切记字符串字面值与string是不同的类型

string类的输入运算符是遇到空白便停止，空白包括（空格，换行符，制表符）

而getline函数是读取一行，包括最后的换行符，然后去掉最后的换行符将所读内容赋值给string对象中

### 处理string对象中的字符

在c++中cctype头文件中定义了一组标准库函数处理这部分工作

常用的有：

```c++
isalunm(c)       //当c是字母或数字时为真
isalpha(c)       //当c是字母时为真
isdigit(c)       //当c是数字时为真
islower(c)       //若c为小写则返回真
isupper(c)       //若c为大写则返回真
tolower(c)       //将c变为小写
toupper(c)       //将C变为大写字母
isspace(c)       //当c是空白时为真
ispunct(c)       //当c是标点符号时为真
```
想处理每个字符，最好使用基于范围的for语句

```c++
for(declaration:expression)
	statement
```
较为坑的是由于现在大学的几乎所有自带IDE都是VS2010，但是VS2010不支持基于范围的for语句，线程等。。。。。，若是你要去一些大学内部的考点的话，，咳咳，，那就跟我一样尴尬了。。。。囧。。

在这种情况下你要想全部遍历的话便只能用类似如下的代码。。

```c++
for(int i=0;i<s.size();++i){		
		char c=s[i];     //或类似string c=s.substr(i,1);
		cout<<c<<endl;
	}
```

所以这就很坑爹了，有一点其实我是真的不太明白，为什么到现在大学还都是用什么VC++6.0 VS2005 VS2010 这种已经早就几乎被所以程序员弃用的IDE。。。与时俱进多好，，哈哈，小小吐槽一下下，不喜勿喷



如果我们不需要处理每一个字符，要访问单个字符时，便可利用下标和迭代器

需要注意的是使用下标时要注意下标>=0且小于所要访问字符串的大小，若是越界，变可能发生不可预知的错误，所以我们也不能对空字符串进行下标访问

顺便提一句 `decltype`为返回相关类型，例如s.size()返回类型为string::size_type,是无符号整数

<h3>Vector</h3>

Vector是模板而非类型，由vector生成的类型必须包含vector中元素的类型，例如

`vector<int> vector<类> vector<vector<string>> ` 等

对于vector来说，最常见的方式就是先定义一个空的vertor然后当运行时获取到元素的值再逐一添加 

对于vector也有一些常用函数如：

```c++
	v.empty()         //如果v不含有任何元素，返回真，否则返回假
	v.size()          //返回v中元素的个数
	v.push_back(t)    //向v的尾端添加一个值为t的元素
	v[n]              //返回对v中的第N个元素的引用
	v1=v2             //将v2拷贝赋予v1
	v1={a,b,c...}     //列表初始化
	v1==v2            //判断相等
	v1!=v2            //不等
```
对空vector添加元素时，不能用下标形式添加，只能用`v.push_back(t)`

用一个小例子来演示一下vector

读入一组整数并把他们存入一个vector对象，将每对相邻整数的和输出，

和将第一个数与最后一个数的和输出，第二个与倒数第二个数的和输出

代码如下

```c++
	vector<int>  v;
    int x,i=0;
	while(cin>>x){
		v.push_back(x);
		++i;
		if(i>=10){
			break;
		}
	}
	for(decltype(v.size()) index=0;index!=v.size()-1;++index){
		cout<<v[index]+v[index+1]<<" ";
	}
	cout<<endl;
	 for(decltype(v.size())index=0,indexi=v.size()
	 ;index!=indexi;++index,--indexi)
	{
		cout<<v[index]+v[indexi-1]<<" ";
	}	
```
<h3>迭代器</h3>

迭代器都拥有 `begin`  `end` 这两个成员， `begin` 负责指向第一个元素的迭代器； `end` 为尾后迭代器，指向最后一个的后面，若容器为空 `begin` 与 `end` 指向同一个元素的迭代器，均为尾后迭代器

标准容器迭代器的运算符

```c++
*iter          //对iter所指元素的引用
iter->mem      
++iter         //指向下一个
--iter         //指向上一个
iter1==iter2   //两者相等条件指向同一元素或同为尾后迭代器时相等，否则不相等
iter1!=iter2
```
在使用for循环时，我们用了 `！=` 做了判断，而不是 `<` 这是因为有些迭代器没有 `<` 运算符，而都有 `!=` 所以都能使用，这有个泛型编程的概念



谨记，但凡是使用了迭代器的循环体，均不能向迭代器所属容器添加元素





<h3>以上内容均是C++Primer中的内容</h3>

​    
