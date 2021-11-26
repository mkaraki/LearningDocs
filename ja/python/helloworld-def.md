---
lang: ja
title: Hello World、関数定義
---

## 対象者
- マウス・キーボードを利用できる
- Webブラウザを利用できる

## 環境
[Google](https://about.google/)が提供する[Google Colaboratory](https://colab.research.google.com/)を利用する。

[Google Colaboratory](https://colab.research.google.com/)を開くとファイルを開くダイアログが表示される。
一度キャンセルをクリックし、Google colaboratoryとJupitor Notebookの簡単な使い方を理解した上で実習に移ることを推奨する。

Googleの提供している[YouTubeのチュートリアル動画](https://youtu.be/inN8seMm7UI)も参考になる。
字幕で日本語対応されているので参照されることを推奨する。

## `Hello, World!`

Wikipediaによれば、`Hello World`の定義は下記の通りである。

> Hello world（ハロー・ワールド）は、画面に「Hello, world!」やそれに類する文字列を表示するプログラムの通称である。多くのプログラミング言語において非常に単純なプログラムであり、プログラミング言語の入門書で、プログラムを動かすためのプログラミング言語の基本文法の解説例として提示される。
> 
> -- Source: [Hello World - Wikipedia](https://ja.wikipedia.org/w/index.php?title=Hello_world&oldid=85444747)

Pythonでの`Hello World`は下記のようなコードになる。

```python
print("Hello, World!")
```

[公式ドキュメント](https://docs.python.org/ja/3/library/functions.html#print)によれば、
`print`は文字列を特定の場所に出力する関数である。
指定なき場合、標準出力（コンソール）に出力される。

そのため、`print`に`Hello, World!`という文字列を与えることにより、
コンソールに`Hello, World!`が出力されたということになる。

`"`で囲まれた文字列をPythonは文字列として扱う。
それ以外の文字列は命令や変数名として扱う。

## 関数の定義
Pythonでは命令の集まりをひとくくりに関数という形にまとめることができる。

これには`def`を利用する。

```python
def helloworld():
    print("Hello, World!")
```

`def`の書式は下記のとおりである

```python
def 関数名([引数 [, ...]]):
    命令
    [...]
```

注意点として、Pythonでは`タブ文字`と`スペース`で入れ子関係を表す。
そのため、関数の命令はすべて、タブなどでインデントされていなければならない。

また、インデントは同じレベルでなければならない。

## 関数の呼び出し

関数の呼び出しは、標準ライブラリを呼び出すのと同様に呼び出せる。

```python
helloworld()
```

これを実行すると、

```
Hello, World!
```

が出力される。