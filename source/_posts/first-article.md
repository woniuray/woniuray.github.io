---
title: Github+hexo搭建网站
date: 2016-10-12 19:46:28
tags: github hexo
categories: github hexo
---
# 本博客是采用github+hexo搭建的一个静态小站
### 摘要
      由于以前的域名空间到期了，想想还是搭建一个免费的博客。正好了解到github上有gh-pages
    这项功能，看到简洁的hexo-next主题心动了，因此就用它来搭建自己的博客。 
<!--more-->
#### 建站准备
        1. github账号
        2. git
        3. Node.js
        4. hexo
        5. 多说账号
       
#### 安装环境
        2.1 安装git
                2.1.1 Windows下安装git
                    从官网下载git安装包(默认安装即可)，下载地址：   https://git-for-windows.github.io
                2.1.2 进入git bash进行设置
                    git config --global user.name "yourname"
                    git config --global user.email "email@example.com"
                2.1.3 SSH Key
                    生成SSH Key
                        在git bash下：ssh-keygen -t rsa -C "youremail@example.com" (直接所有确定即可)
                        生成.shh目录和id_rsa(私钥)、id_rsa.pub(公钥)
                    添加SSH Key到github上
                        cd ~/.shh （进入.shh目录）
                        cat id_rsa.pub （查看公钥内容）
                        登录github，进入个人设置（Personal settings）
                        选择SSH and GPG keys
                        选择New SSH key 将id_rsa.pub的内容复制到里面即可
        2.2 安装Node.js
                2.2.1 Windows下安装：
                    官网下载：   https://nodejs.org/en/download/ （默认安装即可）
                    测试是否成功cmd进入DOS环境输入node --version 检查node.js版本
        2.3 安装hexo博客框架
                npm install -g hexo-cli  （前提是安装node.js）
        2.4 安装git插件
                npm install hexo-deployer-git --save
#### github创建仓库
        选择Create a new repository
        repository name命名规则: woniuray.github.io woniuray为随便起的内容,我的名字叫woniuray（其它默认创建即可）
#### 博客创建
        4.1 初始化
                hexo init woniuray.github.io （woniuray.github.io为文件名）
        4.2 主题安装
                默认主题是：landscape（无需安装），不想安装主题的可以跳过此步骤
                我的主题是next，你也可以选择自己喜欢的主题进行安装
                $ cd your-hexo-site
                $ git clone https://github.com/iissnan/hexo-theme-next themes/next
        4.3 基础配置
                4.3.1 站点配置
                    站点配置文件是在woniuray.github.io文件下的* _config.yml *文件
                    ```
                    # Site
                    title: 杂记 //博客名字
                    subtitle: 吾尝终日而思矣，不如须臾之所学也  //副标题
                    description: "学习==>积累==>进步"   //博客描述
                    author: woniuray   //作者名字
                    language: zh-Hans  //网站语言中文
                    timezone:          //时区设置默认
                    # URL
                    url: http://woniuray.github.io  //自己站点的域名
                    root: /                         //站点目录
                    theme: next                     //站点主题
                    deploy:                                     
                      type: git                     //使用git发布
                      repository: https://github.com/woniuray/woniuray.github.io.git  //3步骤github创建的仓库
                      branch: master                 //分支
                    ```
                4.3.2 主题配置
                    主题配置文件为themes/next目录 _config.yml
                    主题默认配置即可
#### 博客发布
        5.1 博文创建
            在woniuray.github.io目录下输入命令
            $ hexo new '文件名' //会在source/_posts创建一个文件名.md文件
        5.2 博文编辑
            编辑生成的.md文件(博文是用Markdown语法写的)
            ---
            title: new//博客标题
            date: 2016-10-10 10:47:49 //创建时间
            tags:  //分类标签
            ---
            正文（上面的---是必要的）
        5.3 博文预览
            本地预览，执行命令：
            $ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）（简写 hexo s）
            浏览器打开https://localhost:4000本地查看
        5.4 发布到github上
            $ hexo clean
            $ hexo generate #生成静态页面至public目录(简写 hexo g)
            $ hexo deploy #将.deploy目录部署到GitHub(简写 hexo d)
#### 增加评论功能
        评论功能有自带的disqus，不过国内还是使用多说
        6.1 多说账号
            由于多说是使用QQ、微博、微信、豆瓣、谷歌、百度等账号登录的，无需申请，直接登录即可
            多说网址： http://duoshuo.com/ 点击我要安装
            创建站点
                站点名称：自己随便写
                站点地址：自己站点的域名 例如：http://woniuray.github.io 
                多说域名：自己写
        6.2 配置主题文件开启评论功能
            在themes/next目录下打开 _config.yml，设置
            duoshuo_shortname:  nanshanyi //上面多说域名中填的内容
            需要分享的打开duoshuo_share: true 即可，支持分享到微博、QQ空间、微信
#### 增加本地搜索功能
        7.1 安装hexo-generator-search插件
            在博客目录下输入下面命令
            $ npm install hexo-generator-search --save
        7.2 主题配置文件中增加
            themes/next/_config.yml添加
            search: 
              path: search.xml
              field: post
#### 增加标签页、分类页
        8.1 命令创建
            $ hexo new page tags //会在woniuray.github.io/source下创建tags文件夹内部是一个index.md和index文件夹
            $ hexo new page categories  //同理
        8.2 站点配置文件配置
            将menu：对应下的#去掉
            menu:
              home: /
              categories: /categories
              archives: /archives
              tags: /tags
#### 关于主题的使用
        更多关于本主题的使用请参考：http://theme-next.iissnan.com/