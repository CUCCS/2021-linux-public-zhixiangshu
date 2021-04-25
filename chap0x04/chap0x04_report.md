# 实验四

## 实验目的

掌握shell基本脚本编程

## 实验环境

- Ubuntu 20.04 server 64bit
- bash:   version 5.0.17(1)-release (x86_64-pc-linux-gnu)
- imagemagick:  6.9.10-23 Q16 x86_64 20190101 https://imagemagick.org

## 实验内容

- 线上课操作

  - 跟着老师的b站视频，创建文本文件shell-example。

  - 在个人`github`账号下创建一个小仓库shell-examples

    ![创建shell-examples仓库](chap0x04_img/创建shell-examples仓库.jpg)

  - 创建`.sh`文件，编写并运行。

  - 创建`.travis.yml`文件和`test.sh`

  - 将文件上传到`travis`环境中运行

    ![课上操作内容](chap0x04_img/课上操作内容.jpg)

- 任务一：用bash编写一个图片批处理脚本，实现以下功能：

  - [x] 支持命令行参数方式使用不同功能

  - [x] 支持对指定目录下所有支持格式的图片文件进行批处理

    支持以下常见图片批处理功能的单独使用或组合使用：

  - [x] 支持对`jpeg`格式图片进行图片质量压缩

  - [x] 支持对`jpeg/png/svg`格式图片在保持原始宽高比的前提下压缩分辨率

  - [x] 支持对图片批量添加自定义文本水印

  - [x] 支持批量重命名（统一添加文件名前缀或后缀，不影响原始文件扩展名）

  - [x] 支持将`png/svg`图片统一转换为`jpg`格式图片

- 任务二：用bash编写一个文本批处理脚本，对以下附件分别进行批量处理完成相应的数据统计任务：

  **2014世界杯运动员数据**

  - [x] 统计不同年龄区间范围（20岁以下、[20-30]、30岁以上）的球员**数量**、**百分比**
  - [x] 统计不同场上位置的球员**数量**、**百分比**
  - [x] 名字最长的球员是谁？名字最短的球员是谁？
  - [x] 年龄最大的球员是谁？年龄最小的球员是谁？

- 任务二：用bash编写一个文本批处理脚本，对以下附件分别进行批量处理完成相应的数据统计任务：

  **Web服务器访问日志**

  - [x] 统计访问来源主机TOP 100和分别对应出现的总次数
  - [x] 统计访问来源主机TOP 100 IP和分别对应出现的总次数
  - [x] 统计最频繁被访问的URL TOP 100
  - [x] 统计不同响应状态码的出现次数和对应百分比
  - [x] 分别统计不同4XX状态码对应的TOP 10 URL和对应出现的总次数
  - [x] 给定URL输出TOP 100访问来源主机

## 实验步骤

1. 打开Virtual Box登录账号
2. 使用vs code && git bash 远程登录
3. 下载实验所需数据
   - 2014年运动员世界杯数据
   - Web服务器访问日志
4. 编写代码
5. 测试代码并将结果截图
6. 编写实验报告并提交

## 实验结果

- 任务一

  ```
   help帮助文档
   bash img-batch-processing.sh -h
  ```

  

  ```
  支持对`jpeg`格式图片进行图片质量压缩
   bash img-batch-processing.sh -d img-original/ -q 50%
  ```

  图片路径：*chap0x04_img/img-processed/jpeg质量压缩后*

  

  ```
  支持对`jpeg/png/svg`格式图片在保持原始宽高比的前提下压缩分辨率
  bash img-batch-processing.sh -d img-original/ -r 90
  ```

  图片路径：*chap0x04_img/img-processed/压缩分辨率*

  

  ```
  支持对图片批量添加自定义文本水印
  bash img-batch-processing.sh -d img-original/ -w "www.cnblogs.com"
  ```

  图片路径：*chap0x04_img/img-processed/批量添加水印*

  

  ```
  支持批量重命名（统一添加文件名前缀或后缀，不影响原始文件扩展名）
  bash img-batch-processing.sh -d img-original/ -p "Pre"
  bash img-batch-processing.sh -d img-original/ -s "Tail"
  ```

  图片路径：*chap0x04_img/img-processed/添加前缀后缀*

  

```
支持将`png/svg`图片统一转换为`jpg`格式图片
bash img-batch-processing.sh -d img-original/ -c 100
```

图片路径：*chap0x04_img/img-processed/png变jpg*

- 任务二 1/2

  ```
  help帮助文档
  bash world-cup-players.sh -h
  ```

  ![players帮助文档](chap0x04_img/players帮助文档.jpg)

  

  

  ```
  统计不同年龄区间范围（20岁以下、[20-30]、30岁以上）的球员**数量**、**百分比**
  bash world-cup-players.sh -ar
  ```

  ![年龄区间](chap0x04_img/年龄区间.jpg)

​       

```
统计不同场上位置的球员**数量**、**百分比**
bash world-cup-players.sh -p
```

![球员数量](chap0x04_img/球员数量.jpg)



```
 名字最长的球员是谁？名字最短的球员是谁？
 bash world-cup-players.sh -n
```

![名字长短](chap0x04_img/名字长短.jpg)



```
年龄最大的球员是谁？年龄最小的球员是谁？
bash world-cup-players.sh -ac
```

![最老最小球员](chap0x04_img/最老最小球员.jpg)



- 任务二  2/2

```
 help帮助文档
 bash web-blog.sh -h
```

![日志帮助文档](chap0x04_img/日志帮助文档.jpg)



```
统计访问来源主机TOP 100和分别对应出现的总次数
bash web-blog.sh -o 100
```

 结果：chap0x04/web-blog-data/HostTop.log



```
 统计访问来源主机TOP 100 IP和分别对应出现的总次数
 bash web-blog.sh -i 100
```

结果：chap0x04/web-blog-data/IpTop.log



```
统计最频繁被访问的URL TOP 100
bash web-blog.sh -u 100
```

结果：chap0x04/web-blog-data/UrlTop.log



```
 统计不同响应状态码的出现次数和对应百分比
 bash web-blog.sh -r
```

结果：chap0x04/web-blog-data/Response.log



```
 分别统计不同4XX状态码对应的TOP 10 URL和对应出现的总次数
 bash web-blog.sh -u4 100
```

结果：chap0x04/web-blog-data/Response4xxTop.log



```
 给定URL输出TOP 100访问来源主机,例给定URL"ksc.html"
 bash web-blog.sh -uh  "ksc.html" 100
```

结果：chap0x04/web-blog-data/SpecifiedURLHost.log

## 问题&&解决方法

1. 登录`travis-ci.com/account/repositories`,看不到shell-examples仓库

   解决方法：点击`activate`绿色按钮，连接上`github`即可

   ![找不到shell-examples仓库](chap0x04_img/找不到shell-examples仓库.jpg)

2. `travis`构建出错

   ![travis构建出错](chap0x04_img/travis构建出错.jpg)

   错因：所有编辑的文件都放在master中

   解决方法：创建一个分支，将实验操作的`.sh`文件上传到此分支；`.travis.yml`和`test.sh`放在master主干

3. 怎样在`.travis-ci.yml` 里 ls 查看脚本所在目录有哪些文件？

   `travis`和本地是两个不同的环境。在`test.sh`中添加 ls语句，将修改后的`test.sh`重新push到`travis`中执行。（针对课上实验的错误）

4. 代码的**问题**一看**代码本身**，二看代码里的打印语句输出**调试信息**。

5. 将图片传进虚拟机，直接从vs code拖进去就可以了！不用大费周章创建共享文件夹

6. 图片无法拖进vs code

   错因：创建的是文件，而不是文件夹，所以拖不进

   ![区分文件&文件夹](chap0x04_img/区分文件&文件夹.jpg)

7. 将处理后的文件从虚拟机中复制到主机时，报错`ssh: Could not resolve hostname c: Temporary failure in name resolution
   lost connection`

   - 解决方法一：

   ```
   vim /ect/profile
   ```

   编辑文件，在最后加上

   ```
   export JAVA_HOME=/usr/java/jdk
   
   export HADOOP_HOME=/itcast/hadoop-2.6.4                                   
   export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
   export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
   
   export PATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin 
   ```

   重新执行该文件 ` source /etc/profile`  → 失败！

   - 解决方法二

     直接在vs code里面下载！！！  →成功了！！

   

8. 在编辑etc/profile文件时，无法保存 报错`E45: 'readonly' option is set (add ! to override)`

   解决方法

   - 强行保存`:wq!`  → 失败
   - `sudo vim /etc/profile`  编辑后再使用命令 `:Wq!`保存退出  →成功！ 

   ​                 

9. 将球员和webblog数据拖进虚拟机时，在chap0x04文件夹中创建一个新的文件夹data存数据，代码运行出错

   ```
   awk: fatal: cannot open file `worldcupplayerinfo.tsv' for reading (No such file or directory)
   (standard_in) 2: syntax error
   (standard_in) 2: syntax error
   (standard_in) 2: syntax error
   ```

   解决方法：直接将数据放在chap0x04文件夹中，无需单独创建文件夹，即可运行成功

## 参考资料

- 2014年运动员世界杯数据
- Web服务器访问日志
- https://github.com/CUCCS/linux-2020-cuc-Lynn
- [问题7解决方法](https://www.cnblogs.com/xiaohua92/p/5469772.html)
- [CSDN网站](https://www.csdn.net/)



