
- 节省磁盘空间：
	- 不同版本的依赖，只有不同的文件会添加到存储中；
	- 所有依赖包保存在磁盘同一个位置。使得在不同项目中可以共享相同版本的依赖，而不用单独安装。
- 快速：通过**硬链接**的方式写入到项目。
- 创建非扁平 node_modules 目录
- 工作区支持
- 管理运行时

## install

```Zsh
# Node.js > v16.13.0
corepack enable pnpm

corepack use pnpm@latest-10 # 在项目package.json中添加`packageManager`字段，固定pnpm版本
```


## 基本命令

```Zsh
alias pn=pnpm # .zshrc，设置别名

pnpm --dir <path> <command> # 在path目录下运行命令，而不是当前工作目录
pnpm --workspace-root <command> # 在根目录下运行命令，而不是当前工作目录

pnpm --filter <package> <command> # 在指定包下运行命令

pnpm add <pkg> [-D|-P|-g|-O] # 安装一个软件包及其依赖的所有软件包
pnpm install [--force|--offline|--lockfile-only] # 安装所有项目的所有依赖 i
pnpm reintstall 
pnpm update [<package>] [--latest] # 更新指定范围的软件包到最新版本 upgrade、up
pnpm remove <package> # 删除软件包 rm、uninstall、un
pnpm link [<dir>] [<package>] # 使当前本地包可在系统范围内或在其他位置访问 -- unlink
pnpm prune # 删除不必要的包
```

## pnpm approve-builds

解决 pnpm 构建脚本被阻止（Ignored build scripts）的问题。

### 为什么需要？

- 安全策略：pnpm 默认阻止包的构建脚本（如postinstall、preinstall等）
- 依赖包行为：某些包（如 esbuild）在安装后需要运行构建脚本（如esbuild、node-sass等）
- 许可列表：pnpm 需要明确的许可才能运行这些脚本

### 

```Zsh
# 全局设置批准所有包（不推荐，有安全风险）
pnpm config set --global ignore-scripts false

# 批准单个包
pnpm install --ignore-scripts=false esbuild


```

https://blog.csdn.net/Irene1991/article/details/155789404