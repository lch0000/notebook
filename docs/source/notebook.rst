.. _htmlnotebook:

The Jupyter Notebook
====================

介绍
------------

Notebook 扩展了控制台的交互计算功能，它提供了一个web应用程序来很方便的处理整个计算过程。这其中包括开发，记录，执行代码和生成结果。
Jupyter notebook由两个构件组成：

**一个web应用程序**: 一个基于浏览器的交互式文档编辑工具，它可以将说明性的文字，数学公式，计算过程和其他多媒体的资源有机的结合起来。

**Notebook文档**: 它是web应用程序中所有可见内容背后对应的源文件。包括之前所说的文字，公式，多媒体资源等。

.. seealso::

    看下 :ref:`安装向导 <jupyter:install>` 描述了如何安装notebook和它的相关依赖库.


Notebook的web应用的主要特性
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 在浏览器中编辑代码时，可以自动的代码染色，缩进，并且可以支持自动完成和内省。（试试Tab键）

* 从浏览器执行代码的能力，当执行时将计算的结果附加在代码的后边。

* 使用富媒体元素来显示计算的结果，例如HTML，LaTeX，PNG，SVG等等. 例如，可以引用并使用 matplotlib_ 库来绘图。

* 在浏览器编辑富文本时可以使用 Markdown_ 这种文本标记语言，他可以为代码提供注释和更加美观的行文结构，而不局限于纯文本。

* 可以使用LaTeX支持很容易的将复杂的数学公式放入markdown的元素中，使用 MathJax_ 来渲染。



.. _MathJax: https://www.mathjax.org/


Notebook文档
~~~~~~~~~~~~~~~~~~
Notebook文档包含交互式会话的输入输出，还有一些用来说明代码的文本（它们并不需要被执行）。以这种方式，notebook文件可以成为一个会话的完整信息记录，将可执行代码和解释性文本、数学公式、富媒体元素混排，这些文件的内在是 JSON_ 文件并被存储为 ``.ipynb`` 格式。因为JSON是纯文本格式，所以Notebook文档可以通过版本控制工具管理并和同事分享。

.. _JSON: https://en.wikipedia.org/wiki/JSON

通过使用 nbconvert_ 命令，Notebooks可以被输出为多种静态格式，这其中包括HTML(例如博客)，reStructuredText，LaTeX，PDF，还有幻灯。

此外，任何 ``.ipynb`` 后缀的notebook文档可以通过 `Jupyter Notebook Viewer <nbviewer>`_ (nbviewer_)分享成为一条开放的URL链接。这个服务可以从URL读取notebook文档并将它转化为一个静态的web页面。这样的结果可以用来和同事分享，或者作为一个博客，来提供给那些并没有安装Jupyter notebook需求的人们。事实上， nbviewer_ 作为一个web服务是一个简化的 nbconvert_ ，因此你可以通过nbconvert做你自己想要的静态转换，而不是必须要依赖于nbviewer.



.. seealso::

    :ref:`详细介绍了notebook JSON的文件格式 <nbformat:notebook_file_format>`


开启notebook服务
----------------------------

你可以通过以下的命令开启一个notebook服务::

    jupyter notebook

这将在你的控制台上打印出一些关于notebook服务的信息，随后会通过你的浏览器自动打开该web应用的URL(默认是 ``http://127.0.0.1:8888``)。

Jupyter notebook的web应用主页是 **仪表盘** ，它列出了当前可用的notebook路径下所有的notebooks(默认状态下，这个路径是notebook启动时执行命令所在的路径)。

你可以通过点击 ``New Notebook`` 按钮来从仪表盘创建一个新的notebooks，或者通过点击一个notebooks的名字来打开它。你也可以拖放 ``.ipynb`` notebooks 或者标准的 ``.py`` Python源代码文件到notebook的列表中。

当从命令行启动了一个notebook服务，你也可以直接打开一个特殊的notebook，通过仪表盘上的 ``jupyter notebook my_notebook.ipynb`` 。 如果没给出扩展名那么就使用 ``.ipynb`` 作为扩展名。

当你正在编辑一个打开的notebook时， `File | Open...` 菜单选项将会在浏览器的新标签页打开仪表盘，这允许你从notebook路径打开一个另外的notebook文件或是创建一个新的notebook。


.. note::

   如果你想在不同路径上的notebooks上工作，你可以同一时间开启多个notebook服务。默认的，notebook服务第一次启动在8888端口，之后再启动notebook服务，它会找寻邻近的端口。当然，你也可以通过 ``--port`` 手动配置端口。

创建一个新的notebook文档
~~~~~~~~~~~~~~~~~~~~~~~~

一个新的notebook可以在任何时间被创建出来，既可以通过仪表盘，也可以使用一个活动的notebook中的 :menuselection:`File --> New` 菜单来创建。新的notebook创建在一个相同的路径，之后在浏览器的新标签页被打开。它也可以被当做仪表盘notebook列表的一个新入口。

.. image:: _static/images/new-notebook.gif


打开notebooks
~~~~~~~~~~~~~
一个打开的notebook拥有 **确切的** 连接到内核的交互式会话，它可以执行用户发送的代码并返回结果。即使浏览器窗口被关闭了，内核仍然会保持活动状态，可以通过重新在仪表盘中打开相同的notebook来重新将web应用链接到之前的内核。在仪表盘中，拥有活动内核的notebooks会有 ``Shutdown`` 按钮，而没有活动内核的则会显示 ``Delete`` 按钮取而代之。

其它的客户端可能连接到相同的内核。当一个内核启动之后，notebook服务打印到终端类似如下的信息::

    [NotebookApp] Kernel started: 87f7d2c0-13e3-43df-8bb8-1bd37aaf3373

这个长字符串是kernel的ID，这对于拿到链接到内核的必要信息来说已经足够了。如果notebook使用Ipython内核，你也可以通过运行 ``%connect_info`` :ref:`magic <magics_explained>` 来看到连接信息，这在打印相同的ID信息的同时也会打印其它细节。

你可以通过命令行手动开启Qt控制台，这样可以在参数上加上部分ID来链接到 *你想要的* 内核。

    $ jupyter qtconsole --existing 87f7d2c0

如果没有给出ID，那么 ``--existing`` 参数将会链接到上一个打开的内核。

如果在使用IPython内核，你也可以在notebook中运行 ``%qtconsole`` 命令，从而打开Qt控制台来链接指定的内核。
:ref:`magic <magics_explained>` in the notebook to open a Qt console connected
to the same kernel.

.. seealso::

    :ref:`ipythonzmq`

Notebook的用户接口
------------------

当你创建一个新的notebook文档后，你将得到一个 **notebook名称**, 一个 **菜单栏**, 一个 **工具栏** 和一个空的 **代码单元** 。

**notebook名称**: notebook文档的名称被显示在页面的顶端，挨着 ``IP[y]: Notebook`` 的logo。这个名字指向了后缀名为 ``.ipynb`` 的notebook文档。当你点击这个notebook的名字后，会弹出一个对话框来允许你进行重命名。举个例子，在浏览器里重命名一个notebook从"Untitled0"到"My first notebook"，这个操作将会使文件从 ``Untitled0.ipynb`` 变为 ``My first notebook.ipynb`` 。

**菜单栏**: 菜单栏提供了不同的选项，可以用来操作notebook的功能。

**工具栏**: 工具栏给出一种快捷的方式，可以通过点击图标来使用经常被使用到的那些操作。

**代码单元**: 默认的单元格类型，你可以从单元格的描述中得到更多的解释。

.. note::

    当使用notebook4.1版本时，用户接口允许多个单元格被选中。从菜单栏找到 ``quick celltype selector``，当多个单元格被选中，而显示 ``-`` ，这表明选择的多个单元格的类型可能不一致。此时此刻，快速选择器仍然可以改变所有当前被选中的单元格的类型。


notebook的文件结构
------------------

notebook由一些列的子单元构成。一个子单元是一个多行文本的输入域，它所包含的内容可以通过 :kbd:`Shift-Enter` 或点击工具栏上的“Play”按钮或菜单栏的 `Cell | Run` 来执行。一个子单元的执行方式由子单元的类型来决定。我们有三种子单元的类型: **code cells** ， **markdown cells** ，和 **raw cells** 。子单元初始是 **code cell** ，但是它的类型可以通过工具栏上的下拉菜单或是快捷键 :ref:`keyboard shortcuts <keyboard-shortcuts>` 来改变。

想要获取更多信息，请看这里 `集合的例子 <http://nbviewer.jupyter.org/github/jupyter/notebook/tree/master/docs/source/examples/Notebook/>`_ 。

代码单元
~~~~~~~~
一个 *代码单元* 允许你在代码染色和自动完成的帮助下编辑或写入新的代码。代码单元的默认语言是Python，但也可以切换为 ``Julia`` 和 ``R`` 语言，通过使用 :ref:`cell magic commands <magics_explained>` 来进行切换。

当你执行代码单元时，它所包含的代码被notebook发送到内核。返回的计算结果被作为单元的 *output* ，显示在notebook中。该输出不局限于文本，还有很多其他的输出类型，其中包括 ``matplotlib`` 图标和HTML标签(举个常用的例子，比如在 ``pandas`` 数据分析的扩展包中)。这些是已知的IPython的 *多媒体显示* 能力。

.. seealso::

   `Rich Output`_  notebook的例子

Markdown单元
~~~~~~~~~~~~
你可以用一种更好的方式将计算过程书写为文档，从而使描述文本和代码交互结合，这种方式就是使用 *富文本* ，在IPython中，这是通过Markdown这种文本标记语言来实现的。此时相应的单元被叫做 *Markdown单元* 。Markdown语言提供了一种简单的方式去实现这种标记，比如强调（斜体），着重，列表等。

如果你想为你的文档添加结构，你可以使用markdown的标题。Markdown标题包含1到6个#标记 ``#`` 在你标题句的首尾。markdown的标题将被转换为notebook章节中的一种可以电机的链接。当导出为PDF这类文档时它也可以被用作是一种提示。

当Markdown单元被执行，Markdown代码会被转化为相应格式的富文本。Markdown支持HTML代码格式。

在Markdown单元中，你可以使用标准LaTeX符号来书写 *数学公式* ： ``$...$`` 用来内联数学公式，
``$$...$$`` 用来显示数学公式。 当Markdown单元被执行，LaTeX部分会被自动渲染为HTML格式，并输出为高质量印刷格式。这些通过 MathJax_ 来实现，它支持LaTeX的功能性 `大子集 <mathjax_tex>`_ 。

.. _mathjax_tex: http://docs.mathjax.org/en/latest/tex.html

标准的数学环境定义为LaTeX，AMS-LaTeX (使用 `amsmath` 扩展包)也可以，例如 ``\begin{equation}...\end{equation}`` 和  ``\begin{align}...\end{align}`` 。新的LaTeX可以使用标准模式来定义，例如 ``\newcommand`` ，只需要将它们放置在Markdown单元中任何位置的两个 *数学分隔符之间* 。这些定义可以在IPython的其它会话中使用。

.. seealso::

    `Working with Markdown Cells`_ notebook例子

Raw单元
~~~~~~~

*Raw* 单元可以让你直接写 *输出* 。Raw 单元不会被notebook处理。当经过 nbconvert_ 处理，raw单元直接达到目的格式而未经过修改。举个例子，这种方式允许你在raw单元中键入完整的LaTeX，而不用担心它被nbconvert转化。


基本的工作流
------------

notebook中的正常工作流与标准IPython的会话非常相似，不同之处在于你可以对同一单元格进行多次编辑，直到你得到想要的结果，而不需要使用 ``%run`` 命令来重新运行脚本。


通常情况下，你可以将准备计算的问题分解，把相关的想法组织到单元格中，直到这部分正确工作了再进行下一步。这对于交互式探索来说比将计算分解为必须一起执行的脚本来说要方便许多。拆分脚本在以前是很有必要的，特别是如果某一部分会执行很长时间的情况。

在某些时候，可能有必要中断一个耗时过长的计算。这可以用 `Kernel | Interrupt` 菜单或 :kbd:`Ctrl-m i` 快捷键来完成操作。同样的，也可以通过 `Kernel | Restart` 或者 :kbd:`Ctrl-m .` 来重启整个计算过程。

执行菜单选项 `File | Download as` 可以将notebook下载为 ``.ipynb`` 或 ``.py`` 文件。如果选择 ``.py`` 选项下载Python ``.py`` 脚本，它将会移除所有的多媒体输出并且将markdown单元格的内容转化为注释插入进来。

.. seealso::

    `Running Code in the Jupyter Notebook`_ notebook例子

    `Notebook Basics`_ notebook例子

.. _keyboard-shortcuts:

键盘快捷键
~~~~~~~~~~
notebook中所有的操作都可以使用鼠标执行，但键盘快捷键也可用于最常见的操作。以下是常见的几种需要记忆的快捷键：

* :kbd:`Shift-Enter`: 执行单元格
    执行当前单元格，如果有输出则将其显示，然后跳转到下一个单元格。如果在最后一个单元格上调用 :kbd:`Shift-Enter` ，则还会创建一个新的代码单元格。需要注意的是，在notebook中，自己输入 :kbd:`Enter` *从不* 强制执行，它只会在当前单元格中插入新的行。:kbd:`Shift-Enter` 相当于点击 ``Cell | Run`` 菜单项。

* :kbd:`Ctrl-Enter`: 原地执行单元格
    像在“终端”模式中执行当前单元格一样，显示所有输出，但光标还 *停留* 在当前单元格中。单元格的全部内容在执行后被选中，此时你再键入新的内容的话老内容将被清除。这对于进行快速实验或查询诸如文件系统一类的操作是很方便的，用完就扔掉。

* :kbd:`Alt-Enter`: 执行单元格，并在之后插入
    执行当前单元格，显示输出，并且插入一个 *新的* 单元格在当前的单元格和下一个单元格（如果存在的话）之间。这是序列的快捷键 :kbd:`Shift-Enter` ，:kbd:`Ctrl-m a` 。（:kbd:`Ctrl-m a` 添加一个新的单元格在当前单元格之前。）

* :kbd:`Esc` 和 :kbd:`Enter`: 命令模式和编辑模式
    在命令模式下，你可以使用键盘快捷键轻松浏览notebook。
    在编辑模式下，你可以编辑单元格文本。

想获得全部的可用快捷键列表，请在notebook菜单中点击 :guilabel:`Help` ，:guilabel:`Keyboard Shortcuts` 。

绘制
----
Jupyter notebook的一个主要的特点是能够显示所运行的代码单元的输出图形。IPython内核被设计为与 matplotlib_ 绘图库无缝协作来提供该功能。特定绘图库集成功能是内核的一个特性。

安装内核
--------

有关如何安装Python内核，请参阅 `IPython安装页面 <http://ipython.org/install.html>`__.

其它语言的内核可以在 `IPython wiki <https://github.com/ipython/ipython/wiki/IPython%20kernels%20for%20other%20languages>`_ 中找到。它们通常会附带说明教你如何在notebook中使该内核可用。


.. _signing_notebooks:

Notebook签名
-------------

为防止用户在notebook上打开并执行不可信的代码，我们在notebook上添加了一个签名，存储在元数据中。notebook服务器在notebook被打开时验证这个签名。如果存储在notebook中的元数据签名不匹配，JavaScript和HTML输出将不会在加载时显示，它们必须通过重新执行单元格来重新生成。

你自己执行的任何notebook都会 *作为一个整体* 被信任，并且其HTML和JavaScript输出将在加载时显示。

如果你需要查看HTML或JavaScript输出而不想重新执行单元格，你可以明确信任notebook，例如那些共享给你的或者你之前用IPython2.0写的那些，可以在命令行中如下操作::

    $ jupyter trust mynotebook.ipynb [other notebooks.ipynb]

这将会产生一个签名存储在这些notebook中。

你可以通过如下方法生成一个新的notebook的秘钥::

    $ jupyter trust --reset

.. include:: links.txt

浏览器兼容性
------------

Jupyter Notebook受以下浏览器的最新稳定版本的正式支持:

* Chrome
* Safari
* Firefox

这主要是因为notebook使用了WebSockets和flexible box model（一种CSS技术）。

以下版本的浏览器不被支持:

* Safari < 5
* Firefox < 6
* Chrome < 13
* Opera （任何版本）: 只存在CSS问题，执行上应该没问题
* Internet Explorer < 10
* Internet Explorer ≥ 10 (和Opera一样的原因)

在Safari下当使用HTTPS和不受信任的证书时不能正常工作（websockets会失败）。
