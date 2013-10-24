---
layout: post
title: "Octopress博客配置笔记:1"
date: 2013-10-21 17:26
comments: true
categories: [CentOS, Octopress Blog, GitHub]
---
<a href="http://octopress.org/" class="fl_left a_unline">
{% img insert_img /images/post_img/octopress.jpg Octopress %}
</a>
<a href="https://github.com/" class="fl_left a_unline">
{% img insert_img /images/post_img/github.jpg github %}
</a>

<p class="clear" /></p>

安装此博客时，参照了官方的一些说明文档( <a href="http://octopress.org/docs/">octopress</a>、<a href="https://help.github.com/categories/20/articles">github</a> )，外加自己的google。
<!-- more --> 
第一步

安装Octopress 到您的系统。
我的系统环境为“centos 6.3”。

安装 git
{% codeblock %}
yum install git
{% endcodeblock %}

安装Ruby，Ruby版本必须大于1.9.3，不使用Ruby的话可以使用“rbenv 或 RVM.”，在这里我使用的时Ruby。 Octoperss使用yaml格式文件作为配置文件，所以还需要安装libyaml。 先安装 libyaml
{% codeblock %}
wget http://pyyaml.org/download/libyaml/yaml-0.1.4.tar.gz
tar xzvf yaml-0.1.4.tar.gz
cd yaml-0.1.4
./configure --prefix=/usr/local
make
make install
{% endcodeblock %}

安装Ruby
{% codeblock %}
#使用ftp下载
lftp ftp.ruby-lang.org
lftp ftp.ruby-lang.org:/> cd /pub/ruby
lftp ftp.ruby-lang.org:/pub/ruby>
lftp ftp.ruby-lang.org:/pub/ruby> get ruby-1.9.3.pXXX.tar.gz  # 选择合适的版本下载
lftp ftp.ruby-lang.org:/pub/ruby> exit
#编辑安装
tar zxvf ruby-1.9.3.pXXX.tar.gz
cd ruby-1.9.3.pXXX
./configure --prefix=/usr/local --enable-shared --disable-install-doc --with-opt-dir=/usr/local/lib
make
make install
{% endcodeblock %}

安装Octopress
{% codeblock %}
git clone git://github.com/imathis/octopress.git octopress
cd octopress

# 安装相关依赖
gem install bundler
bundle install

# 安装默认主题
rake install

#设置您的github链接(http://username.github.io)，当用在rake deploy时，octopress知道要将源码提交到哪
rake setup_github_pages
{% endcodeblock %}

到这里Otopress就安装好了。

第二步

配置您的github

登录github，github为每个用户提供一个个人主页，为每每个项目提供一个项目主页。这些都是只能是静态HTML文件的。 进去后您会看到类似于“yourname.github.io”这样的一个字样，和您创建的项目列在一起，点击链接进去。 可以参考这个<a href="https://help.github.com/articles/creating-pages-with-the-automatic-generator" target="_blank">页面</a>，从第一步到第六步。 这样直接访问“yourname.github.io”，就可以看到您刚才设置的那套模板了！我们就是利用这一种方式来搭建一个速度可观，无限流量的blog。

生成SSH keys

当您提交代码到您的github时，git是需要权限验证的。所以您需要用您注册时所使用的email来生成一个唯一的SSH keys，并为这设置密码。
{% codeblock %}
ssh-keygen -t rsa -C "your_email@example.com"
# Creates a new ssh key, using the provided email as a label
# Generating public/private rsa key pair.
# 直接回车，将文件存放在用户目录
# Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter]
ssh-add id_rsa

# 输入密码
Enter passphrase (empty for no passphrase): [Type a passphrase]
# Enter same passphrase again: [Type passphrase again]
{% endcodeblock %}

将生成的key复制到您的github账户
{% codeblock %}
cd ~/.ssh
vi id_rsa.pub
# 显示类似于这样的字符：ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAu2PxN9ft1wdaFaMcQJbS+MOTKsEJ6nU....
{% endcodeblock %}
添加操作”Account settings -> SSH Keys -> Add SSH key”，完成添加。

测试连接是否正常
{% codeblock %}
ssh -T git@github.com
#输入密码后，当看到显示下面的字符时，说明连接成功
#Hi yourname! You've successfully authenticated, but GitHub does not provide shell access.
{% endcodeblock %}

Octopress博客配置笔记:1

【完】





