# pnpm 构建 monorepo

## 安装依赖

### 安装根目录依赖

```shell

pnpm add -w -D lodash
```

### 安装子项目依赖

**pnpm add -D 包名 -F package.json中的name**
**pnpm add -D 包名 --filter package.json中的name**

注意：-F要大写，否则异常

```shell
pnpm add  -D eslint --filter @ant/eslint-config
pnpm add  -D eslint-config-prettier -F @ant/eslint-config
pnpm add -D rimraf  --filter @ant/*

```

### 项目之间相互依赖

A项目依赖B项目

**pnpm add -D package.json中的name(B) -F package.json中的name(A)**
**pnpm add -D package.json中的name(B) --filter package.json中的name(A)**

```shell
pnpm add -D @ant/eslint-config --filter @ant/vite-config
```
