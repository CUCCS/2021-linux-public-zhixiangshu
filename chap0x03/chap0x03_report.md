# 实验三

## 实验目的

- 熟悉并掌握Systemd的基本操作
- 学会逻辑分卷管理

## 实验环境

Virtual Box

## 实验内容

- 使用git-bash配置SSH免密登录
- 进行逻辑分卷管理

- 跟着日志进行操作：
  - [Systemd 入门教程：命令篇 by 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)
  - [Systemd 入门教程：实战篇 by 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html)

## 实验步骤

如录像所示；

## 录像URL

- 命令篇_系统管理 [https://asciinema.org/a/404589](https://asciinema.org/a/404589)
- 命令篇_Unit [https://asciinema.org/a/404593](https://asciinema.org/a/404593)
- 命令篇_Unit的配置文件 [https://asciinema.org/a/404596](https://asciinema.org/a/404596)
- 命令篇_Target [https://asciinema.org/a/404599](https://asciinema.org/a/404599)
- 命令篇_日志管理 [https://asciinema.org/a/404602](https://asciinema.org/a/404602)
- 实战篇：开机启动_启动、停止服务 [https://asciinema.org/a/404606](https://asciinema.org/a/404606)
- 实战篇：读懂配置..~修改配置.. [https://asciinema.org/a/404612](https://asciinema.org/a/404612)

## 自查清单

- 如何添加一个用户并使其具备sudo执行程序的权限？

  - 添加用户：`sudo user add 用户名`

  - 添加sudo权限：`vim /etc/sudoers`进入编辑模式

    ​                           "root ALL=(ALL) ALL"在下面添加`用户名 ALL=(ALL) ALL`

- 如何将一个用户添加到一个用户组？

  - `usermod -a -G group_name user_name` (用户添加到新的组后，不会离开原来的组)
  - ``usermod  -G group_name user_name`` （用户会离开原来的组）

- 如何查看当前系统的分区表和文件系统详细信息？

  - 查看分区表 
    - `lsblk`
    -    `sudo fdisk -l` 
    - `fdisk -l/dev/sda`
    - `sudo parted/dev/sda`
    - `sudo parted -l`
  - 查看文件系统详细信息 `[root@localhost ~]# stat [选项]文件名或目录名`

- 如何实现开机自动挂载Virtualbox的共享目录分区？

  - 在VirtualBox的菜单里选择”设备” -> “安装增强功能”。

  - 进入命令终端输入`cd/media/username/VBOXADDITIONS_5.1.18_114002
    sudo ./VBoxLinuxAdditions.run`

  - 重启完成后点击”设备” -> 共享文档夹 菜单，添加一个共享文档夹，尽量使用有**辨识度**的**英文**名

  - 重新进入虚拟Ubuntu，在命令行终端下输入：

    `sudo mkdir /mnt/shared`

    `sudo mount -t vboxsf 共享文件夹名 /mnt/shared`

  - 在/etc/fstab中添加如下一行：

    `shareforlinux /mnt/shared vboxsf rw,gid=username,uid=username,auto 0 0`

- 基于LVM（逻辑分卷管理）的分区如何实现动态扩容和缩减容量？ 

  - 动态扩容

    - 查看磁盘信息 `fdisk -l`

    - 格式化磁盘 `parted /dev/xvdg`

    - 使用`print`命令查看磁盘信息，提示`Error: /dev/xvdg: unrecognised disk label`；

    - 需使用`mklabel gpt`命令，对磁盘创建分区表；

    - 使用`mkpart primary 0 100%`命令，出现警告输入`Ignore`忽略；

    - 使用`print`即可查看新的分区信息，使用`quit`退出

    - 查看磁盘信息 `fdisk -l /dev/xvdg` （新磁盘分区为/dev/xvdg1）

    - 使用命令创建物理卷 `pvcreate /dev/xvdg1`

    - 物理卷创建成功，使用`pvdisplay`可查看物理卷信息

    - 将新增的xvdg1加入到卷组license（需要扩容的卷组）：

      `vgextend license /dev/xvdg1`

    - 将卷组中新加入的磁盘空间容量扩展到逻辑卷中

      使用`lvextend -l +100%FREE /dev/license/license-data`将余空间全部扩容到l/dev/license/license-data逻辑卷中

    - 刷新文件系统使扩容生效

      `resize2fs /dev/license/license-data`

  - 缩减容量

    - 逻辑卷回缩不能在线进行，所以先卸载已经挂载的逻辑卷并检测文件系统

    - 使用umount卸载 

      `umount /dev/app/app_lv`

    - 使用e2fsck检测文件系统 

      `e2fsck -f /dev/app/app_lv`

    - 使用resize2f缩小文件系统为5G  

      `resize2f /dev/app/app_lv 5G`

    - 使用lvreduce 缩小逻辑卷，上面要缩小到5G，原先是6G，所以这里减少1G

       `lvreduce -L -1G /dev/app/app_lv 5G`

    - 查看缩小后的逻辑卷 `lvdisplay`

    - 挂载逻辑卷

       `mount /dev/app/app_lv /app/`

- 如何通过systemd设置实现在网络连通时运行一个指定脚本，在网络断开时运行另一个脚本？

  

  修改systemd-network中的service

  ExecStartPost=网络联通时运行的指定脚本

  ExecStopPost=网络断开时运行的另一个脚本

  

- 如何通过systemd设置实现一个脚本在任何情况下被杀死之后会立即重新启动？实现***杀不死\***？

​       在[service]区块中设置  

​        `Restart=always`

​        重载配置文件

​        `sudo systemctl darmon-reload`





