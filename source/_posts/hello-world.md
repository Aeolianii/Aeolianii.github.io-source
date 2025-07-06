---
title: 如何使用github同步远程代码
---
作者在考完期末考后依照软工集市上的教程搭建了一个个人网站。由于作者有两台电脑，一台在家里，一台在学校，为了方便更新网站，便想在这两步电脑上同步网站代码，经过向豆包的不断提问，终于掌握了方法。下面想和大家分享一下我在同步过程中遇到的问题。为方便描述，两台电脑分别称为电脑1与电脑2。

## 1、静态文件与源码

作者用电脑1搭建完网站以后把它部署到了github上，然后美滋滋的把部署到github的代码仓库克隆到电脑2上，没想到电脑2却无法运行hexo的指令。我查询ai以后发现原来部署到github上的是静态文件，仅供预览。如果需要更新网站，则需要上传源码到github上，在进行克隆操作。

### 静态文件
静态文件是无需编译与解释、可直接被浏览器或程序读取的文件，内容固定且不依赖运行时计算。
静态文件由源码产生，所以我们生成与部署静态文件的时候可以使用以下指令：
``` bash
npm install -g hexo-cli  # 安装 Hexo 命令行工具
hexo init blog  ## 创建新的 Hexo 站点
cd blog  #进入到你的网站文件夹
npm install  # 安装依赖

配置 GitHub 仓库（下文会提到）

hexo clean  # 清理缓存和旧文件
hexo generate  # 或简写为 hexo g
npm install hexo-deployer-git --save  # 安装部署插件
hexo deploy  # 或简写为 hexo d
```


### 源码
源码指开发者编写的、用于实现特定功能的代码文件，是软件或项目的核心逻辑载体。我们需要更新网页则需要更新源码，所以同步代码其实是同步源码的意思，作者一开始还以为是在静态文件上修改，真是令人感慨。
以下是上传源码到github，并把它克隆到新电脑的过程：
#### 上传源码
``` bash
git --version  # 检查版本，若未安装需先安装

在 Hexo 项目根目录创建 .gitignore 文件（下文会提到）
在 GitHub 上创建源码仓库

git init  # 初始化本地 Git 仓库（首次上传需要）
git add .  # 添加所有文件
git commit -m "Initial commit"  # 提交到本地仓库，每次git commit 都需要添加一条简短描述，说明本次提交做了哪些修改。
git remote add origin git@github.com:用户名/仓库名.git  # 添加远程仓库地址(首次上传需要)
git push origin main  #上传（首次上传需要指定上游分支）
```
#### 克隆源码
首次：
``` bash
git clone git@github.com:Aeolianii/Aeolianii.github.io-source.git .  #.的意思是克隆到当前文件夹，所以输入指令之前要先进入到指定目录
npm install -g hexo-cli  # 安装 Hexo CLI（如果未全局安装）
npm install  # 安装项目依赖（根据 package.json）

```
非首次：
``` bash
git pull origin main  # 拉取最新代码（确保本地与远程同步）
npm install  # 安装可能新增的依赖
```


### 2、Github仓库使用注意事项
由于Github是全英文网站，且连接不稳定，所以在使用的时候也遇到了一些麻烦
#### 创建github仓库
``` bash
登录 GitHub 账号，点击右上角的 “New repository” 按钮，进入创建仓库页面。
填写仓库信息，包括仓库名称、描述等，选择仓库类型（Public 或 Private）。若勾选 “Initialize this repository with a README”，则会创建一个初始的 README.md 文件，方便后续管理。
点击 “Create repository” 按钮完成创建。
```

#### SSH KEY
SSH KEY把你的电脑和github联系起来，这样的话github就会允许你当前电脑去克隆以及上传代码
``` bash
打开终端，输入命令ssh-keygen -t rsa -C "your email@.com"，其中邮箱地址为注册 GitHub 时使用的邮箱，一路回车即可完成密钥创建。
打开存储.ssh 文件的位置，复制id_rsa.pub文件中的内容。
登录 GitHub 账号，进入 “Settings” 界面，点击左侧菜单中的 “SSH and GPG keys”，再点击 “New SSH Key” 按钮。在 “title” 处为密钥起一个标题，将复制的密钥粘贴到 “key” 框中，点击 “Add SSH KEY” 完成添加。
回到终端，输入ssh -T git@github.com，若出现相关提示信息，说明链接成功。
```

#### .gitignore忽略规则
.gitignore 是 Git 中用于指定需要忽略的文件或目录的配置文件，其作用是让 Git 不追踪这些文件，避免它们被意外提交到版本库中（例如临时文件、编译产物、敏感信息等）。同时也可以减小代码储存空间，使得上传与克隆更加快速。
我的.gitignore规则
``` bash
# Hexo默认忽略规则
.DS_Store
Thumbs.db
db.json
*.log
node_modules/    # 依赖包目录
public/          # 生成的静态文件
.deploy*/        # 部署临时文件
```
### 3、一些碎碎念
首次更新文章，还是有很多不熟练的地方，逻辑不是很通畅，要点也不是很齐全，等想到了再慢慢补充



