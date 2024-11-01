# MacOS操作
记录一些OS常用的快捷操作

* `shift + cmd + 。` 显示访达隐藏文件
* `mkdir “path”`  在当前路径下新建路径
* `cd “path”`  前往路径
* `rm test.txt`   在当前路径下删除文件
* `pwd`  		查看当前路径
* `cat test.txt`  查看当前路径下的指定文件内容
* `chsh -s /bin/zsh` 将终端中使用zsh命令，重启后生效
* `chsh -s /bin/bash` 将终端中使用bash命令，重启后生效
* `alias | grep python` 检查是否为python设置别名，如果设置了别名，那么在终端运行python命令，就会自动调用别名
* `unalias python` 移除python的别名
* `source ~/.zshrc` 重新加载zsh配置文件。.zshrc


MacOS提示文件损坏
* `sudo spctl –master-disable`，输入密码回车，然后去设置中打开任意来源
* `sudo xattr -cr 拖入要打开的app`
然后去设置中点击仍要打开即可
[参考文章](https://blog.csdn.net/2301_78028487/article/details/130550961)
[参考文章](https://www.onlinedown.net/article/10020830.htm)

# Vim相关操作

* :q! 强制退出vim
* :wq! 

