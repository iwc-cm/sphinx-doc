

####################
sphinx 项目介绍
####################

sphinx是一个Python包，如果没有安装，需要先使用pip安装：

.. code-block:: bash

    pip install sphinx

新建sphinx项目
==================

新建一个空目录，执行sphinx-quickstart

.. code-block:: bash

    mkdir docs && cd docs;
    sphinx-quickstart

然后会有很多询问步骤，一般直接默认就好了，后期可以重新在配置文件 ``conf.py`` 中修改。

有几个选项需要注意填写，项目名称，作者，版本号。但是这几个字段依然可以后期在配置文件中修改。

构建sphinx
=============

新建项目之后，或者文档编写完成之后，执行 make 构建。

不带任何参数执行make，会打印所有选项。
常用的是 ``make html`` 可以构建为html类型的文档。构建完成后可以在 _build/html中，打开index.html查看.

sphinx配置
============

extensions

    sphinx的插件，常用的有: 
    
    * sphinx.ext.autodoc: 自动从python代码中抽取文档。
    * recommonmark: markdown的支持。需要额外安装。

language:

    当前文档语言，中文填写 ``zh_CN``

    查看所有语言以及代号: http://sphinx-doc.org/config.html#confval-language

html_theme

    构建HTML格式文档时使用什么主题。

latex_elements

    latex 选项，构建pdf文档时会使用到。
