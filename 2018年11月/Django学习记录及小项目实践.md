# Django学习记录以及小项目实践

Django学习记录以及小项目实践

项目地址：https://github.com/shuming9886/Django_sinacrawler

## 前言

传统Web开发需要编写大量代码，工作量大，代码重复性高，且业务逻辑过于复杂，不利于长期维护。对于开发者来说，选择一个简洁、高效的开发框架，将会大大提高开发效率。

## 项目实践

项目要求是做一个微博爬取页面。页面的具体功能是基于**关键词**搜索的微博爬取。爬取一定数量的微博，并将微博展示在页面上。微博在页面上滚动展示。
使用环境：Python 3.5，Django 2.1

## Django简介

Django是一个开放源代码的Web应用框架，由**Python**写成。采用了MVC的框架模式，即模型M，视图V和控制器C。它最初是被开发来用于管理劳伦斯出版集团旗下的一些以新闻内容为主的网站的，即是CMS（内容管理系统）软件。这套框架是以比利时的吉普赛爵士吉他手**Django Reinhardt**来命名的。

Django是由python开发的一个免费的开源网站框架，可以用于快速搭建高性能、 优雅的网站。 Django框架遵循MVC (Modern,view,controler)开发模式 ，包含多种web开发组件，同时拥有一个独立的轻量级web服务器，为快速开发 web 应用提供便利。具体说来它具有以下特点： ①强大的数据库功能：用python的类继承，几行代码就可以拥有一个丰富，动态的数据库操作接口（API），如果需要也能执行SQL语句。②自带的强大的后台功能：几行简单的代码就让网站拥有一个强大的后台，可轻松管理网站内容。 ③优雅的网址：用正则匹配网址，传递到对应函数，随意定义， 如你所想。 ④模板系统：强大，易扩展的模板系统，设计简易，代码、 样式分开设计，更容易管理。 ⑤缓存系统：与 memcached 或其甩的缓存系统联用，更出色的表现，更快的加载速度。 ⑥国际化：完全支持多语言应用，允许你定义翻译的字符，轻松翻译成不同国家的语言。

## Django使用方法

在Python3 命令行中依次输入：

``1. django-admin startproject projectname``
新建一个项目（project），projectname为新创建的项目名

``2. python manage.py startapp appname``
新建一个应用（app）

第三步，将新定义的**app**加到settings.py中的INSTALL_APPS中。

第四步，在终端上运行：
``python manage.py runserver``

**startproject**命令创建一个目录，包含4个文件：

```python
mysite/
        __init__.py
        manage.py
        settings.py
        urls.py
```

- *\__init__.py*：让Python把该目录当成一个开发包（即一组模块）所需文件。这是一个空文件，一般你不需要修改它。

- *manage.py*：一种命令行工具，允许你以多种方式与该Django项目交互。键入 ``python manage.py help``，看一下它能做什么。你应当不需要编辑这个文件；在这个目录下生成它纯是为了方便。

- *settings.py*：该Django项目的设置或配置。查看并理解这个文件可用的设置类型及其默认值。

- *urls.py*：Django项目的URL设置。可视其为你的django网站的目录。
