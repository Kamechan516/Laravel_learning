FROM nginx:mainline AS base

# opensslのインストール
RUN apt-get update && apt-get install -y openssl

FROM base AS dev

# nginx.confのコピー
COPY conf/dev/nginx.conf /etc/nginx/nginx.conf

# 設定ファイルを格納sるディレクトリを作成
RUN mkdir -p /etc/nginx/conf

# 設定ファイルのコピー
COPY conf/dev/laravel.conf /etc/nginx/conf/laravel.conf
