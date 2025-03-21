[### 1. 安装Anaconda（4版本）、Jupyter notebook

#### 第一步

打开清华镜像源：https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/

![](https://gitee.com/capmlin/pictures/raw/master/typoro/image-20250227211635811.png)

找到对应版本号下载，例如自己是64位就点击对应64，下载安装并一直下一步。

查看版本号：

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321085441144.png)

#### 第二步

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321080242863.png)

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321080455996.png)

#### 第三步

打开anoconda prompt

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321080722284.png)

输入 ：

```
conda install  jupyter
```

执行：

```
jupyter notebook
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321081142624.png)

### 2. 完成Anaconda的国内镜像源的设置

打开anaconda prompt,逐次输入以下命令并回车：

```
conda config --remove-key channels #恢复默认源

# 添加清华大学镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
```

查看镜像源`conda config --show`

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321081828570.png)

### 3. 创建3个Anaconda下的虚拟环境，分别是python2环境(2.7.9版本)、python3环境(3.9.13版本)、python最新版本的环境。

* 这里如果报错的的话可以试试恢复默认镜像源或者更新一下官方镜像源，更新命令为`conda update conda`，因为旧版本少一些官方源，而一些包恰好在新的源。

```
conda create -n py2_7_9 python=2.7.9 #创建环境

activate py2_7_9 #激活环境

python --version # 查看python版本

deactivate py2_7_9 #退出环境
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321082417812.png)

同理安装3.9.13以及最新版本3.13.12

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321092958807.png)

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321093413283.png)

#### 4. 创建一个名字为MyMLenv环境，使用python3.11版本，然后确认当前该环境下是否包括scikit-learn、numpy、pandas、matplotlib包，如果没有，进行这3个包最新版本的安装

#### 第一步

```
conda create -n MyMLenv python=3.11 #创建环境

activate MyMLenv

python --version 

conda list #查看环境
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321170428508.png)

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321170510227.png)

#### 第二步

scikit-learn最新版本为1.6、numpy为2.2、pandas为2.2.3、matplotlib为3.10

```
conda install scikit-learn=1.6

conda install numpy=2.2

conda install pandas=2.2.3

conda install matplotlib=3.10
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321170001940.png)

### 5.基于某个已安装好的虚拟环境（MyMLenv），克隆一个新环境(MyMLenv_clone)

```
conda create --name MyMLenv_clone --clone MyMlenv

conda info --envs #查看环境列表
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321171242405.png)

#### 6. 某个Anaconda虚拟环境下(例如MyMLenv)：如何查看全部已安装的包?查看一共安装了多少个包?查看是否已安装某个包，例如scikit-learn ？

```
conda list -n MyMLenv
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321171648493.png)

查看有多少个包：

```
conda list --export | find /v "#" | find /c /v ""
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321172304572.png)

查看是否已经安装某个包：

```
conda list scikit-learn
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321172412119.png)

#### 7. 删除没用的Anaconda环境（例如MyMLenv_clone等）

```
conda env remove --name MyMLenv_clone
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321172546539.png)

#### 8. 创建一个新的Anaconda环境（例如MyMLenvAllinOne等）,成功安装scikit-learn、numpy、pandas、matplotlib、xgboost、lightgbm、pdfplumber、seaborn，然后验证是否已安装成功

```
conda create -n MyMLenvAllinOne
```

然后激活环境安装

```
conda install scikit-learn numpy pandas matplotlib xgboost lightgbm pdfplumber seaborn
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321173118184.png)

出现报错，这个时候用社区源来安装，若失败，用`pip install pdfplumber`,其他分别安装。

```
pip install pdfplumber --no-deps -i https://mirrors.aliyun.com/pypi/simple

conda install scikit-learn
conda install numpy
conda install pandas
conda install matplotlib 
conda install xgboost
conda install lightgbm 
conda install seaborn
```

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321181143641.png)

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321181254265.png)

#### 9. 在Jupyter notebook下面配置多个python环境，例如，python2.7.9、python3.9.13

```
activate py2_7_9

pip install ipykernel #因为python版本比较老，直接conda安装失败概率太大
python -m ipykernel install --user --name py2_7_9 #建立内核

activate py3_9_13
conda install ipykernel
python -m ipykernel install --user --name py3_9_13 #建立内核
```

回到base环境下执行`jupyter notebook`

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321183608493.png)

#### 10. Jupyter notebook下面个性化配置本地工程代码目录，例如：c:\myProjects\

执行

```
jupyter notebook --notebook-dir "C:\myProjects"
```

在c盘出现：

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321184141352.png)

#### 11. 在一个新的Anaconda环境（例如MyMLenvAllinOne等）下，使用pip方式安装pymysql，使用conda方式安装gensim，请问使用pip安装和conda安装有什么相同点？不同点？

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321184715497.png)

![](https://gitee.com/capmlin/pictures/raw/master/typoro/20250321184747301.png)

**pip** 和 **conda** 是 Python 生态中常用的包管理工具，虽然功能相似，但在设计目标和实现方式上有显著差异。以下是它们的相同点和不同点：

**相同点**

1. **安装 Python 包**  
   两者均可从各自的仓库（PyPI 或 Conda 仓库）安装 Python 包和依赖。
2. **依赖管理**  
   都能自动解析并安装包的依赖项。
3. **命令行工具**  
   均通过命令行操作，支持安装、卸载、更新等常见操作。
4. **支持虚拟环境**  
   均可配合虚拟环境使用（conda 内置环境管理，pip 通常与 `venv`/`virtualenv` 结合使用）。

---

#### **不同点**

| **对比维度**     | **pip**                               | **conda**                                        |
| ---------------- | ------------------------------------- | ------------------------------------------------ |
| **核心定位**     | Python 专属包管理器                   | 跨语言包管理器（支持 Python、R、C/C++ 等）       |
| **依赖来源**     | 仅从 PyPI（Python Package Index）安装 | 从 Anaconda 仓库或 Conda Forge 安装              |
| **依赖类型**     | 仅管理 Python 包                      | 管理 Python 包 + 系统级依赖（如 C 库、编译器）   |
| **环境隔离**     | 需配合 `venv`/`virtualenv` 创建环境   | 内置 `conda create` 环境管理，独立 Python 解释器 |
| **二进制包处理** | 可能需编译源码（依赖系统环境）        | 直接安装预编译的二进制包（跨平台兼容性更好）     |
| **依赖冲突处理** | 相对宽松，可能导致版本冲突            | 依赖解析更严格，尽量避免冲突                     |
| **跨平台一致性** | 依赖用户环境，可能需手动处理兼容性    | 强调跨平台一致性（如指定操作系统和架构）         |
| **适用场景**     | 轻量级 Python 项目、纯 Python 依赖    | 科学计算、数据科学、复杂依赖链项目               |

](https://github.com/adenaden432432/install_anaconda.git)
