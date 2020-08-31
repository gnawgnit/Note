# 编写延时循环

## 系统时钟

### 头文件

ctime;

### 类型

clock_t//返回的类型，编译器将它转化为适合系统的类型，如long, unsigned int;

### 宏

CLOCKS_PER_SEC//clock函数返回的时间不一定是秒，利用它可将其转化为秒

## 代码

~~~c++
#include <iostream>
#include <ctime>
int main(void)
{
	using namespace std;
	cout<<"times you want to delay: ";
	float secs;
	cin>>secs;
	clock_t delay = secs * CLOCKS_PER_SEC; 
	cout<<"starting"<<endl;
	clock_t start = clock();
	while(clock() -start < delay)
		;
	cout<<"\a\a\a";
	return 0;
}
~~~

