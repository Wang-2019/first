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
# 3.5
```C++
#include<bits/stdc++.h>
using namespace std;

int main(){
	string s,space,nospace;
	while(cin>>s){
		space+=s;
		space+=' ';
		nospace+=s;
	}
	cout<<"不带空格的是："<<nospace<<endl;
	cout<<"带空格的是："<<space<<endl;
	return 0;
} 
```
# 3.20
```c++
#include<bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v;
	int a;
	for(int i=0;i<10;i++){
		cin>>a;
		v.push_back(a);
	}
	for(int i=0;i<9;i++){
		cout<<v[i]+v[i+1]<<' ';
	}
	cout<<endl;
	cout<<"改写后："<<endl;
	for(int i=0;i<10;i++){
		cout<<v[i]+v[9-i]<<' ';
	}
	return 0;
} 
```
# 3.23
```c++
#include<bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v;
	int q;
	while(cin>>q){
		v.push_back(q);
	}
	for(auto i=v.begin();i!=v.end();i++){
		*i=*i*2;
		cout<<*i<<endl;
	}
	return 0;
} 
```
# 6.10
```C++
#include<bits/stdc++.h>
using namespace std;

void swap1(int *a,int *b){
	int temp;
	temp=*a;
	*a=*b;
	*b=temp;
	return;
}
int main(){
	int a,b;
	cin>>a>>b;
	swap1(&a,&b);
	cout<<a<<' '<<b;
	return 0;
} 
```
	引用类型形参代替指针（如下）
```c++
#include<bits/stdc++.h>
using namespace std;

void swap1(int &a,int &b){
	int temp;
	temp=a;
	a=b;
	b=temp;
	return;
}
int main(){
	int a,b;
	cin>>a>>b;
	swap1(a,b);
	cout<<a<<' '<<b;
	return 0;
} 
```
# 6.19
	(a) 不合法，函数calc只有一个参数，不能传入两个值
	(b) 合法
	(c) 合法
	(d) 合法
# 6.39
	(a) 新函数，作用于int常量
	(b) 不合法，两个函数仅有返回类型不同
	(c) reset是一个函数指针，指向double（double *）函数
# 7.16	
	在类的定义中对于访问说明符出现的位置和次数没有严格限定，
	定义在public说明符后的成员在整个程序内可被访问，public成员定义类的接口
	定义在private说明符后的成员可以被类中的成员访问，但是不能被使用该类的代码访问，private部分封装了类的实现细节
# 7.27
```C++
#include <string>
#include <iostream>

class Screen {
    public:
        using pos = std::string::size_type;

        Screen() = default;
        Screen(pos ht, pos wd):height(ht), width(wd){ }
        Screen(pos ht, pos wd, char c):height(ht), width(wd), contents(ht*wd, c){ }

        char get() const { return contents[cursor]; }
        char get(pos r, pos c) const { return contents[r*width+c]; }
        Screen &move(pos r, pos c);
        Screen &set(char);
        Screen &set(pos, pos, char);
        Screen &display(std::ostream &os) {do_display(os); return *this;}
        const Screen &display(std::ostream &os) const {do_display(os); return *this;}

    private:
        pos cursor = 0;
        pos height = 0, width = 0;
        std::string contents;
        void do_display(std::ostream &os) const {os << contents;}
};

inline Screen &Screen::move(pos r, pos c)
{
	pos row = r * width;
	cursor = row + c;
	return *this;
}

inline Screen &Screen::set(char c)
{
	contents[cursor] = c;
	return *this;
}

inline Screen &Screen::set(pos r, pos col, char c)
{
	contents[r*width + col] = c;
	return *this;
}

int main()
{
	Screen myScreen(5, 5, 'X');	
	myScreen.move(4, 0).set('#').display(std::cout);
	std::cout << "\n";
	myScreen.display(std::cout);
	std::cout << "\n";
	return 0;
}

```
# 7.49
	(a) 合法
	(b) 不合法，Sales_data与Sales_data &不是一个类型
	(c) 不合法，combine本身需要有值传入，所以不应该用const
# 7.58
	类的静态成员不应该在类的内部初始化
	
	
		
