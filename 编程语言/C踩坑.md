# 本章主要记录工作中C/C++遇到过的坑

## 一.构造函数初始化列表中的执行顺序

​    构造函数执行顺序只与成员声明顺序有关，而与初始化表中各项的排列顺序无关

```c++
class A {
private:
	int n1;
	int n2;
public:
	A(): n2(0), n1(n2 + 2)
	{
	}
	void Print()
	{
		std::cout << "n1: " << n1 << ", n2: " << n2 << std::endl;
	}
};

// 输出n1是一个随机的数字，n2为0
```

## 二.Map查找效率问题

​	如下两种查找元素方式，哪种快？

```c++
// 方式一
if(m.count(key) >0 ) {
    return m[key];
}
return nullptr;

// 方式二
iter = m.find(key);
if(iter != m.end()) {
    return iter->second;
}
return nullptr;

// 方式二的的效率更高，方式一进行了2次查找操作
```

## 三.虚函数缺省参数