FROM ubuntu:14.04
EXPOSE 80

RUN apt-get update && apt-get -y install supervisor apache2 php5 php5-mysql 
# Setup database
RUN echo 'mysql-server mysql-server/root_password password f7388dc5eeaef942c5b7910454444a25' | debconf-set-selections && \
   echo 'mysql-server mysql-server/root_password_again password f7388dc5eeaef942c5b7910454444a25' | debconf-set-selections
RUN apt-get install -qqy mysql-server
RUN (/usr/bin/mysqld_safe &); sleep 5; mysqladmin -u root -pf7388dc5eeaef942c5b7910454444a25 create wordpress
RUN rm -f /var/www/html/index.html
COPY supervisor.conf /etc/supervisor/conf.d/supervisor.conf
COPY mime.conf /etc/apache2/mods.enabled/mime.conf
COPY index.php /var/www/html/
CMD ["/usr/bin/supervisord","-c","/etc/supervisor/conf.d/supervisor.conf"]
