# 2.23
```
  不能
  指针指向的是一个地址空间，并不能确定其地址空间的对象是否合法
```
# 2.24
```
  void类型的指针可以指向任意对象
  
  long类型指针不能使int类型的对象初始化
```

# 2.25
```
（1）
  ip是int类型的空指针，值不确定
  i是int类型，没有赋予初值，所以值也不确定
  r是对i的引用，所以也是int类型，但是值不确定
（2）
  i是int类型，值不确定
  ip是int类型的空指针，值不确定
（3）
  ip是int类型空指针，值不确定
  ip2是int类型，值不确定
```
# 2.35
```
  i是int类型常量
  j是int类型变量
  k是常量引用，绑定到常量i上
  p是int类型指针，指向常量i
  j2是int类型常量
  k2是常量引用，绑定到常量i上
```
```C++
#include<iostream>

int main(){
	const int i = 42;
	auto j = i;
	const auto &k = i;
	auto *p = &i;
	const auto j2 = i,&k2 = i;
	cout <<"i的类型是："<<typeid(i).name()<<endl;
	cout <<"j的类型是："<<typeid(j).name()<<endl;
	cout <<"k的类型是："<<typeid(k).name()<<endl;
	cout <<"p的类型是："<<typeid(p).name()<<endl;
	cout <<"j2的类型是："<<typeid(j2).name()<<endl;
	cout <<"k2的类型是："<<typeid(p2).name()<<endl;
	return 0;
} 
```
# 3.4
比较两字符串是否相等
```C++
#include<bits/stdc++.h>
using namespace std;

int main(){
	string s,t;
	cin>>s>>t;
	if(s>t) cout<<s<<endl;
	else if(s<t) cout<<t<<endl;
	else cout<<"两字符串相等"<<endl;
	return 0;
} 
```
比较两字符串是否等长
```C++
#include<bits/stdc++.h>
using namespace std;

int main(){
	string s,t;
	cin>>s>>t;
	int num1=s.size();
	int num2=t.size();
	if(num1>num2) cout<<s<<endl;
	else if(num1<num2) cout<<t<<endl;
	else cout<<"两字符串相等"<<endl;
	return 0;
} 
```
