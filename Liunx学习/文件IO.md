# 文件IO

---

在Linux中万物都为文件，普通文件，设备，socket，标准输入输出等等

常用接口：

---

|  Method   |            Parameters            |               Descriptions               | Return                                         |    H     |
| :-------: | :------------------------------: | :--------------------------------------: | ---------------------------------------------- | :------: |
|   open    |  (char* name,int flags,[mode])   |  打开文件，通过不同的flags有不同的效果   | int(文件描述符)                                | fcntl.h  |
|   read    | (int fd, void * buf, size_t len) |     通过文件描述符，读取内容到buf中      | ssize_t(写入buf字节数),0代表 EOF, -1代表 ERROR | unistd.h |
|   write   | (int fd, void * buf, size_t len) | 无法保证调用后立马存在于文件中（写缓存） | ssize_t(写入buf字节数), -1代表 ERROR           | unistd.h |
|   fsync   |             (int fd)             |      直接IO，至少两个IO，性能消耗高      | 成功0，失败-1                                  | unisd.h  |
| fdatasync |             (int fd)             |           直接IO，不更新元数据           | 成功0，失败-1                                  | unisd.h  |
|   sync    |               void               |       对磁盘上的所有缓冲区进行同步       | void                                           |          |

### 

---

参数解析：

1. **open**

```
1. 常用flags
	O_APPEND,文件以追加模式打开，每次写操作之前都会指向文件末尾
	O_ASYNC,当文件可读或可写时，会生成信号默认为SIGIO，不适用普通文件
	O_CLOEXEC,执行新进程会关闭文件,可以避免竞争,和调用fctnl()设置标志位效果一直
	O_CREAT,文件不存在时新建文件
	O_DIRECT,直接用与IO
	O_EXCL,只能和O_CREAT一起使用，文件已经存在时调用失败，可以避免创建竞争
	O_LARGEFILE,可以支持2G以上大文件
	O_NOATIME,不打开修改记录时间戳，避免大量IO
	O_NONBLOCK，文件以非阻塞模式打开，只适合FIFO
	O_TRUNC，普通文件长度截为0
2. MODE，只有新建文件的时候有用，分配文件权限
	直接写数字
	S_IRUSR，文件所有者可读
	......
```

2. **read**

```
read的返回值情况多种多样
0 EOF：
	1.在阻塞模式下（socket）表示没有数据可读，等待新的数据
	2.在普通文件中，代表到了文件结尾
-1 error:
	1.error == EINTR，取任何字节之前接收到信号，可以重新调用
	2.error == EAGAIN , 这表示由于当前没有数据可用，读操作会阻塞，请求应该稍后再重新执行。这种情况只在非阻塞模式下发生。
	3.error == 其他 ,一些其他严重的错误
len ：
	1.与预期一样
小于len :
	1.读取中出错
	2.读取中中断
	3.数据长度小于len
```

 2.1 读入所有字节代码

```c
ssize_t ret; //ssize_t 为有符号的size_t ,在32系统相当于int 和 unsigned int
if (len > SSIZE_MAX)
    len = SSIZE_MAX; //当len大于SSIZE_MAX,read的行为没有定义
while(len != 0 && (ret = read(fd,buf,len)) != 0){
    if (ret == -1){
        if (errno == EINTR) //防止部分读
            continue;
        perror("read");
        break;
    }
    len -= ret;
    buf += ret;
}
```

3.  **write**

普通文件预防部分写方法

```c
unsigned Long word =1720;
size_t count;
ssize_t nr;
count = sizeof (word);
nr = write (fd,&word,count);
if(nr==-1)
	/*error，check errno*/
else if (nr != count)
    /* possible error,but 'errno' not set */
```

socket预防部分写方法

```c
ssize_t ret; //ssize_t 为有符号的size_t ,在32系统相当于int 和 unsigned int
if (len > SSIZE_MAX)
    len = SSIZE_MAX; //当len大于SSIZE_MAX,read的行为没有定义
while(len != 0 && (ret = write(fd,buf,len)) != 0){
    if (ret == -1){
        if (errno == EINTR) //防止部分读
            continue;
        perror("write");
        break;
    }
    len -= ret;
    buf += ret;
}
```



###### Refernece

---

《Linux应用编程第二版》

