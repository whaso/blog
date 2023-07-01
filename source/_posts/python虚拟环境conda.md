---
title: python虚拟环境conda
date: 2023-04-26 14:18:19
tags: python conda
---

# conda

> mac下安装完anaconda后会自动安装conda，进入终端会自动启动base虚拟环境（自带的默认虚拟环境）

## 常用命令

### 基操

1. `conda create`：创建新的虚拟环境。`conda create -n py39 python=3.9`
2. `conda activate`：激活一个已经存在的虚拟环境。
3. `conda deactivate`：停用当前激活的虚拟环境。
4. `conda list`：列出所有已安装的包及其版本号。
5. `conda install`：安装新的包。
6. `conda update`：更新已安装的包。
7. `conda remove`：卸载已安装的包。
8. `conda search`：搜索可用的包。
9. `conda info`：查看conda的配置信息。
10. `conda clean`：清理conda中的缓存、未使用的软件包和环境。
11. `conda config`：配置conda的选项。





## 常见问题

### mac下安完anaconda后进终端会自动启用base虚拟环境

- 使用 `conda config --set auto_activate_base false` 关闭

