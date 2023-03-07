# 常用命令集合

## 1.删除命令

### rm命令

```shell
1.rm file //删除文件
2.rm -r directory //删除目录

```

## 2.复制命令

### cp

```shell
1.cp oldname newname //复制文件
2.cp -r old new //旧目录到新目录
```

## 3.文本命令

```
1.cat file //读取文本文件
2.head -n num file //读取文本前num行
3.tail -n num file //读取文本后num行
4.tail -f file //动态读取
5.tailf        //类似tail -f 不同的是没有变化不会访问磁盘，而且从头开始读，不是脚本
```

## 4.重命名

```shell
1.mv  //实际上是move
-b如果存在，则覆盖前会进行备份
-f如果存在，则直接覆盖
-i让用户选择是否覆盖

mv *.txt /coffee  //将后缀为txt的文件移动到/coffee里面
2.rename //批量修改文件夹

```

