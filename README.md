# typescript 4.5.5
TypeScriptのバージョン4.5.5の学習用に作ります。

## 前提条件
- MacOS / Windows環境
- Gitコマンド
- Docker for Desktop

## ミドルウェア
- Node 12.x.x
- Typescript 4.5.5

## ファイル構成
```
┗ src
  ┣ dist           ← トランスパイルされたファイル
  ┣ node_modules   ← npm installでインストールされるライブラリ
  ┣ src            ← Typescriptのコード
  ┣ package.json
  ┣ package-lock.json
  ┗ tsconfig.json
```

## 準備
必要となるコードをリポジトリからclonseして配置します。
```bash
$ mkdir -p ~/workspace/typescript4.5.5/ && cd ~/workspace/typescript4.5.5
$ git clone https://github.com/reflet/typescript4.4.5.git .
```

## docker構築
dockerイメージを作成し、バージョン確認してみる。

```bash
# dockerイメージ作成
$ docker compose build

$ docker compose run --rm node npx tsc --version
Version 4.5.5
```

## サーバ起動
dockerコンテナを起動します。
```bash
$ docker compose up -d
```

## トランスパイル
Typescriptのコードをjsファイルに変換します。
```bash
$ docker compose exec node npx tsc
```

## プログラム実行
jsファイルを実行してみる。
```bash
$ docker compose exec node node ./dist/index.js
Hello, Typescript.
```

## プロジェクト作成
新規にプロジェクトを作成する場合は、下記コマンドで、各設定ファイルを作成ください。

＜各設定ファイル＞
```
┗ src
  ┣ package.json
  ┣ package-lock.json
  ┗ tsconfig.json
```
下記コマンドを実行することで、上記３つのファイルが作成されます。

### ① 初期化(npm)
`src/package.json` を作成します

```bash
$ docker compose run --rm node npm init -y
```

### ② ライブラリをインストールする
`src/package-lock.json` と `src/node_modules` が作成されます。

```bash
$ docker compose run --rm node npm install -D typescript@4.5.5
```

### ③ 初期化 (TypeScript)
TypeScriptの `src/tsconfig.json` ファイルを作成します。

```bash
$ docker compose run --rm node npx tsc --init
```


## 参考サイト
* [ゼロからわかるTypeScript入門](https://gihyo.jp/book/2022/978-4-297-12635-3)

以上
