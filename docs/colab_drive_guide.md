# 使用 Google Drive 持久存储与 Google Colab 集成指南

## 什么是 Google Drive？

Google Drive 是 Colab 的“云硬盘”，可以作为文件读写的后端，持久保存你的一切数据和代码。  
相比 Colab 的临时环境，Drive 中的文件不会因断开连接而丢失，非常适合存放数据集、模型权重和项目代码。

---

## 如何在 Colab 中挂载 Google Drive？

在 Google Colab Notebook 的代码单元格中直接运行以下代码：

```python
from google.colab import drive
drive.mount('/content/drive')
```
系统会弹出一个授权链接，登录你的 Google 账号后，即可成功挂载。

![alt text](drive-mount-success.png)

## 克隆 Git 项目到 Google Drive
```
%cd /content/drive/MyDrive/
!git clone https://github.com/coqui-ai/TTS.git

```
这样项目代码将被保存到 Google Drive，避免 Colab 会话断开导致文件丢失。