## 一、介绍

pair是将2个数据组合成一组数据，当需要这样的需求时就可以使用pair，如stl中的map就是将key和value放在一起来保存。另一个应用是，当一个函数需要返回2个数据的时候，可以选择pair。 pair的实现是一个结构体，主要的两个成员变量是first second 因为是使用struct不是class，所以可以直接使用pair的成员变量。

pair是一种关联类型，不是容器。

其标准库类型--pair类型定义在#include 头文件中，定义如下：

类模板：template<class T1,class T2> struct pair

参数：T1是第一个值的数据类型，T2是第二个值的数据类型。

功能：pair将一对值(T1和T2)组合成一个值，

```
这一对值可以具有不同的数据类型（T1和T2），

两个值可以分别用pair的两个公有函数first和second访问。
```

定义(构造函数)：

```cpp
pair<T1, T2> p1; //创建一个空的pair对象（使用默认构造），它的两个元素分别是T1和T2类型，采用值初始化。
pair<T1, T2> p1(v1, v2); //创建一个pair对象，它的两个元素分别是T1和T2类型，其中first成员初始化为v1，second成员初始化为v2。
make_pair(v1, v2); // 以v1和v2的值创建一个新的pair对象，其元素类型分别是v1和v2的类型。
p1 < p2; // 两个pair对象间的小于运算，其定义遵循字典次序：如 p1.first < p2.first 或者 !(p2.first < p1.first) && (p1.second < p2.second) 则返回true。
p1 == p2； // 如果两个对象的first和second依次相等，则这两个对象相等；该运算使用元素的==操作符。
p1.first; // 返回对象p1中名为first的公有数据成员
p1.second; // 返回对象p1中名为second的公有数据成员
```

## 二、pair的创建和初始化

pair包含两个数值，与容器一样，pair也是一种模板类型。但是又与之前介绍的容器不同；

在创建pair对象时，必须提供两个类型名，两个对应的类型名的类型不必相同

```cpp
pair<string, string> anon; // 创建一个空对象anon，两个元素类型都是string
pair<string, int> word_count; // 创建一个空对象 word_count, 两个元素类型分别是string和int类型
pair<string, vector<int> > line; // 创建一个空对象line，两个元素类型分别是string和vector类型
```

当然也可以在定义时进行成员初始化：

```cpp
pair<string, string> author("James","Joy"); // 创建一个author对象，两个元素类型分别为string类型，并默认初始值为James和Joy。
pair<string, int> name_age("Tom", 18);
pair<string, int> name_age2(name_age); // 拷贝构造初始化
```

pair类型的使用相当的繁琐，如果定义多个相同的pair类型对象，可以使用typedef简化声明：

```cpp
typedef pair<string,string> Author;
Author proust("March","Proust");
Author Joy("James","Joy");
```

变量间赋值

```cpp
pair<int, double> p1(1, 1.2);
pair<int, double> p2 = p1; // copy construction to initialize object
pair<int, double> p3；
p3 = p1;
```

## 三、pair对象的操作

访问两个元素操作可以通过first和sencond访问：

```cpp
pair<int ,double> p1;
p1.first = 1;
p1.second = 2.5;
cout<<p1.first<<' '<<p1.second<<endl;
//输出结果：1 2.5

string firstBook;
if(author.first=="James" && author.second=="Joy")
firstBook="Stephen Hero";
```

## 四、生成新的pair对象

还可以利用make_pair创建新的pair对象：

```cpp
pair<int, double> p1;
p1 = make_pair(1, 1.2);
cout << p1.first << p1.second << endl;
//output: 1 1.2

int a = 8;
string m = "James";
pair<int, string> newone;
newone = make_pair(a, m);
cout << newone.first << newone.second << endl;
//output: 8 James
```

五、通过tie获取pair元素值

在某些清况函数会以pair对象作为返回值时，可以直接通过std::tie进行接收。比如：

```cpp
std::pair<std::string, int> getPreson() {
    return std::make_pair("Sven", 25);
}

int main(int argc, char **argv) {
    std::string name;
    int ages;
    std::tie(name, ages) = getPreson();
    std::cout << "name: " << name << ", ages: " << ages << std::endl;
    return 0;
}
```
