FROM nginx:latest

RUN groupadd -g 1000 magento

RUN useradd -d /var/www/html -s /bin/bash -u 1000 -g 1000 magento

RUN usermod -a -G sudo magento

RUN mkdir -p /var/www/html

RUN chown -R magento:magento /var/www/html

RUN touch /var/run/nginx.pid \
 && chown -R magento:magento /var/run/nginx.pid /var/cache/nginx

USER magento