FROM node:20-slim

# 必要最小限のパッケージのみインストール
RUN apt-get update && apt-get install -y \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Voltaのインストール
RUN curl https://get.volta.sh | bash

# 環境変数の設定
ENV VOLTA_HOME="/root/.volta"
ENV PATH="/root/.volta/bin:$PATH"

# ワークスペースディレクトリを作成
WORKDIR /workspace

# タイムゾーンを設定
ENV TZ=Asia/Tokyo

# 依存関係のコピー
COPY package*.json ./

# nodeとnpmのインストール
RUN volta install node@18

# 依存関係のインストール
RUN npm install

# lint関係のインストール
RUN npm i -D eslint@8 eslint-config-airbnb eslint-config-airbnb-base prettier lint-staged husky@8

# gitの初期化
RUN git init

# huskyの初期化
RUN npx husky install

# ソースコードのコピー
COPY . .

# .eslintrc ファイルをコピー (明示的にコピー)
COPY .eslintrc /workspace/

# .husky ディレクトリをコピー
COPY .husky .husky

# .husky/pre-commit に実行権限を付与
RUN chmod +x .husky/pre-commit

# Husky のインストール場所を PATH 環境変数に追加
ENV PATH="./node_modules/.bin:$PATH"

# ポートの公開
EXPOSE 3000

# 起動コマンド
CMD ["npm", "run", "dev"]