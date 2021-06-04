# Git命令

- ==初始化本地仓库==

```sh
git init
```

- 修改默认分支为main分支

```bash
git config --global init.defaultBranch main
```

- 修改默认分支为任意分支，比如main_main

```bash
git config --global init.defaultBranch main_main
```

- ==删除远程Git仓库==

```sh
git remote rm origin
```

- ==查看状态==

```bash
git status   
```

- ==将当前目录下修改的所有代码从工作区添加到缓存区==

```bash
git add . 
```

- ==将缓存区内容添加到本地仓库==

```bash
git commit -m "注释"
```

- 拉取远程仓库代码合并到本地

```sh
git pull
```

- ==将本地仓库的代码推送到远程仓库==

```sh
git push origin main
```

