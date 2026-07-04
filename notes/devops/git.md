
## branch

给分支添加备注：
```Zsh
git checkout -b feature/new-login # 创建并切换到新分支
git branch --edit-description # 为当前分支添加或编辑备注说明，描述信息是存储在本地的 `.git/config` 文件中，不会被推送到远程仓库
git config branch.<branchName>.description # 查看备注说明 

git branch --list --verbose # 用于查看本地所有分支最新的提交哈希值和提交信息摘要
```

## commit

将projectA中a文件的最近几个commit内容，更新到projectB的b文件中：
```Zsh
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

修改commit message：
```Zsh
git commit --amend
```


