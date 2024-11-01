# Linux常用操作

## 软件安装

- CentOS系统使用：
  - yum [install remove search] [-y] 软件名称
    - install 安装
    - remove 卸载
    - search 搜索
    - -y，自动确认
- Ubuntu系统使用
  - apt [install remove search] [-y] 软件名称
    - install 安装
    - remove 卸载
    - search 搜索  
    - -y，自动确认

> yum 和 apt 均需要root权限



## systemctl

功能：控制系统服务的启动关闭等

语法：`systemctl start | stop | restart | disable | enable | status 服务名`

- start，启动
- stop，停止
- status，查看状态
- disable，关闭开机自启
- enable，开启开机自启
- restart，重启
![img.png](images/img.png)


## 软链接
![img_1.png](images/img_1.png)
功能：创建文件、文件夹软链接（快捷方式）

语法：`ln -s 参数1 参数2`

- 参数1：被链接的
- 参数2：要链接去的地方（快捷方式的名称和存放位置）



## 日期

语法：`date [-d] [+格式化字符串]`

- -d 按照给定的字符串显示日期，一般用于日期计算

- 格式化字符串：通过特定的字符串标记，来控制显示的日期格式
  - %Y   年%y   年份后两位数字 (00..99)
  - %m   月份 (01..12)
  - %d   日 (01..31)
  - %H   小时 (00..23)
  - %M   分钟 (00..59)
  - %S   秒 (00..60)
  - %s   自 1970-01-01 00:00:00 UTC 到现在的秒数



示例：

- 按照2022-01-01的格式显示日期

  ![image-20221027220514640](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220514.png)

- 按照2022-01-01 10:00:00的格式显示日期

  ![image-20221027220525625](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220525.png)

- -d选项日期计算

  ![image-20221027220429831](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220429.png)

  - 支持的时间标记为：

    ![image-20221027220449312](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220449.png)





## 时区

修改时区为中国时区

![image-20221027220554654](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220554.png)



## ntp

功能：同步时间

安装：`yum install -y ntp`

启动管理：`systemctl start | stop | restart | status | disable | enable ntpd`



通过阿里云的时间校准服务器手动校准时间：`ntpdate -u ntp.aliyun.com`



## ip地址
![img_2.png](images/img_2.png)

格式：a.b.c.d

- abcd为0~255的数字



特殊IP：

- 127.0.0.1，表示本机
- 0.0.0.0
  - 可以表示本机
  - 也可以表示任意IP（看使用场景），放行ip设置为0.0.0.0，表示允许任意ip



查看ip：`ifconfig`



## 主机名

功能：Linux系统的名称

查看：`hostname`

设置：`hostnamectl set-hostname 主机名`

百度网站的ip地址可以被解析为www.baidu.com这个域名
![img_3.png](images/img_3.png)  
![img_4.png](images/img_4.png)
## 配置Vmware固定IP
![img_5.png](images/img_5.png)
1. 修改Vmware网络，参阅PPT，图太多

2. 设置Linux内部固定IP

   修改文件：`/etc/sysconfig/network-scripts/ifcfg-ens33`

   示例文件内容：

   ```shell
   TYPE="Ethernet"
   PROXY_METHOD="none"
   BROWSER_ONLY="no"
   BOOTPROTO="static"			# 改为static，固定IP
   DEFROUTE="yes"
   IPV4_FAILURE_FATAL="no"
   IPV6INIT="yes"
   IPV6_AUTOCONF="yes"
   IPV6_DEFROUTE="yes"
   IPV6_FAILURE_FATAL="no"
   IPV6_ADDR_GEN_MODE="stable-privacy"
   NAME="ens33"
   UUID="1b0011cb-0d2e-4eaa-8a11-af7d50ebc876"
   DEVICE="ens33"
   ONBOOT="yes"
   IPADDR="192.168.88.131"		# IP地址，自己设置，要匹配网络范围
   NETMASK="255.255.255.0"		# 子网掩码，固定写法255.255.255.0
   GATEWAY="192.168.88.2"		# 网关，要和VMware中配置的一致
   DNS1="192.168.88.2"			# DNS1服务器，和网关一致即可
   ```



## ps命令

功能：查看进程信息

语法：`ps -ef`，查看全部进程信息，可以搭配grep做过滤：`ps -ef | grep xxx`
![img_9.png](images/img_9.png)

  
## kill命令

![image-20221027221303037](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221303.png)



## nmap命令

![image-20221027221241123](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221241.png)



## netstat命令

功能：查看端口占用

用法：`netstat -anp | grep xxx`  xxx代表要查看的端口
 
![img_6.png](images/img_6.png)
![img_7.png](images/img_7.png)

nmap命令也可以查看端口, e.g. nmap 127.0.0.1 查看本机占用端口
![img_8.png](images/img_8.png)
## ping命令

测试网络是否联通

语法：`ping [-c num] 参数`

![image-20221027221129782](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221129.png)



## wget命令

![image-20221027221148964](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221149.png)

## curl命令

![image-20221027221201079](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221201.png)

![image-20221027221210518](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221210.png)



## top命令

功能：查看主机运行状态

语法：`top`，查看基础信息
![img_10.png](images/img_10.png)
负载为1可以理解为有一颗cpu很繁忙
![img_11.png](images/img_11.png)


可用选项：

![image-20221027221340729](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221340.png)


交互式模式中，可用快捷键：

![image-20221027221354137](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221354.png)



## df命令

查看磁盘占用

![image-20221027221413787](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221413.png)



## iostat命令

查看CPU、磁盘的相关信息

![image-20221027221439990](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221440.png)

![image-20221027221514237](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221514.png)



## sar命令

查看网络统计

![image-20221027221545822](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221545.png)



## 环境变量

![img_12.png](images/img_12.png)
![img_13.png](images/img_13.png)
![img_14.png](images/img_14.png)
- export 用于添加环境变量
- 临时设置：export 变量名=变量值
- 永久设置：
  - 针对用户，设置用户HOME目录内：`~/.bashrc`文件(bash) 或`~/.zshrc`文件(zsh)
  - 针对全局，设置`/etc/profile`
    * 在文件中添加 `export 变量名=变量值` 
    * 输入命令`source 修改的路径名称`让修改生效
- 查看环境变量: echo $env_var_name



### PATH变量
 - PATH是一个特殊且非常重要的环境变量。它定义了系统在执行命令时搜索可执行文件的目录列表。<br><br>

 - 可以将自定义路径加入PATH内，实现自定义命令在任意地方均可执行的效果。

* 如果export PATH="~./bin:$PATH"，那么在~./bin目录下的所有可执行文件，都可以在zsh终端运行时被系统查找到
![img_15.png](images/img_15.png)
- 例如，将python添加到可执行程序的搜索路径: export PATH="/Users/wenglongao/anaconda3/envs/torch/bin/python:$PATH"
![img_25.png](images/img_25.png)
- 注意两种export的写法的区别
## $符号

可以取出指定的环境变量的值

语法：`$变量名`

示例：

`echo $PATH`，输出PATH环境变量的值

`echo ${PATH}ABC`，输出PATH环境变量的值以及ABC

如果变量名和其它内容混淆在一起，可以使用${}

![img_16.png](images/img_16.png)




## 压缩解压

![img_19.png](images/img_19.png)
![img_20.png](images/img_20.png)

### 压缩

`tar -zcvf 压缩包 被压缩1 被压缩2 ... 被压缩N`
* .tar格式：tar -cvf，体积不会变小
* .tar.gz格式：tar -zcvf，体积变小明显
- -z表示使用gzip，可以不写
![img_21.png](images/img_21.png)


`zip [-r] 参数1 参数2 参数N`

![image-20221027221906247](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221906.png)


### 解压

`tar -zxvf 被解压的文件 -C 要解压去的地方`

- -z表示使用gzip，可以省略
- -C，可以省略，指定要解压去的地方，不写解压到当前目录

![img_22.png](images/img_22.png)

`unzip`
![img_23.png](images/img_23.png)

总结

![img_24.png](images/img_24.png)

## 上传、下载

* 通过final shell直接拖拽

![img_17.png](images/img_17.png)
* 通过rz、sz命令

![img_18.png](images/img_18.png)





`unzip [-d] 参数`

![image-20221027221939899](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221939.png)





## su命令

切换用户

语法：`su [-] [用户]`

![image-20221027222021619](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222021.png)



## sudo命令

![image-20221027222035337](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222035.png)



比如：

```shell
itheima ALL=(ALL)       NOPASSWD: ALL
```

在visudo内配置如上内容，可以让itheima用户，无需密码直接使用`sudo`



## chmod命令

修改文件、文件夹权限



语法：`chmod [-R] 权限 参数`

- 权限，要设置的权限，比如755，表示：`rwxr-xr-x`

  ![image-20221027222157276](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222157.png)

- 参数，被修改的文件、文件夹

- 选项-R，设置文件夹和其内部全部内容一样生效



## chown命令

修改文件、文件夹所属用户、组



语法：`chown [-R] [用户][:][用户组] 文件或文件夹`

![image-20221027222326192](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222326.png)



## 用户组管理

![image-20221027222354498](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222354.png)



## 用户管理

![image-20221027222407618](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222407.png)



## genenv命令

- `getenv group`，查看系统全部的用户组

  ![image-20221027222446514](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222446.png)

- `getenv passwd`，查看系统全部的用户

  ![image-20221027222512274](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222512.png)



## env命令

查看系统全部的环境变量

语法：`env`