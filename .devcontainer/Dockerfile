# ビルドステージ
FROM node:20-slim AS builder

# git と curl のインストール
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
WORKDIR /playground

# タイムゾーンを設定
ENV TZ=Asia/Tokyo

# gitの初期化
RUN git init

# 依存関係のコピー
COPY package*.json ./

# nodeとnpmのインストール
RUN volta install node@18

# yarnのインストール
RUN npm install -g yarn

# 依存関係のインストール
RUN yarn install

# lint関係のインストール
RUN yarn add -D eslint@8 eslint-config-airbnb eslint-config-airbnb-base prettier

# typescript
ENV PATH="./node_modules/.bin:$PATH"
RUN yarn add typescript --dev
RUN yarn install
RUN yarn tsc --init

# # create-react-appのインストール
# RUN yarn global add create-react-app

# ソースコードのコピー
COPY . .

# .eslintrc ファイルをコピー (明示的にコピー)
COPY .eslintrc /playground/

# 非特権ユーザーの作成
RUN adduser --disabled-password --gecos "" devuser

# ワークスペースディレクトリの所有者を変更
RUN chown -R devuser:devuser /playground

# .gitディレクトリの所有者を変更
RUN chown -R devuser:devuser /playground/.git

# ランタイムステージ
FROM node:20-slim

# 必要最小限のパッケージのみインストール
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# ワークスペースディレクトリを作成
WORKDIR /playground

# タイムゾーンを設定
ENV TZ=Asia/Tokyo
ENV PUBLIC_URL=./React/public

# ランタイムステージに必要なファイルのみコピー
COPY --from=builder /playground /playground

# ランタイムステージでdevuserを作成
RUN adduser --disabled-password --gecos "" devuser

# ワークスペースディレクトリの所有者を変更
RUN chown -R devuser:devuser /playground

# .gitディレクトリの所有者を変更
RUN chown -R devuser:devuser /playground/.git

# ユーザーを切り替え
USER devuser

# ポートの公開
EXPOSE 3000

# 起動コマンド
CMD ["yarn", "start"]