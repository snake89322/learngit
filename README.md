## git开发日志

### 1 创建版本库
>2016年12月17日07:41:19

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
