## SSH-Key

```Shell
ssh-keygen -t rsa -C '2008042226@163.com' # 生成公钥和私钥

cd ~/.ssh # 存放目录
cat id_rsa.pub # 复制公钥，添加到https://github.com/settings/keys

ssh -T git@github.com # 验证
```

## commitlint

```Shell
# @commitlint/cli - commitlint 命令行工具
# @commitlint/config-conventional - Commits 规范
pnpm add @commitlint/cli @commitlint/config-conventional --save-dev

# 测试配置是否生效
echo 'feat: 这是一段提交信息' | npx commitlint
```

###### .commitlintrc.cjs

[文档](https://commitlint.nodejs.cn/reference/configuration.html#config-option-cli)

```js
module.exports = {
	extends: ["@commitlint/config-conventional"], // 遵循 Conventional Commits 规范
	rules: {
		// 规则名称: [校验级别：0(禁用)、1(警告)、2(错误), 应用时机：always(总是触发)、never(从不触发触发), 规则值]
		'type-enum': [2, 'always', ['feat']]
	},
	// 将校验报告（Report）转换为带颜色/符号的可读终端输出字符串数组
	formatter: "@commitlint/format",
	// Array of functions that return true if commitlint should ignore the given message.
	ignores: [(commit) => commit === ""],
}
```

## lefthook



## branch

###### 给分支添加备注

```Shell
git checkout -b feature/new-login # 创建并切换到新分支
git branch --edit-description # 为当前分支添加或编辑备注说明，描述信息是存储在本地的 `.git/config` 文件中，不会被推送到远程仓库
git config branch.<branchName>.description # 查看备注说明 

git branch --list --verbose # 用于查看本地所有分支最新的提交哈希值和提交信息摘要
```

## commit

###### 将projectA中a文件的最近几个commit内容，更新到projectB的b文件中

```Shell
cd /path/to/projectA
# 查看指定文件的最近4个 commit 的哈希值
git log --oneline -4 -- /path/to/file
# 将提交记录转换成补丁文件
git format-patch -4 -- /path/to/file -o /patches
# 复制到项目B的根目录
cp /patches/*.patch /path/to/projectB/

# 在项目B应用补丁

# 1、文件路径和名称完全一致
cd /path/to/projectB
git am *.patch

# 2、文件路径或名称不一致
# 修改 *.patch 文件中 `--- a/...` 和 `+++ b/...` 行中的路径
```

###### 修改commit message

```Shell
git commit --amend
```


