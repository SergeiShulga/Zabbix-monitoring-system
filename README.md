# Zabbix monitoring system -Сергей Шульга
### Задание 1
Установите Zabbix Server с веб-интерфейсом.
Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия что есть в системном репозитороии Debian 11
Пользуясь конфигуратором комманд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server
### Решение:
1. Выбераем платформу
   ВЕРСИЯ ZABBIX 6.4
   ДИСТРИБУТИВ ОС Debian
   ВЕРСИЯ ОС 11 (Bullseye)
   КОМПОНЕНТ ЗАББИКС Server, Frontend, Agent
   БАЗА ДАННЫХ PostgreSQL
   ВЕБ-СЕРВЕР Apache
2. Установите и сконфигурируйте Zabbix для выбранной платформы
   a. Установите репозиторий Zabbix
   #### wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
   #### dpkg -i zabbix-release_6.4-1+debian11_all.deb
   #### apt update
   b. Установите Zabbix сервер, веб-интерфейс и агент
   #### apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent2
   c. Создайте базу данных
   Установите и запустите сервер базы данных.
   Выполните следующие комманды на хосте, где будет распологаться база данных.
   #### sudo -u postgres createuser --pwprompt zabbix
   #### sudo -u postgres createdb -O zabbix zabbix
   На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.
   #### zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
   d. Настройте базу данных для Zabbix сервера
   Отредактируйте файл /etc/zabbix/zabbix_server.conf
   DBPassword=password
   e. Запустите процессы Zabbix сервера и агента
   Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.
   #### systemctl restart zabbix-server zabbix-agent2 apache2
   #### systemctl enable zabbix-server zabbix-agent2 apache2
   f. Open Zabbix UI web page
   The default URL for Zabbix UI when using Apache web server is http://192.168.56.101/zabbix
   логин для входа: Admin, пароль: zabbix 
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/001_1_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/002_2_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/004_5_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/005_6_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/006_7_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/007_8_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/008_9_11zon.png)
### Задание 2
Установите Zabbix Agent на два хоста.

Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

### Решение:
Установите и сконфигурируйте Zabbix для выбранной платформы
a. Установите репозиторий Zabbix
Документация
#### wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
#### dpkg -i zabbix-release_6.4-1+debian11_all.deb
#### apt update
b. Установите Заббикс aгент2
#### apt install zabbix-agent2 zabbix-agent2-plugin-*
c. Запустите процесс Zabbix агента2
Запустите процесс Zabbix агента2 и настройте его запуск при загрузке ОС.
#### systemctl restart zabbix-agent2
#### systemctl enable zabbix-agent2

![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/001_9_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/001_10_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/011_11_11zon.png)
![alt text](https://github.com/SergeiShulga/Zabbix-monitoring-system/blob/main/img/012_12_11zon.png)
