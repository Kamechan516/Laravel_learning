FROM php:8.3.0-fpm AS base

# Vite用のポートを開放
EXPOSE 5173

# 必須パッケージのインストール
RUN apt-get update && apt-get install -y git libzip-dev zip unzip

# PHP拡張のインストール
RUN docker-php-ext-install pdo_mysql zip

# Composerのインストール
COPY --from=composer:lts /usr/bin/composer /usr/bin/composer

# Node.jsのインストール
COPY --from=node:lts /usr/local/bin/node /usr/local/bin/node
COPY --from=node:lts /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node:lts /usr/local/bin/npm /usr/local/bin/npm

# npm用のシンボリックリンクを作成
RUN ln -s /usr/local/lib/node_modules/npm/lib/cli.js /usr/local/lib/cli.js

# npmを最新版にアップデート
RUN npm install -g npm



FROM base AS dev

# php.iniのをコピー
COPY conf/dev/php.ini /usr/local/etc/php/php.ini

# Composerの環境変数を設定
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_PROCESS_TIMEOUT 4600

# 作業ディレクトリを設定
WORKDIR /var/www/app