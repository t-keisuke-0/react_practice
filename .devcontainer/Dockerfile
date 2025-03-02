FROM node:20-slim

# 必要最小限のパッケージのみインストール
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# ワークスペースディレクトリを作成
WORKDIR /workspace

# タイムゾーンを設定
ENV TZ=Asia/Tokyo

# ビルド時にusernameを環境変数から取得し、.gitconfigをコピー
ARG USERNAME
COPY --from=node:20-slim /root/.bashrc /tmp/
RUN if [ -n "$USERNAME" ]; then \
    if [ -f "/c/Users/$USERNAME/.gitconfig" ]; then \
        cp /tmp/.bashrc /root/.bashrc && \
        cp "/c/Users/$USERNAME/.gitconfig" /root/.gitconfig; \
    else \
        echo ".gitconfig not found at /c/Users/$USERNAME/.gitconfig" ; \
    fi \
    else \
    echo "USERNAME is not set. Using default .gitconfig." ; \
    fi

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