
Ubuntu 14.04 安装 GCC 4.8.x, 4.9.x, 5.5 和 6.4 并随意切换
============================================================

## 1. 添加 PPA 源 ##

在 `toolchain/test` 下已经有打包好的 `gcc` ，版本有 `4.x`、`5.0`、`6.0` 等，用这个 `PPA` 升级 `gcc` 就可以啦！

首先添加 `ppa` 到更新源，并更新 `apt-get` ：

```shell
# 安装 add-apt-repository 组件
$ sudo apt-get install -y software-properties-common

# 添加 ppa 源
$ sudo add-apt-repository ppa:ubuntu-toolchain-r/test

# 更新 apt 源
$ sudo apt-get update
```

其中第二句执行的时候，如果你已经安装过 `add-apt-repository` 了的话，按回车确认，继续即可。

如果出现下面的错误信息或其他错误提示，则说明 `add-apt-repository` 没有安装或无法正常工作：

```shell
sudo: add-apt-repository: command not found
```

注意：在添加了 `ppa` 源以后，一定要记得执行 `sudo apt-get update` 命令，才会让添加的 `ppa` 生效。

## 2. 安装 gcc 各个版本 ##

`Ubuntu 14.04` 系统更新源默认安装的版本是 `gcc-4.8`，但现在都什么年代了，可以先安装默认的版本，接着再安装 `gcc-4.9`、`gcc-5` 之类的！

```shell
$ sudo apt-get upgrade   # 这句可以不执行

$ sudo apt-get install gcc-4.8 g++-4.8
$ sudo apt-get install gcc-4.9 g++-4.9
$ sudo apt-get install gcc-5 g++-5
$ sudo apt-get install gcc-6 g++-6
```

（注意：`gcc-4.8` 安装的版本是 `4.8.5`，比 `Ubuntu 14.04` 系统默认安装的版本 `4.8.4` 略高。 `gcc-5` 目前已经更新到了 `5.5.0`，且没有 `5.1`、`5.2` 或 `5.3` 之类的选择，`gcc-6` 目前则已经更新到了 `6.4.0` 版本。最后验证日期：`2018` 年 `7` 月 `19` 日。）

现在可以考虑刷新一下设置，否则，使用 `locate` 等命令，是找不到新版本文件所在目录的：

```shell
$ sudo updatedb && sudo ldconfig

$ locate gcc
```

（注意：此步不是必须的，可以跳过）

你会发现 `gcc -v` 显示出来的版本还是你原来装的 `gcc` 的版本，因此需要更新一下软链接，命令如下。

## 3. 设置 gcc 的链接，便于切换 ##

(下面是配置快速切换的命令，可保留原来的 `4.8.x` 版本。)

### 3.1. 单命令行的版本 ###

（推荐使用！）

`gcc 4.8.x`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 48 --slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-4.8 --slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-4.8 --slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-4.8

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 48
```

`gcc 4.9.x`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 49 --slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-4.9 --slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-4.9 --slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-4.9

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 49
```

`gcc 5.5.0`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 55 --slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-5 --slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-5 --slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-5

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 55
```

`gcc 6.4.0`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 64 --slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-6 --slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-6 --slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-6

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 64
```

### 3.2. 多命令行的版本 ###

（跟上面一样的，只是加了换行符 "\\"）

`gcc 4.8.x`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 48 \
--slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-4.8 \
--slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-4.8 \
--slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-4.8

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 48
```

`gcc 4.9.x`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 49 \
--slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-4.9 \
--slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-4.9 \
--slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-4.9

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 49
```

`gcc 5.5.0`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 55 \
--slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-5 \
--slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-5 \
--slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-5

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 55
```

`gcc 6.4.0`：

```shell
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 64 \
--slave /usr/bin/gcc-ar gcc-ar /usr/bin/gcc-ar-6 \
--slave /usr/bin/gcc-nm gcc-nm /usr/bin/gcc-nm-6 \
--slave /usr/bin/gcc-ranlib gcc-ranlib /usr/bin/gcc-ranlib-6

$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 64
```

## 4. 快速切换 gcc 版本 ##

### 4.1. 切换 `gcc` 版本的命令 ###

```shell
$ sudo update-alternatives --config gcc
```

有 4 个候选项可用于替换 `gcc` （默认路径 `/usr/bin/gcc`），如下所示：

```shell
  选择       路径            优先级  状态
------------------------------------------------------------
* 0            /usr/bin/gcc-4.9   49        自动模式
  1            /usr/bin/gcc-4.8   48        手动模式
  2            /usr/bin/gcc-4.9   49        手动模式
  3            /usr/bin/gcc-5     55        手动模式
  4            /usr/bin/gcc-6     64        手动模式
```

### 4.2. 切换 `g++` 版本的命令 ###

```shell
$ sudo update-alternatives --config g++
```

有 4 个候选项可用于替换 `g++` （默认路径 `/usr/bin/g++`），如下所示：

```shell
  选择       路径            优先级  状态
------------------------------------------------------------
* 0            /usr/bin/g++-4.9   49        自动模式
  1            /usr/bin/g++-4.8   48        手动模式
  2            /usr/bin/g++-4.9   49        手动模式
  3            /usr/bin/g++-5     55        手动模式
  4            /usr/bin/g++-6     64        手动模式
```

## 5. 参考文章 ##

----------------------------------------------------------------

[http://www.cnblogs.com/BlackStorm/p/5183490.html](http://www.cnblogs.com/BlackStorm/p/5183490.html)

[http://blog.sina.com.cn/s/blog_54dd80920102vvt6.html](http://www.cnblogs.com/BlackStorm/p/5183490.html)

----------------------------------------------------------------

（最后更新日期：`2018` 年 `7` 月 `19` 日）

<.end.>
