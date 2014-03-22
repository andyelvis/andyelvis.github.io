---
layout: post
title: Windows下Jekyll的安装和使用
categories:
- github
tags:
- github
---

## 安装Ruby环境

1、去[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)下载Ruby 2.0.0-p451安装，根据自己的系统版本选择32位还是64位版本，假设安装在D:\program_file\Ruby200-x64目录下，记得安装的时候选上“Add Ruby executables to your PATH”（添加系统环境变量）。

2、在第一步的下载页面，根据自己的系统版本以及Ruby版本，选择合适的DEVELOPMENT KIT版本下载安装，我安装的是64位的Ruby2.0版本，所以这里我下载的是DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe，假设安装在D:\program_file\ruby_devkit目录下。

3、打开cmd，进入D:\program_file\ruby_devkit目录，运行如下命令：  
ruby dk.rb init  
这时会在当前目录下生成config.yml文件。修改config.yml文件，在文件末尾添加上Ruby的安装路径：  
- D:/program_file/Ruby200-x64  
安装DEVELOPMENT KIT，运行如下命令：  
ruby dk.rb install

---

## 安装Jekyll

1、进入D:\program_file\Ruby200-x64\bin目录， 查看默认的gem镜像源列表：  
gem sources -l  
删除默认的源列表，将淘宝的镜像加到gem的镜像列表里：  
gem sources --remove http://rubygems.org/  
gem sources --remove https://rubygems.org/  
gem sources -a http://ruby.taobao.org/

2、安装Jekyll，默认安装的是Jekyll 1.4.3版本，这个版本在windows下运行会出错，所以这里安装1.4.2版本：  
gem install jekyll --version "=1.4.2"

3、Jekyll默认用maruku来解析markdown语言，你也可以用别的程序来解析，比如rdiscount或kramdown，都给装上吧：  
gem install rdiscount kramdown

---

## 安装Pygments

1、安装python2.7版本，并把python的安装路径加到系统的path环境变量中。

2、安装easy\_install，官方推荐的方式的是下载[https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py](https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py)，然后运行  
python ez\_setup.py。  
另一种方式是下载[http://python-distribute.org/distribute_setup.py](http://python-distribute.org/distribute_setup.py)，然后运行  
python distribute\_setup.py。

3、安装Pygments，进入easy\_install的安装目录，一般是在python的安装目录的Scripts目录下，运行如下命令：  
easy_install Pygments

4、检查pygments.rb的版本，运行gem list查看pygments.rb的版本，如果不是0.5.0版本，需要先移除然后在安装0.5.0版本，非0.5.0版本与Jekyll不太兼容：  
gem uninstall pygments.rb --version "=0.5.4"  
gem install pygments.rb --version "=0.5.0"

---

## 运行Jekyll

初始化一个站点，运行命令：  
jekyll new myblog  
会在当前目录下生成myblog目录，进入这个目录，然后启动jekyll：  
cd myblog  
jekyll serve  
然后在浏览器中输入[http://localhost:4000](http://localhost:4000)查看。  
如果出现中文编码的问题，只需在myblog目录下的_config.yml文件中添加：  
encoding: utf-8

---







