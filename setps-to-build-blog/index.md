# 使用hugo搭建blog


Hugo是最流行的开源静态站点生成器之一。凭借其惊人的速度和灵活性，Hugo使构建网站变得非常简单。

## 安装 hugo
``` bash
brew install hugo
```
## 新建一个blog网站
``` bash
hugo new site blog
```
## 选择一个 Hugo 主题
1. 访问 hugo 主题: https://themes.gohugo.io/
2. 选择一个主题， 比如 LoveIt:  https://github.com/dillonzq/LoveIt
3. git clone 至blog目录下
``` bash
cd blog
git clone https://github.com/dillonzq/LoveIt.git themes/LoveIt
```
4. 编辑配置文件 config.toml
refer: https://hugoloveit.com/zh-cn/theme-documentation-basics/#top

## 新建一篇文章
``` bash
hugo new post/my-first-post.md
```
在文章中随便写点什么
## 本地预览
``` bash
hugo server -D 
```
参数 -D, --buildDrafts            include content marked as draft
打开网址 http://localhost:1313/ 即可查看本地生成的静态网站

## 部署至 github
1. 在github中新建一个repo: your_name.github.io, 注意`your_name`必须是你的 github 的 username
2. 执行一下命令
``` bash
git init
git add --all
git commit -m 'first commit'
git remote add origin git@github.com:username/username.github.io.git
git push -u  origin master 
```
登陆 https://your_github_name.github.io 查看效果

