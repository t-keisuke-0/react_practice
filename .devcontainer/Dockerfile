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

# 依存関係のインストール
RUN volta install node@20 && volta install npm@latest && npm install

# ソースコードのコピー
COPY . .

# ポートの公開
EXPOSE 3000

# 起動コマンド
CMD ["npm", "run", "dev"]