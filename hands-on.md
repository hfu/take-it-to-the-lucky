# ベクトルタイルハンズオン 2018
## 構成
1. Preparation
2. Vector tile production with Node.js and tippecanoe
3. Vector tile hosting and consumption with tile-block.js

## 1. Preparation
### Recommended software
他の選択も可能であるが、ハンズオンの単純さのためにこれをお勧めしている、というソフトウェア
#### Linux 
ubuntu を recommended とする。適宜用意してほしいという説明ぶりとする。Windows で困っている人に対しては、Virtualbox で導入することをお勧めする。

#### Chrome
Chrome Secure Shell extension が使えることから、Chrome を推奨する。端末エミュレータとしても、ウェブブラウザとしても使用する。

### Essential software
#### tippecanoe
ソースからビルドすることを推奨する。つまり、ビルドツールが必要だということだ。
https://github.com/mapbox/tippecanoe

#### Node.js
あまりシンプルなアプローチになってはいないが、[Node.js の公式の案内](https://nodejs.org/ja/download/package-manager/#debian-and-ubuntu-based-linux-distributions-debian-ubuntu-linux)に導くのだと思う。

なお、私自身は、下記のような感じにして n を導入している。
```
npm install -y nodejs
npm cache clean
npm install -g n
npm cache clean
n stable
ln -sf /usr/local/bin/node /usr/bin/node
apt-get -y purge npm nodejs
```

#### git
Linux に普通に入っているものとして、詳しい説明は省略する。

## 2. Vector tile production with Node.js and tippecanoe
PostGIS からデータを取り出して GeoJSON にするとともに tippecanoe 属性を付与し、tippecanoe で変換して mbtiles を得る。tileserver-gl でデータができていることを確認する。

### node の動作確認
```bash
$ node -v
v9.9.0
```

### tileserver-gl-light の動作確認
```bash
$ tileserver-gl-light -v
tileserver-gl-light v2.3.1
```

### tippecanoe の動作確認
```bash
$ tippecanoe -v
tippecanoe v1.27.16
```

### git を使って pnd.js を clone する
```bash
$ git clone git@github.com:hfu/pnd.git
Initialized empty Git repository in /home/fhidenori/pnd/.git/
remote: Counting objects: 52, done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 52 (delta 29), reused 35 (delta 14), pack-reused 0
Receiving objects: 100% (52/52), 21.06 KiB, done.
Resolving deltas: 100% (29/29), done.
```

### npm モジュールをインストールする
```bash
$ cd pnd
$ npm install
added 166 packages from 81 contributors in 5.574s
```

## 3. Vector tile hosting and consumption with tile-block.js
