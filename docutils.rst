.. include:: replace.rst

docutilsを使った文書作成
========================

gnupack環境をインストールと設定
-------------------------------

簡単にcygwin環境とemacs等をインストールできるパッケージ，grupack [#f1]_ をインストールします．
ここでは，ユーザのホームディレクトリ（ |user home| ） [#f2]_ にインストールします．

#. `gnupack-basic-7.00.exe`_ をダウンロードします
#. ダブルクリックして実行します
#. "解凍先"に |user home| を指定します

新たに， |gnupack| ディレクトリができます．
その下にファイルが展開されていますので，確認してください．

.. _gnupack: http://gnupack.sourceforge.jp/docs/latest/UsersGuide.html
.. _gnupack-basic-7.00.exe: http://sourceforge.jp/projects/gnupack/downloads/52709/gnupack_basic-7.00.exe/

.. [#f1] gnupackにはbasic版とdevelop版があります．
   develop版のgccは今回利用しないので，basic版をインストールしてください．
.. [#f2] \\ は「￥」記号に読み替えてください．
   *<name>* の部分は，あなたのログイン名に置き換えてください.

cygwin用パッケージ管理ツール
----------------------------

cygwinにパッケージを追加するために， setup.exeをダウンロードします．

#. `setup.exe`_ をダウンロードします．
#. ダウンロードしたファイルを |gnupack| ディレクトリにコピーしてください．
#. また，同じ場所に"package"という名前でフォルダを作成してください．

.. _setup.exe:  http://cygwin.com/setup.exe

setup.exeの起動とディレクトリの指定
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. setup.exeを実行します．
#. "次へ"でページをめくり，"Cygwin Setup - Choose Installation Directory"画面に進みます．
#. "Root Directory"に |cygwin| を指定してください．
#. "次へ"でページをめくり，"Cygwin Setup - Select Local Package Directory"画面に進みます．
#. "Local Package Directory"に |cygwin package| を指定してください．
#. "次へ"でページをめくり，"Cygwin Setup - Choose Download Site(s)"画面に進みます．
#. "ftp://ftp.iij.ad.jp"を選択してください

パッケージの選択
~~~~~~~~~~~~~~~~
まず，次のパッケージを追加します．

- Python
- curl

#. "次へ"でページをめくり，"Cygwin Setup - Select Packages"画面に進みます．
#. "Search"に"python"と入力してください（画面が更新されるまでに若干ラグがあります）．
#. "All:Interpreters"の中にある"python: Python language interpreter"の行にある"Skip"をクリックします（表示がバージョン番号に変わります）．
#. "Search"に"curl"と入力してください．
#. "All:Net"の中にある"curl: Multi-protocol file transfer command-line tool"の行にある"Skip"をクリックします（表示がバージョン番号に変わります）．

パッケージのダウンロードとインストール
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. "次へ"でページをめくり，"Cygwin Setup"画面に進みます．
#. ダウンロードが終了すると，"Cygwin Setup - Installation Status and CReate Icons"画面がでます．
#. "Crate icon on Desktop"のチェックは外して，"完了"を押してください．

python用パッケージ管理ツール
----------------------------

#. |mintty| を起動して，コマンドプロンプトを表示させます．
#. 次のコマンドを実行してください．
#. python ez_setup.pyでエラーが出る場合は、C:\Users\*<name>*\gnupack_basic-7.00\homeにez_setup.pyを保存してください。 （ブラウザでhttp://peak.telecommunity.com/dist/ez_setup.pyを開き、保存する）

::

  # curl -O http://peak.telecommunity.com/dist/ez_setup.py
  # python ez_setup.py

docutilsのインストール
----------------------

- rst2pdfはdocutilsをベースに作られています．
- http://docutils.sourceforge.net/docs/user/tools.html

::

  # easy_install docutils

docutilsのテスト
----------------

テスト用rstの作成
~~~~~~~~~~~~~~~~~

emacsを起動します．

::

  # emacs test.rst &

次の通り入力します．

::

  タイトル
  ========

  - ぐー
  - ちょき
  - ぱー

rst2htmlの実行
~~~~~~~~~~~~~~

::
   
# rst2html.py test.rst > test.html


htmlの表示
~~~~~~~~~~
結果

::

 <?xml version="1.0" encoding="utf-8" ?>
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <meta name="generator" content="Docutils 0.8: http://docutils.sourceforge.net/" />
 <title>タイトル</title>
 <style type="text/css">
 ...省略...
 </style>
 </head>
 <body>
 <div class="document" id="id1">
 <h1 class="title">タイトル</h1>

 <ul class="simple">
 <li>ぐー</li>
 <li>ちょき</li>
 <li>ぱー</li>
 </ul>
 </div>
 </body>
 </html>


任意のブラウザでtest.htmlを開き，内容を確認してください．

その他の文書生成
----------------

LaTeXの生成
~~~~~~~~~~~
platexがインストールされている場合，以下のコマンドを入力することでLaTeXのソースファイルが生成され，コンパイルできます．

::

  # rst2latex.py hoge.rst
  # platex -kanji=utf8 hoge.tex

S5スライドの生成
~~~~~~~~~~~~~~~~
- http://meyerweb.com/eric/tools/s5/
- http://meyerweb.com/eric/tools/s5/primer.html

OpenOffice Writer形式ファイルの生成
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Writer形式で出力することもできます．日本語が乱れますので，使い物にはならないかも．

::

  # rst2odt.py hoge.rst > hoge.odt
