# Kali Linux will not boot to GUI
##  1. Корректировка sources.list:
```bash
cd /etc/apt
sudo nano sources.list
```
Добавить строки в конец файла:

deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib

Ctrl-o и ctrl-x для выхода

## 2. Установка gdm3
```bash
sudo apt-get install gdm3
```
Выбрать gdm3 как "Default display manager"

Перезагрузить Linux
```bash
sudo reboot
```

## 3. Перезайти в VM (при необходимости) 

## 4. Подождать (экран прогружается иногда долго) 
Возможно попробовать запустить gdm3 принудительно 
```bash
service gdm3 start
```
