.. include:: replace.rst

PDFを作成する
=============

rst2pdfのインストール
---------------------

パッケージの選択
~~~~~~~~~~~~~~~~
setup.exeを起動して次のパッケージインストールしてください．．

#. "All:Devel"の中にある"gcc: C compiler upgrade helper"
#. "All:Graphics"にある"jpeg: A library for manipulating JPEG image format files"
#. "All:Graphics"にある"lcms: Little color management engine - (Python bindings)"
#. "All:X11"にある"freetype2: High-quality software font engine (runtime library)"

pythonパッケージの追加
~~~~~~~~~~~~~~~~~~~~~~
|mintty| を起動して，コマンドプロンプトを表示させます．
次のコマンドを実行してください．

::

  # easy_install PIL
  # easy_install reportlab
  # easy_install rst2pdf

コンパイルエラーへの対処
~~~~~~~~~~~~~~~~~~~~~~~~

コンパイル中に以下のエラーになる場合があります．

::

  *** fatal error - unable to remap \\?\C:\Users\<name>\gnupack_basic-7.00\app\cygwin\cygwin\lib\python2.6\lib-dynload\time.dll to same address as parent: 0x3D0000 != 0x3F0000
  Stack trace:
  Frame     Function  Args
  00224DF8  6102796B  (00224DF8, 00000000, 00000000, 00000000)
  002250E8  6102796B  (6117EC60, 00008000, 00000000, 61180977)
  00226118  61004F1B  (611A7FAC, 612483E4, 003D0000, 003F0000)
  End of stack trace
  1 [main] python 6956 fork: child 7068 - died waiting for dll loading, errno 11
  error: Setup script exited with error: Resource temporarily unavailable

その場合， 一旦すべてのプロセス（シェルや，emacsなど）を終了させます。

次に， |cygwin| の下にある\\bin\\ash.exeを起動して，次のコマンドを入力します．

::

  $ /bin/rebaseall
  $ exit

完了したら，もう一度easy_installを使ってパッケージを追加します。

フォントの追加
~~~~~~~~~~~~~~
フォントを組み込むために，~/fontsディレクトリをを作成します。

::

   mkdir ~/fonts

`IPAフォント`_ をダウンロードして解凍します。

.. _IPAフォント: http://ossipedia.ipa.go.jp/ipafont/IPAfont00303.php

TrueTypeフォントファイル（ipag.ttf,ipagp.ttf,ipam.ttf,ipamp.ttf）を~/font（ |gnupack| の下の\\home\\fonts）にコピーします。lsコマンドで確認して，次の結果になれば大丈夫です。

::

  # ls ~/fonts
  ipag.ttf  ipagp.ttf  ipam.ttf  ipamp.ttf


スタイルファイルの作成
~~~~~~~~~~~~~~~~~~~~~~
以下の内容を"ja.json"というファイル名で作成し，保存します。

::

   {
     "embeddedFonts" :[[
       "ipag.ttf",
       "ipagp.ttf",
       "ipam.ttf",
       "ipamp.ttf"
     ]],
     "fontsAlias" : {
       "stdFont": "IPAPGothic",
       "stdBold": "IPAPGothic",
       "stdItalic": "IPAPGothic",
       "stdBoldItalic": "IPAPGothic",
       "stdMono": "IPAPGothic",
       "stdMonoBold": "IPAPGothic",
       "stdSanBold": "IPAPGothic",
       "stdSansBold": "IPAPGothic"
     },
     "styles" : [
       ["base" , {
	 "wordWrap": "CJK",
	 "kerning" : true
       }],
       ["literal" , {
	 "wordWrap": "None"
       }]
     ]
   }

docutilsの修正
~~~~~~~~~~~~~~

次の通りエディタでファイルを開きます．

::

  # emacs /usr/lib/python2.6/site-packages/docutils-0.8-py2.6.egg/docutils/languages/__init__.py &


18行目を以下のコードに置き換えます．

::

   def get_language(language_code, reporter = None):

reportlabの修正
~~~~~~~~~~~~~~~

次の通りエディタでファイルを開きます．

::

  # emacs /usr/lib/python2.6/site-packages/reportlab-2.5-py2.6-cygwin-1.7.9-i686.egg/reportlab/platypus/paragraph.py &

335行目を以下のコードに置き換えます．

::

  simple = last or abs(extraSpace)<=1e-8 or getattr(line, 'lineBreak', False)


PDFファイル生成
---------------

以下のコマンドを実行してください

::

  # rst2pdf -s ja --font-path=~/fonts/ rst2pdf.rst

rst2pdf.pdfが作成されれば完了です．

参考にさせて頂いたWebページ
---------------------------

- `rst2pdfのget_languageで発生する問題について <http://d.hatena.ne.jp/shinriyo/20110810>`_
- `rebaseallについて <http://d.hatena.ne.jp/haradats/20080119/p4>`_
- `reportlabの修正について <http://harajuku-tech.posterous.com/rst2pdfpdf>`_
- `Creating presentations using restructured text <http://lateral.netmanagers.com.ar/stories/BBS52.html>`_
