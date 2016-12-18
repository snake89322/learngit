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


* Q1: 回滚指定版本，保留记录，并且提交远程库？
```sh
git revert HEAD@{*}
git push origin
```
- [x] A1: 如果是前一次版本可用git revert HEAD
- [x] A2: 如果是非前一次版本的之前版本，需要解决conflict后再add&commit

>revert是放弃指定提交的修改，但是会生成一次新的提交，需要填写提交注释，以前的历史记录都在，而reset是指将HEAD指针指到指定提交，历史记录中不会出现放弃的提交记录。

* Q2: 回滚指定版本，不保留记录，并且提交远程库？
```sh
git reset --hard HEAD@{*}
git push origin -f
```
- [x] A1: 使用hard要慎重，后悔药git reflog还能玩

* Q3: 删除历史的commit，并且提交远程库？
```sh
git rebase -i "commit id"
git push origin -f
```
- [x] A1: 有conflict得解决
- [x] A1: 进入后删除对应的pick即可，然后:wq保存

* Q3: 修改历史的commit？
>这种情况的解决方法类似于Q2情况，只需要在第二条打开编辑框之后，将你想要修改的提交所在行的pick替换成edit然后保存退出，这个时候rebase会停在你要修改的提交，然后做你需要的修改，修改完毕之后，执行命令。
```sh
git add .
git commit --amend
git rebase --continue
```
- [x] A1: 如果你在之前的编辑框修改了n行，也就是说要对n次提交做修改，则需要重复执行以上步骤n次
- [x] A2: 在执行rebase命令对指定提交修改或删除之后，该次提交之后的所有提交的"commit id"都会改变


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

```sh
// 从远程库clone
git clone git@github.com:michaelliao/gitskills.git // SSH地址 推荐 速度快

git clone https://github.com/michaelliao/gitskills.git // https地址 速度慢 每次push都要输入口令
```
### 5 平行宇宙

![pic](http://www.liaoxuefeng.com/files/attachments/001384908633976bb65b57548e64bf9be7253aebebd49af000/0)

```sh
// 创建dev分支
git checkout -b dev

//等同于
git branch dev
git checkout dev
```

```sh
// 合并dev分支
git checkout master // 先切换至主分支
git merge dev // 合并
```

```sh
// 删除dev分支
git branch -d dev
```

