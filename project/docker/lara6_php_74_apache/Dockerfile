FROM php:7.4-apache

# Composer のバージョン と ハッシュ値
ARG composer_ver=1.10.16
ARG composer_hash=e494bb438e44b9e4782c16940b229a8c46ea8a3baa9b908bf9db310cd0171ee2

# Composer の保存先
ARG composer_path=/usr/local/bin/composer

RUN apt-get update \
  # Composer インストール
  && php -r "copy('https://getcomposer.org/download/$composer_ver/composer.phar', '$composer_path');" \
  && chmod 755 $composer_path \
  && php -r "if (hash_file('sha256', '$composer_path') !== '$composer_hash') { \
          echo '!!! Failed to install Composer !!!'; \
          unlink('$composer_path'); \
      } \
      echo PHP_EOL;" \
  # Vim （省略可）
  && apt-get install -y vim \
  # unzip コマンド (composer create-project で必要)
  && apt-get install -y unzip \
  # PDO MySQL 拡張
  && docker-php-ext-install pdo_mysql \
  # /var/www/html/public をドキュメントルートに変更
  # (必要に応じて)
  && sed -ri -e 's!/var/www/html!/var/www/html/public!g' /etc/apache2/sites-available/*.conf \
  # mod_rewrite 有効化
  && a2enmod rewrite
