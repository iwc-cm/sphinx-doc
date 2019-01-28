#########################
复杂语法介绍
#########################


sphinx表格
===============

sphinx的表格需要自己绘制。如下

::

    +-------+-------+
    | 表头1 | 表头2 |
    +=======+=======+
    | 内容1 | 内容2 |
    +-------+-------+

效果如下

+-------+-------+
| 表头1 | 表头2 |
+=======+=======+
| 内容1 | 内容2 |
+-------+-------+

这种绘制表格的方法比较繁琐，但是能够充分支持各种奇形怪状的表格需求。

如果使用VSCode，推荐一个 ``Table Formatter`` 的插件，可以自动帮你绘制表格。
或者使用Pandoc将Markdown的文档转化为reStructuredText的文档。
MarkDown的表格虽然功能有限，但是写起来简单。

首页目录组织
===================

目录组织有两种方式。先看看这两种的展现形式。

.. image:: /_static/external_doc.jpg


目录树样式

    这种方式比较常用，通常是在另外一个文件中编写文档，然后把那个文件中的目录引入到当前文档。
    
    比如在 index.rst 中经常出现的如下引用::

        .. toctree::
            :maxdepth: 2
            :numbered:
            :hidden:

            simple/intro
            simple/base
            
    表示当前位置插入simple/intro.rst和simple/base.rst的目录，
    这种index.rst还可以被更上层的index.rst引用，从而产生多层嵌套，完成文档的组织。

    如果一个文档没有被任何目录树引用就会产生一个警告，所以，有时候为了消除这个警告就建立一个隐藏的目录树，
    像上面一样加入一个hidden的属性，就会隐藏。然后通过其他方式，比如超链接，链接到那个文档。

链接其他文件

    这种情况类似于超链接::

        :doc:`simple/complex`
            reStructuredText 复杂语法介绍

    使用这种语法，可以产生一个超链接，链接到其他文件，同时下面还可以附带一个介绍。


autodoc
==================

sphinx天生就是为了编写Python文档而设计，后来发展成了一个通用文档写作平台。

通过autodoc插件，可以让sphinx自动提取文档中的注释，形成文档。

.. important:: Python的注释同样需要符合 reStructuredText 语法，才能够正确解释。

为了使用autodoc插件，需要对sphinx进行一些配置，sphinx配置都放在了conf.py

1. 增加插件。

    在conf.py中的extensions变量加入autodoc插件::

        extensions = ['sphinx.ext.autodoc']
#. 指定代码路径。

    在conf.py开头的位置加入以下代码::

        import os
        import sys
        # 将自己的代码目录加入到sys.path, 具体路径视自己情况而定
        sys.path.insert(0, os.path.abspath('..'))

#. 在文档中使用autodoc自动引入代码中的注释作为文档.

    比如在文档中引入mongoengine.connect的文档::

        .. autofunction:: mongoengine.connect

    效果如下。

    .. image:: /_static/autodoc_example.jpg


Sphinx + MarkDown
============================

sphinx和MarkDown的结合主要有两种方式

* 使用Pandoc将MarkDown文档转化为rST文档, 有兴趣自己去研究，比较简单，不介绍。
* 使用sphinx的MarkDown插件 ``recommonmark`` 。现在介绍这种方式。

1. 安装插件

    .. code::

        pip install recommonmark sphinx-markdown-tables

2. 添加配置

    修改conf.py中的extensions.

    .. code::

        extensions = [
            'recommonmark',
            'sphinx_markdown_tables',
        ]

    修改source_suffix, 让sphinx识别 .md 后缀

    .. code::

        source_suffix = ['.rst', '.md']

然后就可以愉快地使用MarkDown了。
