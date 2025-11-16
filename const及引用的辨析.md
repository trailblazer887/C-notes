实例代码：
```C++
class DynamicString{
private:
    char* data;
    int length;
public:
    // 赋值运算符的重载示例
       |                                |       |
       V                                V       V
    (const) Dynamicstring& operator= (const)((const) Dynamicstring& other){
        if (this != &ohter){
            delete[] data;
            length = other.length;
            data = new char[length + 1];
            strcpy(data, other.data);
        }
        return *this;
    }
}
```
**第一个`const`**：返回一个**返回值的`const`视图**\
即返回值不一定是`const`类型的，但调用这个函数后返回的是一个不可更改(`const`)的视图,这个视图被赋值到其他变量去后，后续便不可更改。
**第二个`const`**：表明**函数不可改变类成员的值**(**普通函数不存在这一部分**，但**在Lambda函数中存在**，表示**无法改变按''值''捕获的变量的值**，对**按''引用''捕获的变量无影响**)\
即在此函数中`this.length = 10`是不合法的。
**第三个`const`**：代表这个接收的目标**在函数内是不可更改值的**(即这个参数在函数内是**只读**的，并**不是**代表要传入一个`const`的值)。\
\
**引用**：用于描述**类型**，表示**作为参数传入**或**作为返回值返回**时，使用**本身的地址**而**不去创造副本**(可用于修改，或避免内存开销)。
**引用**分为**左值引用(&)**和**右值引用(&&)**，左值引用**只能指向左值**，右值引用**只能指向右值**。右值引用可用于**移动语义**，在**函数传参**中使用右值引用(具体实现需要自己写)可以**减少深拷贝的花销，提升程序性能**([详细见知乎文章](https://zhuanlan.zhihu.com/p/335994370))