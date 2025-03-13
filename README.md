# moodlealt
Установка компонентов moodle:

( обязательно сделайте apt-get update -y , иначе не загрузится) apt-get install moodle moodle-apache2 moodle-local-mysql

Включаем БД

systemctl enable --now mysqld Создаём саму БД, о правильном создании БД можете почитать на ALt wiki mysql -u root CREATE DATABASE namedb DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci; GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES,DROP,INDEX,ALTER ON moodledb.* TO moodle@localhost IDENTIFIED BY 'YouPAsswd'; quit;

далее наобходимо загрузить исходники Moodle

cd /opt git clone git://git.moodle.org/moodle.git
cd /opt/moodle

git branch --track MOODLE_39_STABLE origin/MOODLE_405_STABLE

cp -R /opt/moodle /var/www/html/

Выдаём все нужные права mkdir /var/moodledata

chown -R apache2:webmaster /var/moodledata chmod -R 777 /var/moodledata chmod ugoa=rwx /var/moodledata chmod -R 0755 /var/www/html/moodle

Теперь нужно раскомментировать и изменить параметр в /etc/php/8.2/apache2-mod_php/php.ini:

max_input_vars = 10000

Ребут апача

systemctl restart httpd2

далее заходите по доменному имени/IP и настраиваете в морде
