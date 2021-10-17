# Replic-ubuntu
sudo apt update && sudo apt upgrade -y && sudo apt-get install -y mysql-server
 sudo mysql_secure_installation
  sudo systemctl enable mysql добавил в автозагрузку
  sudo mysql
  sudo mysql_config_editor set --login-path=client --host=localhost --user=root --password 
  sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf сменил айпи  с локала
  ![image](https://user-images.githubusercontent.com/79063567/137626783-988f75a2-0a6e-426d-b806-38c52c9aa28c.png)  скрипншот слейва
  
  ![image](https://user-images.githubusercontent.com/79063567/137626849-f17e97c7-2975-45da-8713-071929f9afb2.png)
скриншот мастера  с позицией бинлога


![image](https://user-images.githubusercontent.com/79063567/137627103-3331710b-614c-4c4b-98ff-3821fdf604f1.png) доступность    по портам есть

пользователь для репликации создан 
mysql> SELECT USER from mysql.user;
+------------------+
| USER             |
+------------------+
| repl             |
| debian-sys-maint |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
+------------------+

Б.кап
фаил с рабочего сервера  mysqldump --all-databases --no-create-info > dump-data.sql


  собрал данные с мастера  в слейф 
       mysql --host=10.128.0.4 -u root -p > dump_file.sql
   
сбор  бинлога  на постоянной основе
mysqlbinlog -R -h 10.128.0.4  -p --raw --stop-never binlog.000001

позиция с бинлога 
mysqlbinlog --start-position=1582 binlog.0000017 | mysql
  
