# TypeScript 環境の構築方法 (自動コンパイルまで)

## 目的

TypeScript 環境を構築するために必要な知識や手順を把握すること。

## 前提

- MacOS

## 手順

### 1. anyenv と nodenv を利用して、Node.js インストール

#### anyenv

```bash
# anyenvのインストール
brew install anyenv

# 初期化
anyenv init

# ~/.zshrcに設定追記 (anyenv init 結果に記載)
echo 'eval "$(anyenv init -)"' >> ~/.zshrc

# マニュフェストディレクトリ作成
anyenv install --init

# 設定の確認 (エラー発生しなければOK)
source ~/.zshrc
```

#### nodenv

```bash
# anyenvでnodenvをインストール
anyenv install nodenv

# プロファイルリロード
exec $SHELL -l

# 設定の確認(NODENV_ROOTやNODENV_SHELLが存在すればOK)
env
```

#### Node.js

```bash
# インストール可能バージョンを確認
nodenv install -l

# インストール
nodenv install {バージョン番号}

# プロジェクト毎にNodeバージョンを指定
cd {プロジェクトのパス}
nodenv local {バージョン番号}

# プロジェクト毎のNodeのバージョンの確認
nodenv local
```

### 2. Node.js & TypeScript のプロジェクト作成

#### package.json をセットアップする

```bash
npm init -y
# もしくは yarn init -y
```

#### TypeScript をインストールする

```bash
npm install typescript --save-dev
# もしくは yarn add -D typescript
```

#### Node.js の型宣言ファイル`node.d.ts`をインストール

```bash
npm install @types/node --save-dev
# yarn add -D @types/node
```

#### TypeScript の設定ファイル`tsconfig.json`を初期化する

```bash
npx tsc --init --rootDir src --outDir dist --esModuleInterop --resolveJsonModule --lib es6,dom --module commonjs
```

各オプションの詳細は`tsconfig.json`のコメントアウトを確認してください

### 自動コンパイルと実行

#### インストール

- ts-node
  - TypeScript をコンパイルし、Node.js で実行するため
- nodemon
  - ファイル変更されるたびに ts-node を再起動するため

```bash
npm install ts-node --save-dev
npm install nodemon --save-dev
# yarn add -D ts-node
# yarn add -D nodemon
```

#### package.json に script を定義する

```js
"scripts": {
  "start": "npm run build:live",
  "build": "tsc -p .",
  "build:live": "nodemon --watch 'src/**/*.ts' --exec 'ts-node' src/index.ts"
},
```

### 実行

```bash
npm run build:live
# yarn build:live
```
