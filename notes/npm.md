
## npm

###### 查看帮助信息

```bash
npm --help # 列出所有顶级命令概览和基础用法
npm [command] --help # 查看具体命令的详细帮助：npm install --help
npm help [command] # 打开详细的command说明文档：npm help install
```

###### 查看包信息

```bash
npm view [<package-spec>] [<field>[.subfield]...]

# example
npm view express versions # 查看包所有版本
npm view ronn@0.3.5 dependencies # 查看某个版本的依赖信息
npm view express time'[4.8.0]' # 查看版本的发布时间
```

###### npm pack

将npm包打包成压缩包(.tgz)，用于发布前的本地预检和调试。生成的tarball与`npm publish`上传到npm仓库的文件完全一致。
```bash
npm pack axios # 下载线上package tarball到本地

cd /path/to/project
npm pack # 本地生成npm包，用于验证和测试
npm pack --dry-run # 静默模式，只在终端展示所有被包含的文件列表，并不会创建.tgz文件
```

###### 发布包

```bash
# 登录
npm login
npm whoami

# 构建产物
# 添加到scripts，prepublishOnly作为npm publish前钩子自动触发打包，避免遗漏
prepublishOnly：npm run build

# 预览和测试：使用pack本地构建包并验证测试
npm pack
cd ~/test-project
npm install /path/to/local-package.tgz

# 版本升级
npm version patch|minor|major

# 发布
npm publish --access public # 对于scope 包默认是私有，普通 npm 账号不能发私有，必须加参数公开
npm publish --tag beta # 发布beta版本

# 撤销发布
npm unpublish @scope/my-lib@1.0.0 # 撤销后版本号永久作废【不推荐】
npm deprecate @scope/my-lib@1.0.0 # 废弃【推荐】
```


## pnpm

- 节省磁盘空间：
	- 不同版本的依赖，只有不同的文件会添加到存储中；
	- 所有依赖包保存在磁盘同一个位置。使得在不同项目中可以共享相同版本的依赖，而不用单独安装。
- 快速：通过**硬链接**的方式写入到项目。
- 创建非扁平 node_modules 目录
- 工作区支持
- 管理运行时

```bash
# Node.js > v16.13.0
corepack enable pnpm

# 在项目package.json中添加`packageManager`字段，固定pnpm版本
corepack use pnpm@latest-10 

alias pn=pnpm # .zshrc，设置别名

pnpm --dir <path> <command> # 在path目录下运行命令，而不是当前工作目录
pnpm --workspace-root <command> # 在根目录下运行命令，而不是当前工作目录
pnpm --filter <package> <command> # 在指定包下运行命令
pnpm add <pkg> # 安装一个软件包及其依赖的所有软件包
```

###### approve-builds

pnpm 默认拦截依赖包的 `postinstall/install` 构建脚本（防止供应链恶意脚本），遇到需要编译二进制的包，需要**手动批准**才允许执行脚本。


## cnpm

```bash
# --registry=https://registry.npmmirror.com

cnpm web # 打开cnpm主站
cnpm sync [PackageName] # 从外站同步某个package到npmmirror 镜像站。也可以通过web方式同步：https://npmmirror.com/sync/[packageName]
```


## npx

Run a command from a local or remote npm package。

```bash
# npx：--option 会作为参数传给 foo
npx foo --option=xxx

# npm exec：npm会尝试解析 --option，不是传给foo
npm exec foo --option=xxx
npm exec foo -- --option=xxx # 正确写法：-- 分割，后面全部交给foo

# npm init：（aliases: create, innit）
npm init <package-spec> # same as npx create-<package-spec>
npm init <@scope> # same as npx <@scope>/create

# 等价关系：npx create-<package-spec>  ->  npm exec create-<package-spec>  ->  npm init <package-spec> ->  npm create <package-spec>

# example
npx create-vue@latest my-vue-app
npx skills add vercel-labs/agent-skills --skill vercel-optimize --agent claude-code cursor
```

| 命令             | 底层本质                                        | 核心用途                     | 参数要点                    | 适用场景                     |
| -------------- | ------------------------------------------- | ------------------------ | ----------------------- | ------------------------ |
| **npm run**    | 读取 `package.json` scripts，调用本地 bin          | 执行项目内预定义脚本               | 直接追加参数，不需要 `--`         | 项目脚本：dev/build/lint/test |
| **npm exec**   | npm 内置子命令，临时执行包                             | 一次性运行 cli 包（任意包）         | 传给 cli 的参数前**必须加 `--`** | 临时工具、monorepo、通用 cli     |
| **npx**        | 独立二进制，npm7 + 底层调用 npm exec                  | 一次性运行 cli 包（兼容旧版）        | 后面所有参数直接传给目标程序，不用 `--`  | 老教程、低版本 npm 环境           |
| **npm create** | `npm init xxx` 别名，内部调用`npm exec create-xxx` | 脚手架创建项目，仅匹配`create-xxx`包 | 传给脚手架参数前要加`--`          | 创建新项目：vue/vite/react     |


## 相关网站

[npmx.dev](https://npmx.dev/)：`npmjs.com` 的**社区驱动型替代界面**，旨在提供一个更快、更现代、信息更丰富的用户界面，来提升开发者搜索、评估和管理 npm 包的体验。

[docs.npmjs.com](https://docs.npmjs.com/)：npm官方文档。

[www.npmjs.com](https://www.npmjs.com/)：npm官方注册表前端界面。

[cnpm sync](https://npmmirror.com/sync/[packageName])：cnpm sync web同步地址。

[pnpm](https://pnpm.nodejs.cn/)：pnpm 中文网。