---
title: git子模块
date: 2019-01-23 15:18:41
tags: git
---

当项目越来越庞大之后，不可避免的要拆分成多个子模块，我们希望各个子模块有独立的版本管理，并且由专门的人去维护，这时候我们就要用到git的submodule功能。


> 如果直接使用`git clone`或`git init` 将子目录变成一个git仓库， 被嵌套的Git仓库不能被外层Git仓库检测到。

```bash
git clone https://github.com/yunxifd/git-test.git
```

## 添加子模块

```base
git submodule add https://github.com/yunxifd/git-test-2.git modules/test2 

# 或者
git clone --recursive https://github.com/yunxifd/git-test-2.git modules/test2
```

它会在主仓库中添加 `.gitmodules`文件，内容如下所示

```
[submodule "modules/test2"]
	path = modules/test2
	url = https://github.com/yunxifd/git-test-2.git
```

## 更新子模块
```
cd modules/test2
git pull
# 主仓库，添加更新子模块更新 提交
cd ../..
git add .
git commit -m "更新 test2子模块"
```

## 删除子模块
参考： https://stackoverflow.com/a/1260982

步骤
1. 删除`.gitmodules` 文件中子模块相关节点
1. 删除`.git/config` 文件中子模块相关节点
1. 运行`git rm --cached path_to_submodule` 将子模块移除版本控制
1. 运行`git commit -m "Removed submodule <name>"`
1. 删除未跟踪的子模块文件


## 克隆带子模块的项目
```bash
$ git clone https://github.com/yunxifd/git-test.git
```
查看 `modules/test2` 目录，会发现下面内容是空的

我们需要运行
```base
$ git submodule init # 初始化本地配置文件
Submodule 'modules/test2' (https://github.com/yunxifd/git-test-2.git) registered for path 'modules/test2'
$ git submodule update # 拉去子模块仓库的合适提交
Cloning into 'E:/myGithub/test2/modules/test2'...
Submodule path 'modules/test2': checked out '32895fb3ae7300da793e9f40a9486aaae3140b33'
```

## 参考资料
https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97