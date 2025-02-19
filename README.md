# gcc 6.5.0脚本安装

## 脚本说明

gcc_650.sh在姜峰等同学编写的gcc 6.5.0安装编译文档的基础上完成，由于时间仓促，仅支持6.5.0版本，需要其他版本的同学请自行修改脚本中相关版本内容，且仅支持在VGPU01-04上使用。

由于类脑集群共享存储，因此只需要在一台服务器上安装，无需在其他服务器重复安装

## 使用方法

由于安装编译时间较长，所以建议挂后台运行，建议使用tmux运行，命令如下:

```shell
bash gcc_650.sh [usr] [path]
```

其中`[usr]`和`[path]`分别填入用户名(如zhangsy)和指定的安装目录(如gcc_650)

例如
```
bash gcc_650.sh zhangsy gcc_650
```

## 校验

如果最终正确输出gcc版本号，即如下内容:

```shell
gcc (GCC) 6.5.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

说明安装成功，否则安装失败。
### 安装完成后请清理不必要的压缩文件.


## 补充说明（如果上述安装失败，可以看看是不是下面的原因）
1. 除去247是`home`，246、248、249都是`home1`，注意不要在错误的gpu上忘记修改路径
2. sh文件运行不了可以逐行运行然后按照报错补充
3. 针对 `make && make install` 时出现 `missing aclocal-1.14 -I m4 make: *** [aclocal.m4] 错误 127` 先执行 `autoreconf -ivf` 加载缺失文件后，再执行 `make`就可以了
4. 针对`warning: Clock skew detected. Your build may be incomplete`，可以不用管，在网上搜到的解决方案是`find . -type f | xargs -n 5 touch`但是没有效果依然报warning
5. 虽然不知道为什么，不到200M的gcc-6.5.0.tar.gz的解压过程的确很长，耐心等待，严重怀疑前几次安装失败就是sh文件中这个东西解压很快但是有损失
