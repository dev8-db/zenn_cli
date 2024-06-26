---
title: "ベクター画像とラスター画像の違い"
emoji: "🥪"
type: "tech"
topics: [homebrew]
published: true
---

## ベクター画像とラスター画像とは
画像にはベクター画像とラスター画像という2つのタイプがあります。

### ベクター画像
数学の式で描かれた図形。拡大してもボケず、きれい。
![](https://storage.googleapis.com/zenn-user-upload/9c85ff4ede6f-20240416.png)
- #### SVG (Scalable Vector Graphics)
Webページや印刷物でよく使われる。拡大しても画質が劣化しない。

- #### AI (Adobe Illustrator)
Adobe Illustratorの図形データ形式で、本格的なデザインに使われる。

---

### ラスター画像
小さなドット（ピクセル）の集まりで構成され、拡大するとドットが目立つ。
![](https://storage.googleapis.com/zenn-user-upload/402d4122f1db-20240416.png)
- #### JPEG (Joint Photographic Experts Group)
ウェブ上でよく使われ、写真やイメージに最適。
:::details JPEGの仕組み
JPEGでは以下の方法で画像の情報を削減しています。

1. #### 色情報の削減
人間の目は微細な色の変化をあまり感じ取らないので、近い色をまとめて1つにします。

2. #### 空間の分割
- 画像を8x8ピクセルのブロックに分割します。
- 各ブロックには、色情報を表す値が入っています。
- この値を数学的手法（離散コサイン変換）を使って変換します。

$$
F(u, v) = (1/4)*C(u)*C(v)*sum_{x=0}^{7}sum_{y=0}^{7}f(x, y)*cos[(2x+1)u*pi/16]*cos[(2y+1)v*pi/16]
$$

3. #### 量子化
- 変換された値を量子化します。つまり、整数の形に変換して情報を削減します。

$$
F'(u, v) = round[F(u, v)/Q(u, v)]
$$

4. #### 圧縮
- 量子化された値を使って画像を圧縮します。
- 具体的には、以下の手順で圧縮が行われます。
  - ハフマン符号化
  - 差分符号化

5. #### こちらの方が分かりやすいです
JPEG画像の仕様は以下のラムダさんの動画にて分かりやすく解説されています。
https://www.youtube.com/watch?v=vzuv4rP6jpY
:::
- #### PNG (Portable Network Graphics)
透明な背景を持つ画像に適しており、Webで広く使用される。

- #### GIF (Graphics Interchange Format)
アニメーション画像に使われ、シンプルなイラストやアイコンにも。

## どちらを使うべきか
ベクター画像とラスター画像、どちらを使うかは、使いたい目的やプロジェクトの性質によります。

#### ベクター画像を使うべき場合:
- ロゴやアイコンなどの図形がシャープでクリアに見える必要がある場合。
- プリント物や看板、ウェブページのレスポンシブデザインに適している。
- サイズが変わる可能性があるデザインを作成する際に便利。

#### ラスター画像を使うべき場合:
- 写真や画像が必要な場合。
- グラデーションや微細な色の変化があるデザインを作成する場合。
- ソーシャルメディア用の画像やウェブサイトの背景画像など、固定サイズのものを作成する際。

ベクター画像はサイズが変わってもクリアに見え、拡大・縮小が自由自在。一方、ラスター画像は写真や細かいディテールを表現するのに向いています。プロジェクトの要件に合わせて使い分けましょう。

## 画像タイプの変換
ベクター画像とラスター画像の変換を簡単にし、用途によって使い分けましょう。

### ベクター画像からラスター画像に変換
それぞれのOSに対応した手順でImageMagickをインストールし以下`のコマンドを実行してください。
```
convert 入力ファイル名.svg 出力ファイル名.jpeg
```

#### Windows
1. [ImageMagickのダウンロードページ](https://imagemagick.org/script/download.php)からインストーラーをダウンロードします。
2. ダウンロードしたインストーラーを実行し、指示に従ってインストールします。

#### macOS
1. Homebrewをインストールします。既にインストールできている場合は必要ないです。
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
2. ターミナルを開いて、以下のコマンドを実行します。
```
brew install imagemagick
```

#### Linux（Ubuntuなど）
1. ターミナルを開いて、以下のコマンドを実行します。
```
sudo apt-get update
sudo apt-get install imagemagick
```

#### 変換された画像
しっかりドットに変換されました。
やっていて楽しくなってきました。しっかりJPEG仕様のノイズが入っています。
![](https://storage.googleapis.com/zenn-user-upload/d897cc3e4a88-20240417.jpeg)
https://twitter.com/dev8_db/status/1780251141496049948

---

### ラスター画像からベクター画像に変換
- #### Vectorizer.com
ログインも必要なく無料で1度に20枚も変換できるので便利です。多分無制限だと思います。
https://vectorizer.com/

- #### Vectorizer.AI
UIがシンプルで使いやすいですが有料です。
https://vectorizer.ai/