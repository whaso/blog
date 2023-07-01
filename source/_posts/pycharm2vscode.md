---
title: pycharm2vscode.md
date: 2021-09-20 09:13:59
tags:
---

# VSCode常用快捷键

- 全部折叠:  `cmd + k` + `cmd + 0`



# 注:

## 关于导包

- PyCharm 可以在项目指定目录右键指定为导包路径, VSCode需要在`.vscode/launch.json`内 `settings.configurations` 配置`env`时加上 `"PYTHONPATH": "${fileDirname}/../smartbase:${fileDirname}"`多个目录通过 `:` 追加
