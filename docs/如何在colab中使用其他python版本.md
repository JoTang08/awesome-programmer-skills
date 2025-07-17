# 在 Google Colab 中使用其他 Python 版本（如 Python 3.10）指南

## 背景

Google Colab 默认使用 Python 3.11（2025 年版本），但有些项目对 Python 版本有严格要求，比如需要 Python 3.10 才能正确安装和运行依赖包。

## 简要解决方案

本指南介绍如何在 Google Drive 上编译并安装指定版本的 Python（如 3.10），并在 Colab 中调用该版本，从而避免每次都重复安装依赖，实现环境持久化和隔离。  
关键步骤包括：

- 挂载 Google Drive
- 下载并编译 Python 3.10 到 Google Drive
- 使用 Drive 中的 Python 版本安装依赖
- colab 运行项目时调用 drive 中指定的 Python 路径

---

## 1. 挂载 Google Drive

每次使用 Colab 先挂载 Google Drive，方便存储自定义 Python 版本和依赖包：

```python
from google.colab import drive
drive.mount('/content/drive')
```

## 2. 在 Google Drive 创建安装目录

建议在 Drive 根目录创建专门文件夹存放 Python 和相关文件：

```python
%cd /content/drive/MyDrive
!mkdir -p py310
```

## 3. 下载 Python 3.10 源码并解压

进入刚创建的文件夹，下载官方 Python 3.10 源码包并解压：

```bash
%cd /content/drive/MyDrive/py310
!wget https://www.python.org/ftp/python/3.10.13/Python-3.10.13.tgz
!tar -xzf Python-3.10.13.tgz
```

## 4. 编译安装 Python 3.10

进入源码目录，依次执行以下命令：

```bash
%cd Python-3.10.13
!./configure --prefix=/content/drive/MyDrive/py310/python-install  --with-ensurepip=install --enable-optimizations
!make -j4
!make install
```

> --prefix 指定安装路径（即存放在 Drive 里的目录）  
>  --with-ensurepip=install 添加 ensuirepip 模块，方便后续安装 pip 模块
> --enable-optimizations 开启编译优化，提升运行效率  
> make -j4 使用 4 个 CPU 线程并行编译，加速过程

## 5. 验证 Python 3.10 安装成功

运行下面命令，确认 Python 3.10 版本正确：

```bash
!/content/drive/MyDrive/py310/python-install/bin/python3.10 --version
```

