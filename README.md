# About
Qt5 binding of [CEF](https://bitbucket.org/chromiumembedded/cef)

# 特别注释
fork这个是为了解决在某些linux版本下(比如debian)安装网易云音乐出现的依赖错误
eg：
软件包依赖关系不满足
libqcef1无法安装之类的

或者libqcef已过期或者被其他软件替代之类的，
如果你尝试安装libqcef会提示:
> Package libqcef is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source


`sudo apt-get -f install`
是不行的，因为修复不了，它只会把网易云也卸载了。
毕竟确实是软件源里没有这个包即使换了testing的源也是找不到，
这个仓库就是解决这个问题，clone下来编译安装上qcef

下面步骤:
1. 安装必要的包:
```
sudo apt install devscripts equivs git
```

2. 克隆此仓库并进入文件夹:
```
git clone https://github.com/hoyho/qcef-for-debian-netease-music.git && cd qcef
```


3. 确保没有以前的建立的虚拟包生成并安装一个依赖于所需包的虚拟包:
```
$ rm -f qcef-build-deps_*_*.deb
$ mk-build-deps -s sudo -i
```

4. 建立一个完整的 libqcef1 Debian 软件包

`sudo dpkg-buildpackage -uc -us -b -j$(nproc)`

5. 安装并清理现场
```
$ sudo apt install $(pwd)/../libqcef1_*.deb
$ rm ../*qcef* 2> /dev/null
```

6.安装你的deb包
```
sudo dpkg -i neteasexxxxxxx.deb
```

7. enjoy!

# LICENSE
This project is released under GNU Lesser General Public License which
can be found in LICENSE file.
