\# git常用命令	

把一个已有项目连接到Git

```bash
# 把一个已有项目连接到git
cd myProject
git init	# 初始化git项目
git add .
git commit -m "no msg"
git remote add origin http://github.com/xxx.git
git push -u origin master
```



关于.gitignore——用来忽略不需要上传的文件

GitHub提供的配置：https://github.com/github/gitignore

应该忽略哪些文件？

- 编译生成的中间文件，如.class
- 带有敏感信息的配置文件



其他常用命令

```bash
# 显示git配置
git config --list
# 编辑用户信息
git -config [--global] user.name "username"
git -config [--global] user.email "email"


```

