FROM node:20-slim

# 必要最小限のパッケージのみインストール
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# ワークスペースディレクトリを作成
WORKDIR /workspace

# タイムゾーンを設定
ENV TZ=Asia/Tokyo

# package.jsonを生成
RUN npm init -y

# package.jsonとpackage-lock.jsonをコピー
COPY package*.json ./

# 依存関係のインストール
RUN npm install

# キャッシュのクリア
RUN npx --yes rimraf node_modules/.cache

# TypeScriptのグローバルインストール
RUN npm install -g typescript

# TypeScriptの設定ファイルの初期化
RUN tsc --init