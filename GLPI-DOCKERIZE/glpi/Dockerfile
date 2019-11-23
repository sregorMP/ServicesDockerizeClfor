FROM nginx:alpine
WORKDIR /site

RUN adduser -u 82 -D www-data -S /sbin/nologin \
    && addgroup www-data www-data \
    && addgroup www-data nginx     

RUN wget https://github.com/glpi-project/glpi/releases/download/9.1.6/glpi-9.1.6.tgz -O /tmp/glpi.tgz \
    && tar -C /site/ -xzf /tmp/glpi.tgz

RUN chown -R www-data:www-data /site/glpi/ \
    && chmod -R 755 /site/glpi/ \
    && chmod -R 777 /site/glpi/plugins
    
RUN echo '*/1 * * * * php /site/glpi/front/cron.php &>/dev/null' >> /etc/crontabs/root \ 
    && echo '*/1 * * * * php /site/glpi/front/cron.php &>/dev/null' >> /etc/crontabs/root
