## git开发日志

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
    // 提交失败
```
