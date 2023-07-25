# 一个项目管理多个仓库

## 第一步 先创建一个蚂蚁 GitHub 仓库

git clone https://github.com/752337625/ant.git

## 第二步 subtree add ....

**git subtree add --prefix= **

```shell

git subtree add --prefix=packages/docs https://github.com/752337625/docs-package.git main --squash
git subtree add --prefix=packages/docs https://github.com/752337625/docs-package.git main --squash
git subtree add --prefix=internal/eslint-config https://github.com/752337625/eslint-config.git main --squash
git subtree add --prefix=internal/ts-config https://github.com/752337625/ts-config.git main --squash
git subtree add --prefix=internal/vite-config https://github.com/752337625/vite-config.git main --squash
```
