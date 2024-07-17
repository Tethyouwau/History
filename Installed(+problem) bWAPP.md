Скачать дистрибутив можно здесь  - https://sourceforge.net/projects/bwapp/files/bWAPP/

Установка в Kali

```bash
cd Downloads 
sudo unzip (название архива с bwapp)  -d /var/www/html 
chmod -R 777 /var/www/html/bWAPP
sudo service apache2 start
sudo service mysql start

cd /var/www/html/bWAPP/admin # переходим в директорию админ
nano settings.php # открываем файл настроек и меняем логин и пароль для базы данных на тот который нам нужен (обычно для упрощения используется user/pass)
```
Заходим в браузер и открываем "http://localhost", должна открыться страница apache2, по наличию на которой "IT WORKS" мы понимаем, что http сервер работает.

Если не открывается страница "http://localhost":
```bash
sudo service apache2 restart # пробуем перезагрузить http сервер
sudo reboot # если не получилось - перезагружаем ОС польностью
```
Должно заработать, но если нет , тогда поможет - google.com

Когда мы проверили работу http сервера, переходим по ссылке на bWAPP:

http://localhost/bWAPP/index.php

Нажимаем install страница должна перезагрузиться и пройти полная установка bWAPP. После этого автоматически произойдет перенаправление на страницу с логином. 

Если этого не произошло выполняем следующее:

```bash
cd /var/www/html/bWAPP
nano install.php # открываем файл установки и убираем лишний символ
```

**Лишний символ в install.php убирается вот тут:**
```php
// Checks if the database 'bWAPP' already exists
if(!mysqli_select_db($link,"bWAPP")) //"!" убираем
```

Должно получиться вот так: 
```php
// Checks if the database 'bWAPP' already exists
if(mysqli_select_db($link,"bWAPP")) //"!" отсутствует теперь
```

Пробуем перезагрузить страницу в бразуере, если не получилось - двигаемся дальше: 

```bash
mysql -u root -p # заходим в mysql под рутом
 
use mysql;
 
create user 'user'@'localhost' identified by 'pass'; #создаем пользователя user с паролем pass
 
grant all privileges on bWAPP.* to 'user'@'localhost' identified by 'pass'; # добавляем все привелегии для только что созданного пользователя
```

Перезагружаем страницу в браузере с bWAPP, если не получилось - возвращаемся в терминал с открытым mysql:

```mysql
show databases; # отобразится список всех доступных баз данных, если в списке нет bWAPP - нужно выполнить следующую команду (создать базу данных)
create database bWAPP; # создаем базу данных для bAWPP
\q # выходим из терминала mysql и возвращаемся в bash(zsh)
```

```bash
sudo service mysql restart # после добавления базы данных перезагружаем сервер mysql
```

Снова перезагружаем страницу и теперь должно было заработать. Если не сработало - выход только один (google.com)
