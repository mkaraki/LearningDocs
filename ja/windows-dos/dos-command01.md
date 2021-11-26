---
lang: ja
title: Windows/DOSコマンド 基礎
---

## 対象者
- Windowsの基本的な用語（ファイル、フォルダ、ディレクトリなど）を知っている
- マウス・キーボードを利用できる
- Webブラウザを利用できる

## 環境
- [**v86 Virtualizer**](https://copy.sh/v86/), [FreeDOS](https://www.freedos.org/)

## 環境構築

**注意:** v86はWASMを利用している。ChromeなどのChromiumを利用しているブラウザを利用すること。

1. [v86 FreeDOS Demo](https://copy.sh/v86/?profile=freedos)にアクセスする
1. (必要に応じて) `Load State`ボタンから保存した環境を呼び出す

## データを引き継ぐ
1. `Save State`ボタンを押す
1. データを保存する（9MB近いデータが保存される）
1. [環境構築](#環境構築)セクションの`2.`を参考にして呼び出す\

## この資料の書式について
この資料では、コマンドの前に`> `を付ける。
これは、コンソールに打ち込んだ値と、予測される実行結果を明示的に区別できるようにするためである。

資料の指定環境はMSDOSであるため、コマンドをすべて大文字で記述している。
これは各自小文字で入力しても構わない。

また、Windows/DOSのファイルシステムではファイル名（フォルダ名）に大文字と小文字の区別はない。
そのため、ファイル名も小文字で記述しても構わない。

## HELLO, WORLD!
コンソールに`HELLO, WORLD!`を出力するコマンドを打つ。

```cmd
> ECHO HELLO, WORLD!
HELLO, WORLD!
```

### 解説
`ECHO`コマンドはヘルプによれば下記の効果を持つ。
```
Displays messages, or turns command-echoing on or off.

  ECHO [ON | OFF]
  ECHO [message]

Type ECHO without parameters to display the current echo setting.
```

今回は`Displays messages`の機能（利用例の2行目）を利用し、`HELLO, WORLD!`を出力した。

### 問題
コンソールに`HELLO, FreeDOS!`と出力するコマンドを作れ。

## フォルダの中身を取得する
フォルダの中身を取得する際は`DIR`コマンドを利用する。

```cmd
> DIR
 Volume in drive A is FREEDOS.
 Volume Serial Number is E4C9-5CE8

 Directory of A:\

COMMAND  COM        66,090  12-10-03  7:49a
<-- 省略 -->
FOO                     10  10-25-12  8:38p
        18 File(s)        401,541 bytes
         3 Dir(s)          46,080 bytes free
```
おそらく大量のファイルが出力され、先頭が見えなかったと思われる。
その際には、`/P`オプションを利用する。

```cmd
> DIR /P
 Volume in drive A is FREEDOS.
 Volume Serial Number is E4C9-5CE8

 Directory of A:\

COMMAND  COM        66,090  12-10-03  7:49a
<-- 省略 -->
CLOCK    COM         8,135  10-25-12  7:07a
Press any key to continue . . .
```
このように1画面で収まらない場合は`Press any key to continue . . .`が表示されるようになる。
これが表示された際に`Enter`などのキーを押すことで次の画面が見れるようになる。

しかし、ファイルサイズや更新日を確認しない場合、縦に表示されても見ずらい場合がある。
その場合は、`/W`オプションを利用する。

```cmd
> DIR /W
 Volume in drive A is FREEDOS.
 Volume Serial Number is E4C9-5CE8

 Directory of A:\

COMMAND.COM   AUTOEXEC.BAT   <省略>   FOO
        18 File(s)        401,541 bytes
         3 Dir(s)          46,080 bytes free
```

`/P`や`/W`は`DIR/P`のようにスペースを短縮して打つことも可能である。

## 特定のフォルダの中身を取得する
基本は[前回のセクション](#フォルダの中身を取得する)と同じである。
変更点はフォルダのパス（場所）を指定するところにある。

```cmd
> DIR /W A:\FDOS
 Volume in drive A is FREEDOS.
 Volume Serial Number is E4C9-5CE8

 Directory of A:\FDOS

[.]           [..]           ATTRIB.COM      <省略>
        4 File(s)         91,116 bytes
        2 Dir(s)          46,080 bytes free
```

毎回`A:\FDOS`のような完全なフォルダの場所（フルパス、完全パス）を指定してもよいが、
現在のフォルダ（カレントディレクトリ）からの相対的な場所（相対パス）を確認してもよい。

```cmd
A:\> DIR /W FDOS
 Volume in drive A is FREEDOS.
 Volume Serial Number is E4C9-5CE8

 Directory of A:\FDOS

[.]           [..]           ATTRIB.COM      <省略>
        4 File(s)         91,116 bytes
        2 Dir(s)          46,080 bytes free
```

プロンプト（`>`）の前に`A:\`があったのがお分かり頂けるであろうか。
これまではカレントディレクトリを考える必要がなかったので省略していたが、これは現在のディレクトリを表す。

この場合は、`A:\`の中にあるフォルダやファイルはフルパスを指定しなくてもファイル名やフォルダ名を入力するだけで良い。

## ファイルの中身を閲覧する
事前準備として、下記のコマンドを実行すること。
```cmd
> ECHO TESTING123.. > TEST.TXT
```

ファイルの中身を表示する際は`TYPE`コマンドを利用する。
今回は、`TEST.TXT`というファイルの中身を表示する。
```cmd
> TYPE TEST.TXT
TESTING123..

```

## フォルダを作る
フォルダを作る際は`MKDIR`もしくは`MD`コマンドを利用する。
この例では、`DIR1`フォルダを作る。
```cmd
> MKDIR DIR1
```

## フォルダを削除する
`RMDIR`もしくは`RD`コマンドを利用する。
この例では、`DIR1`フォルダを削除する。
```cmd
> RMDIR DIR1
```

**注意:** フォルダの中身が空である必要がある。

**情報:** フォルダに中身がある状態での削除は[Windowsコマンド 基礎](windows-command01.md#中身が存在するフォルダを削除する)で取り扱う。

## ファイルを削除する
`DEL`コマンドを利用する。
例では`HELLO.TXT`を削除している
```cmd
> DEL HELLO.TXT
one file removed.
```

## ファイル、フォルダの名前を変更
`RENAME`コマンドもしくは`REN`コマンドを利用する。
例では`FILE1.TXT`を`FILE2.TXT`に変更する。
```cmd
> RENAME FILE1.TXT FILE2.TXT
```

## ファイル、フォルダを移動する
**情報:** v86のFreeDOS Demoには`MOVE`コマンドが実装されていない。
読むだけに留めるか、ローカルのWindows/DOSマシンで実行することで演習を行ってほしい。

`MOVE`コマンドを利用する。
例では、`A:\FILE.TXT`を`A:\DATAS\FILE.TXT`に移動している
```cmd
> MOVE A:\FILE.TXT A:\DATAS\FILE.TXT
```

## ファイルをコピーする
ファイルをコピーするコマンドは2つあるが、単純なコピーであれば`COPY`コマンドで差し支えない。
例では、`A:\DATA1.TXT`を`A:\DATA2.TXT`にコピーしている。
```cmd
> COPY A:\DATA1.TXT A:\DATA2.TXT
A:\DATA1.TXT => A:\DATA2.TXT
```

もしデータが正常にコピーできているか確認したい場合、`/V`オプションを付与する。
```cmd
> COPY A:\DATA1.TXT A:\DATA2.TXT /V
A:\DATA1.TXT => A:\DATA2.TXT
```

## フォルダをコピーする
フォルダをコピーする場合は、`XCOPY`コマンドに`/E`オプションを（必要に応じて`/H`オプションも）指定する。
例では、`A:\DIR1`のコピーである`A:\DIR2`を作っている。
```cmd
> MKDIR A:\DIR2
> XCOPY A:\DIR1 A:\DIR2 /E /H
```

`mkdir A:\DIR2`をスキップすることも可能である。
その場合は質問に`d`と答える必要がある。

`/H`は隠しオプションをコピーするオプションである。

## コマンドの実行結果を保存する
コマンドの実行結果を保存する方法として、リダイレクトが存在する。

リダイレクトでは、`>`記号をコマンドの後に入力し、そのあとにファイルを指定する。
今回の場合は、`ECHO A:\`の結果を`ADRIVE.TXT`に保存する。
```cmd
> ECHO A:\ > ADRIVE.TXT
```

`>`句を使ったリダイレクトでは、すでに存在するファイルの場合内容が消える。
`>>`を利用することで、追記が可能になる。
```cmd
> ECHO A:\FDOS >> ADRIVE.TXT
```