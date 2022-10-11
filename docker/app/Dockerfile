# イメージ利用宣言
FROM php:8.1-apache-buster

# 設定ファイルをDockerコンテナないのPHP、Apacheに読み込ませる。
# ADD: ローカルのファイルをDockerコンテナ内にコピーする。
# ADD #{ローカルフォルダ} #{Dockerコンテナ内のパス}
ADD php.ini /usr/local/etc/php/
ADD 000-default.conf /etc/apache2/sites-enabled/

# composerのインストール
# RUN: コンテナ内でコマンドを実行
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# ミドルウェアのインストール
RUN apt-get update \
&& apt-get install -y \
git \
zip \
unzip \
vim \
libpng-dev \
libpq-dev \
&& docker-php-ext-install pdo_mysql

# Laravelで必要になるmodRewriteを有効化
RUN mv /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled
RUN /bin/sh -c a2enmod rewrite

