# GDSFactory 环境配置教程

GDSFactory 环境配置的最大难点在于 KLayout 相关插件的安装，原因在于直接在 KLayout 软件上安装插件大概率会失败（安装插件需要访问国外的服务器，会经常出现访问失败的情况），为了解决这一问题，可以手动安装 KLayout 所需要的插件，下面将逐步介绍如何具体实现这一过程。

## 步骤一：安装 KLayout 软件

如果已经安装过 KLayout 软件，可以直接进行步骤二。

访问 KLayout 官网，访问网址为：[KLayout 官网安装包下载网址](https://www.klayout.de/build.html)

选择合适的安装包并下载，如下图 1 所示。

```{figure} _static/img/GDS_No1.png
:width: 100%
:align: center
:alt: 图 1 KLayout安装包下载界面

图 1 KLayout安装包下载界面
```

由于 KLayout 为国外软件，所以安装包下载过程可能非常缓慢，需要科学上网才能提高下载速度。这里直接给出 KLayout 的 Windows 64 位安装包，网盘链接为：[KLayout软件安装包网盘链接](https://pan.baidu.com/s/1yKoCYbP3UZ3t-hKLFG3nDw?pwd=KLay)

安装包下载完成后，按照正常软件安装的流程完成 KLayout 的安装即可。

## 步骤二：手动安装 KLayout 所需插件

### 1. 下载需要的插件

手动下载 KLayout 所需要的插件包，下载链接如下：

- metainfo-ports：[metainfo-ports-main](https://github.com/gdsfactory/metainfo-ports/archive/refs/heads/main.zip)
- klive：[klive-main](https://github.com/gdsfactory/klive/archive/refs/heads/main.zip)
- gdsfactory：[gdsfactory-main](https://github.com/gdsfactory/gdsfactory/archive/refs/heads/main.zip)

### 2. 创建 KLayout\salt 文件夹

KLayout 的 salt 文件夹用于管理软件插件包，如果之前没有安装过任何插件，是没有这个文件夹的，需要手动创建，创建完成后的文件路径如下（如图 2 所示）：

```
C:\Users\**username**\KLayout\salt
```

```{figure} _static/img/GDS_No2.png
:width: 100%
:align: center
:alt: 图 2 手动创建salt文件夹后的文件目录

图 2 手动创建salt文件夹后的文件目录
```

### 3. 为 salt 文件夹添加插件包

将前面下载的插件压缩包逐一解压，如图 3 所示。

```{figure} _static/img/GDS_No3.png
:width: 100%
:align: center
:alt: 图 3 解压后的插件包

图 3 解压后的插件包
```

修改解压后的插件包名称：

- 将 metainfo-ports-main 更名为 metainfo-ports
- 将 klive-main 更名为 klive
- 将 gdsfactory-main 更名为 gdsfactory

将更名后的插件包复制到前面创建的 salt 文件夹中，如图 4 所示。

```{figure} _static/img/GDS_No4.png
:width: 100%
:align: center
:alt: 图 4 完成配置的salt文件夹

图 4 完成配置的salt文件夹
```

配置完成后，最终的文件目录如下所示：

```
C:\Users\***\KLayout\salt\metainfo-ports 
C:\Users\***\KLayout\salt\klive 
C:\Users\***\KLayout\salt\gdsfactory
```

### 4. 验证插件是否安装成功

打开 KLayout (Editor) 软件，如图 5 所示。

```{figure} _static/img/GDS_No5.png
:width: 100%
:align: center
:alt: 图 5 打开KLayout (Editor) 软件

图 5 打开KLayout (Editor) 软件
```

如果安装成功，则 KLayout 软件的菜单栏里应该出现 gdsfactory 的选项，如图 6 所示。

```{figure} _static/img/GDS_No6.png
:width: 100%
:align: center
:alt: 图 6 插件安装成功的KLayout软件菜单栏

图 6 插件安装成功的KLayout软件菜单栏
```

至此，KLayout 软件已经完成配置，下面只需在 Python 环境中使用 gdsfactory 库进行版图绘制即可。

## 步骤三：配置 Python 开发环境

对于 Python 初学者，可以选择使用 PyCharm 进行版图绘制程序的编写，高手可以直接用 VS Code 进行代码的编写（可用 Conda 进行 Python 解释器的包管理），这里不再赘述。

### 1. 安装PyCharm软件并配置运行环境

这里不再赘述配置过程，可以在网络上找到很多相关教程，最终以能否正常运行 Python 代码为准，网络上的视频教程很多，建议跟着视频教程进行配置。

### 2. 安装 gdsfactory 库

点击 PyCharm 软件右下角的“解释器设置”选项，如图 7 所示。

```{figure} _static/img/GDS_No7.png
:width: 100%
:align: center
:alt: 图 7 解释器设置选项位置

图 7 解释器设置选项位置
```

点击安装“+”按钮。

```{figure} _static/img/GDS_No8.png
:width: 100%
:align: center
:alt: 图 8 Python库安装

图 8 Python库安装
```

输入 gdsfactory，点击“安装软件包”按钮，并点击“关闭”按钮返回 PyCharm 主界面，可观察软件右下角进度条，等待至 gdsfactory 库安装完成。

```{figure} _static/img/GDS_No9.png
:width: 100%
:align: center
:alt: 图 9 Python库安装

图 9 Python库安装
```

### 3. 检验是否配置成功

将 KLayout (Editor) 软件打开，在配置好的 Python 环境下，运行以下代码：

```python
import gdsfactory as gf

gf.gpdk.PDK.activate()

c = gf.Component()
c.add_polygon([(-8, -6), (6, 8), (7, 17), (9, 5)], layer=(1, 0))
c.show()
```

如果 PyCharm 软件没有报错，KLayout 软件将出现下图 10 所示的版图，则说明环境配置成功。

```{figure} _static/img/GDS_No10.png
:width: 100%
:align: center
:alt: 图 9 Python库安装

图 10 配置成功的KLayout版图绘制界面
```

## 注意事项

如果出现一些未知的报错，建议直接将报错信息复制到 ChatGPT 中，根据提示解决问题。

