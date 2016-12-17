## git开发日志

### 1 创建版本库

```sh
git init
/* Initialized empty Git repository in E:/A-Github/learngit/.git/ */
git add <file>
/* 成功 - 不提示
失败 - fatal: pathspec 'hehe.md' did not match any files */
git commit -m "xxx"
/* [master (root-commit) 67ec98e] create README.md
1 file changed, 7 insertions(+)
create mode 100644 README.md */
```

* Q1: 新文件不运行git add能否commit？

```sh
// 新建Q1.md

git commit -m "Q1.md not add"
/* On branch master
Changes not staged for commit:
        modified:   README.md

Untracked files:
        Q1.md

no changes added to commit */
// commit失败
```

```sh
git add README.md
git commit -m "Q1.md not add"
/* [master db49c77] Q1.md not add
1 file changed, 24 insertions(+), 2 deletions(-) */
```

- [x] A1: 命令行中需要有git add操作之后才能够进行commit，否则不会进行commit
>全部提交请 git add -A

* Q2: 文件的删除是否能用git add操作？
```sh
// 删除Q1.md

git commit -m "remove Q1.md"
/* On branch master
On branch master
Changes not staged for commit:
        deleted:    Q1.md

no changes added to commit */
// commit失败
```

```sh
git add Q1.md
git commit -m "remove Q1.md"
/* [master e71df2e] remove Q1.md
 1 file changed, 1 deletion(-)
 delete mode 100644 Q1.md */
```

- [x] A1: git add 可以看作是修改操作，删除的文件也可用add进行确认
>目录是否clear使用git status 提示 working tree clean
>要随时掌握工作区的状态，使用git status命令。

### 2 命运石之门

```sh
// 查看未关机状态下的log
git log --pretty=oneline
// 查看未来的HEAD
git reflog
// 穿梭
git reset --hard commit_id
/*
首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
*/
```

>HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
>穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
>要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
>如果git status告诉你有文件被修改过，用git diff可以查看修改内容，配合reflog，命令是 git diff HEAD@{3} -- README.md

### 3 工作区和暂存区

**工作区**：工作目录，使用IDE修改或者本地资源管理器

**暂存区**：stage，版本库commit之前的存储区，用于存储修改的区域

**分支**：commit的目标区，git默认commit后会提交至master分支

![pic](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

### 4 SSH
```sh
// 生成SSH
ssh-keygen -t rsa -C "youremail@example.com"

// 生成目录找到id_rsa.pub，复制里面的内容

// 去网页Settings > Deploy keys > Add deploy key 粘贴SSH信息

// 即可在本地提交 git push 命令
```
不同电脑SSH重复创建即可

```sh
// 网页在repositories中创建新的learngit

// 添加远程链接
git remote add origin git@github.com:snake89322/learngit.git

// 首次push
git push -u origin master

// 之后push
git push origin master
```