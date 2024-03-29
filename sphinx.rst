Sphinx
======

Sphinxのインストール
--------------------
::

  # easy_install sphinx

作業フォルダの作成
------------------

"sphinx"という名前のフォルダを作成します．

::

  # mkdir ~/sphinx
  # cd ~/sphinx

初期化
------

sphinxの初期設定を行います．

::

  # sphinx-quickstart

質問項目が順番に出てきますので，答えてください．最低限，次の項目を入力してあとはデフォルトでよいでしょう．

- Project name
- Author name(s): User Name
- Project version: 0.1

以下の例では，これらのほか

- Separate source and build directories (y/N) [n]:

のみ「y」と答えています．

::

   Welcome to the Sphinx 1.0.7 quickstart utility.

   Please enter values for the following settings (just press Enter to
   accept a default value, if one is given in brackets).

   Enter the root path for documentation.
   > Root path for the documentation [.]:

   You have two options for placing the build directory for Sphinx output.
   Either, you use a directory "_build" within the root path, or you separate
   "source" and "build" directories within the root path.
   > Separate source and build directories (y/N) [n]: y

   Inside the root directory, two more directories will be created; "_templates"
   for custom HTML templates and "_static" for custom stylesheets and other static
   files. You can enter another prefix (such as ".") to replace the underscore.
   > Name prefix for templates and static dir [_]:

   The project name will occur in several places in the built documentation.
   > Project name: My first sphinx
   > Author name(s): User Name

   Sphinx has the notion of a "version" and a "release" for the
   software. Each version can have multiple releases. For example, for
   Python the version is something like 2.5 or 3.0, while the release is
   something like 2.5.1 or 3.0a1.  If you don't need this dual structure,
   just set both to the same value.
   > Project version: 0.1
   > Project release [0.1]:

   The file name suffix for source files. Commonly, this is either ".txt"
   or ".rst".  Only files with this suffix are considered documents.
   > Source file suffix [.rst]:

   One document is special in that it is considered the top node of the
   "contents tree", that is, it is the root of the hierarchical structure
   of the documents. Normally, this is "index", but if your "index"
   document is a custom template, you can also set this to another filename.
   > Name of your master document (without suffix) [index]:

   Sphinx can also add configuration for epub output:
   > Do you want to use the epub builder (y/N) [n]:

   Please indicate if you want to use one of the following Sphinx extensions:
   > autodoc: automatically insert docstrings from modules (y/N) [n]:
   > doctest: automatically test code snippets in doctest blocks (y/N) [n]:
   > intersphinx: link between Sphinx documentation of different projects (y/N) [n]:
   > todo: write "todo" entries that can be shown or hidden on build (y/N) [n]:
   > coverage: checks for documentation coverage (y/N) [n]:
   > pngmath: include math, rendered as PNG images (y/N) [n]:
   > jsmath: include math, rendered in the browser by JSMath (y/N) [n]:
   > ifconfig: conditional inclusion of content based on config values (y/N) [n]:
   > viewcode: include links to the source code of documented Python objects (y/N) [n]:

   A Makefile and a Windows command file can be generated for you so that you
   only have to run e.g. `make html' instead of invoking sphinx-build
   directly.
   > Create Makefile? (Y/n) [y]:
   > Create Windows command file? (Y/n) [y]:

   Finished: An initial directory structure has been created.

   You should now populate your master file ./source/index.rst and create other documentation
   source files. Use the Makefile to build the docs, like so:
      make builder
      where "builder" is one of the supported builders, e.g. html, latex or linkcheck.



日本語化する設定
----------------

設定ファイルをエディタで開きます．

::

  # emacs ~/sphinx/source/conf.py &

次の通り，languageをja（日本語）にします．

::

  # The language for content autogenerated by Sphinx. Refer to documentation
  # for a list of supported languages.
  language = 'ja'

文書を生成する
--------------

HTMLを生成する
~~~~~~~~~~~~~~

以下のコマンドでhtmlを生成することができます．

::

  # make html

lsコマンドで確認してみましょう．

::

  # ls ~/spinx/_build/html

PDFを生成する
~~~~~~~~~~~~~
config.pyのextensionsを次の通り変更します．

::

  # Add any Sphinx extension module names here, as strings. They can be extensions
  # coming with Sphinx (named 'sphinx.ext.*') or your custom ones.
  extensions = ['rst2pdf.pdfbuilder']

config.pyに次の設定を追加します．

::

   -- Options for PDF output --------------------------------------------------

   # Grouping the document tree into PDF files. List of tuples
   # (source start file, target name, title, author, options).
   #
   # If there is more than one author, separate them with \\.
   # For example: r'Guido van Rossum\\Fred L. Drake, Jr., editor'
   #
   # The options element is a dictionary that lets you override 
   # this config per-document.
   # For example, 
   # ('index', u'MyProject', u'My Project', u'Author Name', 
   #  dict(pdf_compressed = True))
   # would mean that specific document would be compressed
   # regardless of the global pdf_compressed setting.

   pdf_documents = [ 
   ('index', u'MyProject', u'My Project', u'Author Name'),
   ]

   # A comma-separated list of custom stylesheets. Example:
   pdf_stylesheets = ['sphinx','ja']

   # Create a compressed PDF
   # Use True/False or 1/0
   # Example: compressed=True
   #pdf_compressed = False

   # A colon-separated list of folders to search for fonts. Example:
   pdf_font_path = ['~/fonts']

   # Language to be used for hyphenation support
   pdf_language = "ja"

   # Mode for literal blocks wider than the frame. Can be
   # overflow, shrink or truncate
   #pdf_fit_mode = "shrink"

   # Section level that forces a break page.
   # For example: 1 means top-level sections start in a new page
   # 0 means disabled
   #pdf_break_level = 0

   # When a section starts in a new page, force it to be 'even', 'odd',
   # or just use 'any'
   #pdf_breakside = 'any'

   # Insert footnotes where they are defined instead of 
   # at the end.
   #pdf_inline_footnotes = True

   # verbosity level. 0 1 or 2
   #pdf_verbosity = 0

   # If false, no index is generated.
   #pdf_use_index = True

   # If false, no modindex is generated.
   #pdf_use_modindex = True

   # If false, no coverpage is generated.
   #pdf_use_coverpage = True

   # Documents to append as an appendix to all manuals.    
   #pdf_appendices = []

   # Enable experimental feature to split table cells. Use it
   # if you get "DelayedTable too big" errors
   #pdf_splittables = False

   # Set the default DPI for images
   #pdf_default_dpi = 72


Makefileを編集します．

::

  # emacs ~/sphinx/Makefile &

次の設定を追加します．

::

   pdf:
	   $(SPHINXBUILD) -b pdf $(ALLSPHINXOPTS) $(BUILDDIR)/pdf
	   @echo
	   @echo "Build finished. The PDF files are in $(BUILDDIR)/pdf.

前節で作成したrst2pdf用スタイルファイルja.jsonをコピーします．

::

  # cp ~/ja.json ~/sphinx/

以下のコマンドで，PDFが作成されます．

::

  # make pdf

このやり方で作ったPDF文書のサンプル( `rst2pdf版PDF <http://dl.dropbox.com/u/1312957/sphinx/rstmemo/pdf/Sphinxmemo-rst2pdf.pdf>`_ ）です．

LaTeXを生成する
~~~~~~~~~~~~~~~
docutilsを修正します．

::

   emacs /usr/lib/python2.6/site-packages/docutils-0.8-py2.6.egg/docutils/writers/latex2e/__init__.py &


361行目を次の通り変更します．

::

   def __init__(self, language_code, reporter = None):

414行目以降を次の通り変更します．

::

    def get_language(self, language_code = None):
        """Return TeX language name for `language_code`"""
        if language_code == None:
            language_code = self.language_code

latexの生成

::

  make latex


これで，LaTeXファイルが出力されます．なお，実際にplatexにかけるときに現状ではいくつかのエラーが出るので，対処が必要です．

このやり方で作ったPDF文書のサンプル( `LaTeX版PDF <http://dl.dropbox.com/u/1312957/sphinx/rstmemo/pdf/Sphinxmemo-latex.pdf>`_ ）です．

参考にさせて頂いたWebページ
~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Sphinx 1.0 <http://sphinx-users.jp/doc10/>`_
- `Sphinx-Users.jp <http://sphinx-users.jp/doc.html>`_
- `Windowsへのインストール <http://sphinx-users.jp/gettingstarted/install_windows.html#sphinx>`_
- `config.pyのPDF用設定 <http://d.hatena.ne.jp/w650/20100216/1266287625>`_
- `Makefileの修正 <http://d.hatena.ne.jp/MiCHiLU/20091009/1255065687>`_

ToDo
----
  
#. テンプレートをカスタマイズしてみる
#. emacsからmakeできるようにする
