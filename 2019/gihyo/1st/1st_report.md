# PyCon JPとは

@ksugaharaが書きます

# 1日目基調講演

@ussy

![写真タイトル](./_static/hogehuga.jpg)

### 資料リンク

* [動画]()
* [スライド]()


# トークセッション（1）

@ussy

![写真タイトル](./_static/hogehuga.jpg)

### 資料リンク

* [動画]()
* [スライド]()

# トークセッション（2）

@ussy

![写真タイトル](./_static/hogehuga.jpg)

### 資料リンク

* [動画]()
* [スライド]()

# トークセッション（3）

@HiraoMotoki

![写真タイトル](./_static/hogehuga.jpg)

### 資料リンク

* [動画]()
* [スライド]()


# 1日目注目セッション「Yet Another Isolation - Debian Packageと紐づく環境分離」 ー 末田卓巳 (Takumi SUEDA)

（nikkie）

末田卓巳氏による「Yet Another Isolation - Debian Packageと紐づく環境分離」をレポートします。

末田氏は GROOVE X 株式会社にてLOVOT（ラボット）の開発に携わっています。
LOVOTにはDebian Linuxが2台入っており、LOVOTにデプロイするソフトウェアはDebianパッケージにしてAPTでインストールしているそうです。
Python製のソフトウェアをAPTでインストールする際に、依存するPythonパッケージをどう扱うか、実務で培った知見を共有するトークでした。

まずは既存の方法についての共有がありました。
Pythonの環境分離方法にはvenvがあります。
フックを使うと、Debianパッケージのインストール・アンインストール時にスクリプトを実行できるため、インストール時にvenvを作るスクリプトを試したそうです。
venvで満たせた要件もありましたが、「システムの中のどこに、いくつ、誰がvenvを作ったのかはわからない」ことが懸念されました。
他のツールとして、pyenvでも懸念事項が残ったため、末田氏は環境分離ツールを作成することにしました。

早速作るのではなく、実現手法とコマンドの形式を整理します。

- 分離された環境を作る`create`コマンド
- 分離された環境を一覧表示する`list`コマンド
- 指定した環境を削除する`purge`コマンド
- 指定した環境でコマンドを実行する`run`コマンド
- 指定した環境の中の実行ファイルのパスを表示する`which`コマンド

いよいよ実装です。
その中の1つ`run`コマンドの実装方法について、ここで取り上げます。
標準モジュール`subprocess`の`run`メソッドを使うと、Pythonの子プロセスとして別のプログラムを実行できます。
一方、シバン（Shebang）で使われる`env`コマンドから別のプログラムを実行した場合、`env`コマンドはプロセスツリーから消えます。
末田氏は`env`コマンドに倣った挙動としたかったため、標準モジュール`os`の`execv`メソッドを使って実装しました。
`os.execv`を使うとプロセスツリーからPythonが消えることは、対話モードでPythonを立ち上げて確認できます。

```shell
$ python3  # macOS 10.14.4で検証
Python 3.7.3 (v3.7.3:ef4ec6ed12, Mar 25 2019, 16:52:21)
>>> import os
>>> os.execv('/usr/bin/vim', ['vim'])  # vimを起動
# vimが起動する。:qで終了する
$ # 対話モードではなく、シェルに戻る（vimはPythonの子プロセスとして起動されていなかった）
```

本発表は自作した環境分離ツールについての発表でしたが、Pythonでほしいツールを自作する際の方法も学べるトークだったと考えています。
スライドは見やすく、話もうまく、1つの手本と感じたトークでした。

![冒頭、LOVOTの構成について紹介する末田氏](./_static/suedashi_lovot.jpg)

### 資料リンク

* [動画](https://www.youtube.com/watch?v=e9MKpn8bqx4)
* [スライド](https://speakerdeck.com/puhitaku/yet-another-isolation-debian-packagetoniu-dukuhuan-jing-fen-li)
* 取り上げられた環境分離ツールgxenv [PyPI](https://pypi.org/project/gxenv/)、[GitHub](https://github.com/groove-x/gxenv)

# 1日目ライトニングトーク

説明 @ksugahara

## 1つ目タイトル

@ussy

![写真タイトル](./_static/hogehuga.jpg)


## 2つ目タイトル

@nikkie

![写真タイトル](./_static/hogehuga.jpg)


## 1日目ライトニングトーク一覧

@ussy

今回ご紹介しきれなかったものも含め、1日目のライトニングトークの一覧はこちらです。また、Pythonの公式アカウントに[ライトニングトークの動画]()がアップロードされています。



# 次回は

@nikkie

1日目のカンファレンスレポートは以上です。今回紹介できなかったセッションも多数あるのですが、それらは下記のリンクから見ることができます。みなさまの気になるセッションやトークは見つかりましたか？

* [Youtube PyCon JP公式アカウント](https://www.youtube.com/channel/UCxNoKygeZIE1AwZ_NdUCkhQ)

2日目のレポートも後日、公開しますので楽しみにしてください！