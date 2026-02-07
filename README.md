# 🦜 Generative Deep Learning - 2nd Edition Codebase

O'Reilly の *Generative Deep Learning: Teaching Machines to Paint, Write, Compose and Play*.
の第2版コードベースのフォークです。Apple M4 Maxで動作するように調整しました。

[O'Reilly link](https://www.oreilly.com/library/view/generative-deep-learning/9781098134174/)

[Amazon US link](https://www.amazon.com/Generative-Deep-Learning-Teaching-Machines/dp/1098134184/)

[オライリー・ジャパン](https://www.oreilly.co.jp/books/9784873119917/)

<img src="img/book_cover.png" width="300px">

## 🚀 始め方

### Kaggle API

To download some of the datasets for the book, you will need a Kaggle account and an API token. To use the Kaggle API:
書籍のいくつかのデータセットをダウンロードするには、KaggleアカウントとAPIトークンが必要です。Kaggle APIを使う方法は以下の通りです。

1. [Kaggleアカウント](https://www.kaggle.com)を作成します。
2. ユーザープロフィールの「Account」タブに移動します。
3. 「Create API Token」を選択します。これにより、APIクレデンシャルを含む `kaggle.json` がダウンロードされます。

### .env ファイル

ルートディレクトリに `.env` という名前のファイルを作成し、以下の値を含めます（JSONからKaggleのユーザー名とAPIキーを置き換えます）：

```
JUPYTER_PORT=8888
TENSORBOARD_PORT=6006
KAGGLE_USERNAME=<your_kaggle_username>
KAGGLE_KEY=<your_kaggle_key>
```

### Dockerのセットアップ

コードベースは [Docker](https://docs.docker.com/get-docker/) で動作するように設計されています。

Dockerを使ったことがない場合でも心配いりません！このリポジトリの [Docker README](./docs/docker.md) ファイルにDockerのガイドを含めています。Dockerの素晴らしさと、このプロジェクトの `Dockerfile` と `docker-compose.yml` の簡単なガイドが含まれています。

### Dockerイメージのビルド

Apple M4 MaxではGPU版がうまく動かせなかったのでCPU版で動かします。
以下のコマンドを実行してください。

```
docker compose build
```

### コンテナの実行

以下のコマンドを実行してください。

```
docker compose up
```

Jupyterは、`.env` ファイルで指定したポートでローカルブラウザで利用可能になります。例えば：

```
http://localhost:8888
```

ノートブックは `/notebooks` フォルダに章と例ごとに整理されています。

## 🏞️ データのダウンロード

The codebase comes with an in-built data downloader helper script.
コードベースには組み込みのデータダウンローダーヘルパースクリプトが付属しています。

データダウンロードを以下のように実行します（コンテナの外から）。名前でデータセットが選択できます：

```
bash scripts/download.sh [faces, bricks, recipes, flowers, wines, cellosuites, chorales]
```

## 📈 Tensorboard

Tensorboardは、実験を監視し、モデルのトレーニングがどのように進んでいるかを確認するのに非常に便利です。

Tensorboardを起動するには、以下のスクリプトを実行します（コンテナの外から）：
* `<CHAPTER>` - the required chapter (e.g. `03_vae`)
* `<EXAMPLE>` - the required example (e.g. `02_vae_fashion`)

```
bash scripts/tensorboard.sh <CHAPTER> <EXAMPLE>
```

Tensorboardは `.env` ファイルで指定したポートでローカルブラウザで利用可能になります。例：

```
http://localhost:6006
```

## ☁️ クラウドのバーチャルマシンを使う

Google Cloud PlatformでGPU付きの仮想マシンをセットアップするには、このリポジトリの [Google Cloud README](./docs/googlecloud.md) ファイルの指示に従ってください。

## 📦 他のリソース

この本のサンプルのいくつかは、[Kerasのウェブサイト](https://keras.io/examples/generative/)で利用可能な優れたオープンソースの実装から適応されています。新しいモデルやサンプルが常に追加されているので、チェックしてみてください。


