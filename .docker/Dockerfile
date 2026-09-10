# syntax=docker/dockerfile:1.7
FROM webbutvecklinghelsingborg/gitops:openlitespeed-0.0.3

USER root

RUN curl -fsSL -o /usr/local/bin/wp \
  https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && chmod 755 /usr/local/bin/wp

WORKDIR /var/www/vhosts/localhost/html

COPY --chown=1000:1000 build-output/ .
COPY --chown=1000:1000 .docker/templates/htaccess .htaccess
COPY --chown=1000:1000 --chmod=755 \
  .docker/templates/conf_database.sh \
  .docker/templates/conf_seed_db.sh \
  .docker/templates/prepare_wordpress.sh \
  .docker/templates/wp_deactivate_plugins.sh \
  .docker/templates/entrypoint-wrapper.sh \
  ./

EXPOSE 80 7080

ENTRYPOINT ["./entrypoint-wrapper.sh"]
