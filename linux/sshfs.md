# sshfs神器：将远程文件系统挂载到本地,直接编辑

sshfs，可以把ssh连接到的主机资源，映射到本机的文件系统当中，然后用户可以像操作本地文件一样操作，而实际的文件改动将通过ssh传输到远程主机当中。

## 安装
以下是在网上找的利用brew安装sshfs的过程。

    brew tap homebrew/fuse #可以使用brew search sshfs查找软件所在的库

 sshfs需要依赖fuse：

    brew cask install osxfuse

 安装sshfs

    brew install homebrew/fuse/sshfs

## 使用
### 挂载 
 :后面的dir是远端目录，可以留空，默认是用户home目录，mountpoint是本地挂载路径

    sshfs user@hostname:dir mountpoint

 在本地建立目录server，作为挂载点，dev是可以利用ssh免密登录的服务器
 执行以下命令成功挂载，server里面就展示出了远端用户目录下的文件

    sshfs dev: server

### 卸载

    umount server
 如果ssh连接未正常关闭，则挂载点会进入一种异常状态，在访问的时候会提示Input/output error，解决方案如下：

    ps aux | grep sshfs #先找到sshfs挂载进程的pid
    kill -9 pid #强制关闭进程
    sudo diskutil umount force mountpoint #强制卸载
 输出Unmount successful for mountpoint，表示卸载成功