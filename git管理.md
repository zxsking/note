## 1.进行git管理

```bash
git init
```

## 2.添加文件到本地仓库

```bash
git add .   #添加所有文件
git add [某个文件名]   #添加指定文件
```

## 3.查看仓库的提交状态

```bash
git status
```

### 4.提交

```bash
git commit -m "提交信息"
```

## 配置邮箱及用户名

```
git config --global user.email "邮箱"
git config --global user.name "用户名"
```

## 关联github

```bash
git remote add origin https://github.com/zxsking/[repositoriesname].git（上面有说到）
```

报红黄色错误

```bash
git pull origin main
```

若之后报错no common commit则输入

```
git pull --rebase origin main
```

再将本地仓库push到github仓库

```
git push -u origin main
```





## 将本地仓库push到github仓库

```bash
git push -u origin main
```







## 提交代码时会因检查文件换行符报错，为避免报错可执行以下代码

```
git config --global core.autocrlf true
```





