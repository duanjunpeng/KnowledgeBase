# 1、编写文档的目的
LLM的真正价值不是一次性问答，而是充当"知识编译器"，把原始素材喂进去，持续维护一个结构化的知识库，知识被编译一次然后保持更新，而不是每次查询时从头推导。
# 2、整体设计
**Obsidian**：指的是笔记软件本身（也就是应用程序）。
**Obsidian vault（库）**：指的是由 Obsidian 软件打开和管理的**本地文件夹**，里面存放着你的所有笔记文件（.md格式）、附件和配置。

1. **Obsidian vault**：就是一个文件夹，路径在本地磁盘上。里面的核心结构很简单：两个文章目录（AI编程实验室/、机器学习实验室/），两个.base 数据库视图文件，两个canvas 选题规划文件，再加上_knowledge_base/ 素材库和 _briefs/等日常写作需求记录。
2. Claude Code通过Obsidian Skills插件集来操作这个vault。目前我装了5个Obsidian Skills：defuddle（网页抓取）、obsidian-cli（命令行操作）、obsidian-markdown（Markdown 语法）、obsidian-bases（数据库视图）、json-canvas（画布文件）。
3. 简单来说就是，Obsidian负责存储和展示，Claude Code负责读写和智能处理。两者通过文件系统天然打通，不需要任何额外的API对接。

> [!warning] 两个架构经验
> 1. 目录结构尽量扁平。试过在`_knowledge_base/`下按主题分子文件夹，Claude Code在超过两层嵌套时搜索效率明显下降。现在就一层，靠文件名前缀区分，反而更好用。
> 2. vault一定用Git做版本控制，Claude Code偶尔会改错文件，有Git随时能回滚。

# 3、环境准备
## 3.1 安装Obsidian
1. 下载[Obsidian](https://obsidian.md/zh/)
2. 安装Obsidian
## 3.2 创建知识仓库
1. 点击【新建仓库】，创建知识库
## 3.3 Obsidian集成Git插件
1. 在Preferences设置中选择【第三方插件】
2. 关闭安全模式
3. 浏览社区插件市场搜索并安装【Git】
## 3.4 初始化Git

1. 安装git
```shell
brew install git
```
2. git 配置用户信息
```shell
git config --global user.name "duanjunpeng" # github 的用户吗
git config --global user.email "1470219613@qq.com" # github 的邮箱
```
3. 初始化git
```shell
cd 个人知识库/ # 进入个人知识库路径
git init
```

4. 关联远程仓库（如果不管了github则不用这一步）
```shell
git remote add origin https://github.com/duanjunpeng/KnowledgeBase.git

```
5. 提交测试
```shell
# 1. 创建一个测试文件
touch README.md

# 2. 用命令 git add 告诉 Git，把文件添加到仓库
git add README.md

# 3. 用命令 git commit 告诉 Git，把文件提交到仓库
git commit -m "首次提交" # -m 后面输入的是本次提交的说明

# 4. 把本地仓库的所有文件上传到 GitHub 上
git push -u origin main
# 运行命令之后，一般需要输入 GitHub 账号的用户名和密码
# 用户填邮箱
# 关于密码：GitHub 已于 2021 年 8 月 13 日起禁止使用账户密码进行 Git 操作，必须使用个人访问令牌（Personal Access Token） 或 SSH 密钥 来认证。

# 登录 GitHub → 点击右上角头像 → Settings → 左下角 Developer settings → Personal access tokens → Tokens (classic) → Generate new token (classic)

# 验证关联
git remote -v

```
6. 配置`.gitignore`
```shell
# 在你的笔记库根目录下创建 `.gitignore` 文件，并填入以下内容来忽略临时文件和缓存，避免同步冲突
cat << EOF > .gitignore
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/cache
.trash/
**/.DS_Store
EOF
```