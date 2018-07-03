---
title:  Golang官方依赖管理工具：dep
description: Golang官方依赖管理工具：dep 一些常用的用法
categories:
- Golang 
tags:
    - Golang
---

### 介绍
dep是一个原型依赖管理工具，需要在Go 1.7及更高的版本中使用
dep是官方版本，godep是第三方工具，但是他们的作者是同一个人

#安装dep
```
    go get -u github.com/golang/dep/cmd/dep
```
#验证安装
```
    $ dep
    Dep is a tool for managing dependencies for Go projects
    
    Usage: "dep [command]"
    
    Commands:
    
    init     Set up a new Go project, or migrate an existing one
    status   Report the status of the project's dependencies
    ensure   Ensure a dependency is safely vendored in the project
    prune    Pruning is now performed automatically by dep ensure.
    version  Show the dep version information
    
    Examples:
    dep init                               set up a new project
    dep ensure                             install the project's dependencies
    dep ensure -update                     update the locked versions of all dependencies
    dep ensure -add github.com/pkg/errors  add a dependency to the project
    
    Use "dep help [command]" for more information about a command.
```

### 常用命令

1. 初始化
```
    $ dep init
```
如果出现Gopkg.toml and Gopkg.lock are out of sync.时候最好执行一下dep ensure

2. 安装已有的依赖
如果你是用GitHub上拉去的代码 <code>dep ensure</code> 安装依赖
```
    $ dep ensure

```
执行dep ensure 为了更好地看到过程，加上参数-v

3. 添加依赖
```
    $ dep ensure -add github.com/pkg/foo

```

4. 添加依赖指定依赖版本
```
    $ dep ensure -add github.com/pkg/foo/subpkg@1.0.0 

```

5. 更新配置
```

    $ dep ensure -update
    Gopkg.toml and Gopkg.lock are out of sync. Run a plain dep ensure to resync them before attempting to -update
    $ dep  ensure 
    $ dep  ensure -update -v

```

5. 更多例子参考
```
    $ dep ensure -examples
```



## 参考
[https://studygolang.com/articles/10589](https://studygolang.com/articles/10589)
