# 一个项目管理多个仓库

以下命令基本都需要在顶层目录执行

## 第一步 先创建一个蚂蚁 GitHub 仓库

```shell
git clone https://github.com/752337625/ant.git
cd ant
```

## 第二步 subtree add ....

**git subtree add --prefix=自定义目录/自定义目录/自定义目录 仓库地址 分支 --squash**

```shell
git subtree add --prefix=packages/docs https://github.com/752337625/docs-package.git main --squash
git subtree add --prefix=packages/ui https://github.com/752337625/ui-package.git main --squash
git subtree add --prefix=internal/eslint-config https://github.com/752337625/eslint-config.git main --squash
git subtree add --prefix=internal/ts-config https://github.com/752337625/ts-config.git main --squash
git subtree add --prefix=internal/vite-config https://github.com/752337625/vite-config.git main --squash
```

--squash 意思是把 subtree 的改动合并成一次 commit，这样就不用拉取子项目完整的历史记录。如果不加 --squash 参数，主项目会合并子项目本身所有的 commit 历史记录，加上 --squash 参数是把子项目的记录合成一次 commit 提交到主项目，这样主项目只是合并一次 commit 记录。

## 提交更改

### 默认更改提交

蚂蚁仓库的提交和我们平时提交代码到仓库一模一样,不会对子仓库进行提交

### 提交到子仓库更改

> Git 会遍历所有的 蚂蚁仓库的 commit，从中找出针对 指定子仓库目录的更改，然后把这些更改记录提交到 子仓库的 Git 服务器上

**git subtree push --prefix=自定义目录/自定义目录/自定义目录 仓库地址 分支**

> "自定义目录/自定义目录/自定义目录",这里注意是本地放代码的位置

```shell
git subtree push --prefix=packages/docs https://github.com/752337625/docs-package.git main
git subtree push --prefix=packages/ui https://github.com/752337625/ui-package.git main
git subtree push --prefix=internal/eslint-config https://github.com/752337625/eslint-config.git main
git subtree push --prefix=internal/ts-config https://github.com/752337625/ts-config.git main
git subtree push --prefix=internal/vite-config https://github.com/752337625/vite-config.git main
```

注意:push 的内容是所有关于子仓库变动的内容,不会包含其他仓库的.但是可能的公用一个 commits 描述.

高阶：每次 push 命令都会遍历全部的 commit,当你的项目越来越大,commit 的数上来的时候,等待时间就会很长。--rejoin 避免了遍历全部 commit 的问题.

不要看了

```shell
# git subtree split --rejoin --prefix=自定义目录/自定义目录/自定义目录 --branch <临时 branch>
git subtree split --rejoin --prefix=packages/docs --branch srcTemp
# git push <S 项目远程库仓库地址 | S 项目远程库别名> srcTemp:master
git push share srcTemp:master
```

## 更新目录

### 默认更新

蚂蚁仓库的更新和我们平时更新代码到仓库一模一样,不会对子仓库进行更新

### 更新子目录

**git subtree pull --prefix=自定义目录/自定义目录/自定义目录 仓库地址 分支 --squash**

```shell
git subtree pull --prefix=packages/docs https://github.com/752337625/docs-package.git main
git subtree pull --prefix=packages/ui https://github.com/752337625/ui-package.git main
git subtree pull --prefix=internal/eslint-config https://github.com/752337625/eslint-config.git main
git subtree pull --prefix=internal/ts-config https://github.com/752337625/ts-config.git main
git subtree pull --prefix=internal/vite-config https://github.com/752337625/vite-config.git main
```

## 缺点

git 更新/提交只能提交到主仓库,子仓库需要依次执行有关子项目的 git 命令;
git 代码pull，push慢;
git 代码容易产生冲突，解决不易;
git 代码必须主仓库目录依次拉去,子仓库;
