---
title: git代码迁移
date: 2021-12-07 18:04:38
tags:
---

```shell
# 拉所有分支
git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
git fetch --all
git pull --all

# 删除旧源
git remote rm origin

# 改为新源
git remote add origin git@xxxx.com

# 推代码 全部分支 / 标签
git push --all
git push --tags
```

