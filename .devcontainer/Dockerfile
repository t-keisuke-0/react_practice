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
WORKDIR /workspace

# タイムゾーンを設定
ENV TZ=Asia/Tokyo

# gitの初期化
RUN git init

# 依存関係のコピー
COPY package*.json ./

# nodeとnpmのインストール
RUN volta install node@18

# 依存関係のインストール
RUN npm install

# lint関係のインストール
RUN npm i -D eslint@8 eslint-config-airbnb eslint-config-airbnb-base prettier

# typescript
RUN npm install typescript --save-dev && npx tsc --init

# ソースコードのコピー
COPY . .

# .eslintrc ファイルをコピー (明示的にコピー)
COPY .eslintrc /workspace/

# 非特権ユーザーの作成
RUN adduser --disabled-password --gecos "" devuser

# ワークスペースディレクトリの所有者を変更
RUN chown -R devuser:devuser /workspace

# .gitディレクトリの所有者を変更
RUN chown -R devuser:devuser /workspace/.git

# ランタイムステージ
FROM node:20-slim

# 必要最小限のパッケージのみインストール
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# ワークスペースディレクトリを作成
WORKDIR /workspace

# タイムゾーンを設定
ENV TZ=Asia/Tokyo

# ランタイムステージに必要なファイルのみコピー
COPY --from=builder /workspace /workspace

# ランタイムステージでdevuserを作成
RUN adduser --disabled-password --gecos "" devuser

# ワークスペースディレクトリの所有者を変更
RUN chown -R devuser:devuser /workspace

# .gitディレクトリの所有者を変更
RUN chown -R devuser:devuser /workspace/.git

# ユーザーを切り替え
USER devuser

# ポートの公開
EXPOSE 3000

# 起動コマンド
CMD ["npm", "run", "dev"]