<!--
 * @Author: 翁龙傲 1404813015@qq.com
 * @Date: 2023-07-09 18:23:52
 * @LastEditors: 翁龙傲 1404813015@qq.com
 * @LastEditTime: 2023-12-05 16:15:15
 * @FilePath: /mkdocs-knowledge-storage/docs/markdown/operation_utils/conda操作.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

# conda等的操作

## conda操作

* `conda --version`  查看安装的conda的版本
* `conda env list`  查看已经安装的环境列表
* `conda create -n leoweng_test python==3.9` 创建环境
* `conda activate leoweng_test` 激活环境
* `conda remove -n leoweng1.0 --all` 删除环境
* `conda remove -h  pandas`   删除包
* `conda create -n leoweng_test_1 --clone leoweng_test` 将已有环境复制一份，来创建新的环境
* `conda env export > /Users/wenglongao/Downloads/leoweng_test.yaml` 将环境导出为yaml文件
* `conda env create -f /Users/wenglongao/prep/code/platform-engineering/psaconda/pm_1.6.yaml`  用yaml文件创建环境
* `conda install -p /Users/wenglongao/miniforge3/envs/lgbm package_name` 在miniforge3创建的环境中安装package
* `/Users/wenglongao/miniforge3/bin/conda init zsh` 启动miniforge3安装的base
* `/Users/wenglongao/anaconda3/bin/conda init zsh` 启动anaconda安装的base，两者的关键都在于看conda的Unix文件在哪里，然后初始化[anaconda与miniforge3的base切换_miniforge3和anaconda-CSDN博客](https://blog.csdn.net/lc_dreams/article/details/122119961)注意！这一步需要整行命令一起执行，执行完成后重启终端，不然无法切换。

## pip操作

* `pip list`  查看当前环境下已安装的包
* `pip install package`  安装package，版本号为最新发布的
* `pip install pandas==2.0.3`  指定版本号安装package
* `pip install --upgrade pandas`  更新package到最新发布的版本号
* `pip install --upgrade pip`  更新pip自身
* `pip install --upgrade pandas==2.0.1`  将已经安装的package更新到指定版本号
* `pip uninstall`  pandas 卸载包
* `pip show --files pandas`  查看包内详细的文件
* `pip show pandas`  查看包路径等
* `pip --help`  获取命令帮助
* `pip list --help`
* `pip show --help`  根据具体命令获得帮助，可以得到pip show 之后的具体操作
* `pip install <package-name> -i https://pypi.tuna.tsinghua.edu.cn/simple` 临时设置清华镜像源
* `pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple` 永久设置清华镜像源
* `pip config unset global.index-url` 将pip切换为默认源
* `pip config list` 查看pip的安装源

## 其它一些操作

* `python -m ipykernel install --user --name leoweng_test --display-name "Python (leoweng_test)"`  将新环境添加到jupyter notebook的kernel，注意如果出现dquote说明引号输入成中文的了，要用英文引号””。添加新环境后可能需要重启vscode才能生效。
* `jupyter kernelspec list`查看jupyter notebook中已经添加的kernel
* `jupyter kernelspec remove leoweng1.2`删除指定的kernel，注意有可能需要先激活对应环境，再执行，否则有可能无法删除。
* ctrl + c  终止zsh命令窗口

### &emsp;&emsp;总结一下，很多操作的结构为 pip/conda(表示运用的管理器) 操作名称 --指定操作具体参数(可能可以省略），即空格 加上 -- 的结构

&emsp;&emsp;如果在本地导出后想再次create new environment，因为本地已经存在导出的环境了，会报错：CondaValueError: prefix already exists: /Users/wenglongao/anaconda3/envs/leoweng_test，则我们需要编辑yaml文件，将name字段的value修改为新的环境名称，然后可通过yaml文件创建新环境。
