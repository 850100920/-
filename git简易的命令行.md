Git 全局设置:

```
git config --global user.name "小橘猫"
git config --global user.email "850100920@qq.com"
```

创建 git 仓库:

```
git init
git status
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/liuxingqi/notes.git
git push -u origin master
```

已有仓库?

```
cd existing_git_repo
git remote add origin https://gitee.com/liuxingqi/notes.git
git push -u origin master
```
