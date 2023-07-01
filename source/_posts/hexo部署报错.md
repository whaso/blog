---
title: hexo部署报错
date: 2021-12-09 11:25:26
tags:
---

### 报错内容

```shell
fatal: in unpopulated submodule '.deploy_git'
FATAL {
  err: Error: Spawn failed
      at ChildProcess.<anonymous> (/Users/krmac/myProjects/blog/node_modules/hexo-util/lib/spawn.js:51:21)
      at ChildProcess.emit (node:events:390:28)
      at Process.ChildProcess._handle.onexit (node:internal/child_process:290:12) {
    code: 128
  }
}
```

### 解决

直接删除 `.deploy_git`  重新 `hexo g` 生成即可

