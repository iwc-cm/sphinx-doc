#########################################
环境搭建
#########################################


1. 新建 docs 目录. 
#. 进入 docs , 执行 ``sphinx-quickstart``。 不管提示什么选项，一律直接回车，除非遇到跳不过的选项，就仔细看看。
#. 打开 conf.py 修改以下配置。

    ::

        # 
        extensions = [
            'recommonmark',
            'sphinx_markdown_tables',
        ]

        source_suffix = ['.rst', '.md']
        language = 'zh_CN'
        html_theme = 'sphinx_rtd_theme'

    意思是: 支持markdown、后缀md的文件、语言为中文、使用 readTheDocs 主题

#. 新建 requirements.txt 输入以下内容。

    ::
    
        recommonmark
        sphinx-markdown-tables
        sphinx_rtd_theme

#. 安装依赖.

    ::

        pip install -r requirements.txt
