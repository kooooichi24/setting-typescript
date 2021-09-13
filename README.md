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
