# 类型推导
类型推导都是编译器在编译阶段进行的，并不是运行时
### auto
可以通过等号右边的内容推断出变量的类型

1. auto使用必须立马初始化，要不然无法推导出类型（变量）
2. auto在一行定义多个变量时，各个变量的推导不能多个类型
3. auto不能定义数组，但是可以定义指针 
4. 不能作为函数参数 （函数）
5. auto不能用作类的非静态成员变量 （类）
6. auto不能推导模板参数 （模板）
7. auto在声明为普通变量时会忽略const，volatile；如果是引用和指针的话不会忽略（关键字）
```c++
auto i = 10; // i 是int型

class A{
    auto a = 1 ;//error,在类中不能用作非静态成员
    static auto b =1;//error,static无法这样初始化，与auto无关
    static const c =1;//success
}

//这样结合lambda使用auto，会简单很多,建议复杂类型使用auto
auto func = [&]{
    //
}


```
### decltype
相对于auto，decltype用于推导表达式的类型
* exp如果是表达式的话,decltype(exp)和exp类型一致 
* exp如果是函数的话，decltype(exp)和函数返回值类型一致
* exp如果是左值的话，decltype(exp)是exp类型的左值引用
```c++
decltype(i) b = 2;
//decltype高级用法
template<typename T ,typename U>
auto add(T t , U u) -> decltype(t + u){
    return t+u;
} //如果是c++14标准的话，可以只有auto就行



```
# 左值右值
