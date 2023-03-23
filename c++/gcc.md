

## 1. gcc编译过程

gcc为GNU编译套件(GNU Compiler Colletion)

![image-20230322141250515](C:\Users\DoYou\AppData\Roaming\Typora\typora-user-images\image-20230322141250515.png)

## 2. gcc编译命令

```
0. -o
	指定生成目标文件
00. -O
	设定优化级别，123越大越高
1. -I
	指定头文件目录
2. -D
	指定宏，避免修改源代码
3. -g
	添加调试信息
4. -Wall
	更多的警告信息
5. -L
	包含库路径
6. -l
	指定库文件

```

## 3. 制作静态库

```
1. 命名要求
	linux:libxxx.a
	windows:libxxx.dll
2.顺序
	1.将各个.c或.cpp 打包成.o文件
	2.ar rcs libxxx.a xxx.o
examples:
	1.gcc -c *.c -I includepath
	2.ar rcs libxxx.a *.o
	3.gcc -o main.c -L libpath -l libxxx.a -I includePath
```

## 4. 制作动态库

```
动态库与静态库不同的是，程序在运行的时候才会链接动态库
1. 生成与位置无关的.o ， -fPIC
2. 打包.o文件 使用-shared
3. 将库与头文件一起发布
examples:
	1.gcc -fPIC -c *.c -I includepath
	2.gcc -shared -o *.o libxxx.so
	3.gcc -o main.c -I includepath -L libpath -l libxxx.so
```

---

## 5. 静态库与动态库比较

```
1.动态库
	优点：程序体积小，动态库变更时程序不需要重新编译
	缺点：路径设置错误会有链接不到库的风险，分件分布错乱，有可能被恶意替换共享库
2.静态库
	优点：程序集成一体，不需要额外发布库，没有找不到库的风险
	缺点：程序文件大，库文件更新时，程序需要重新编译
```



## 其它命令

```
1.ldd <filename>
		检查当前程序链接情况
```

