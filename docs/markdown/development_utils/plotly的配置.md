# plotly的配置
1. plotly的配置可能会遇到ipywidgets安装后导致jupyter notebook server error
解决办法：<br>
* `conda install -c conda-forge widgetsnbextension`
* `jupyter nbextension enable --py widgetsnbextension`
* `jupyter nbextension enable --py --sys-prefix widgetsnbextension`

目前还没搞定