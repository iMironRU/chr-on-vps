# Установка CHR RouterOS на VPS

### Обновляем CenteOS
> yum update
### Ставим нужный софт
> yum install -y wget unzip net-tools
### Смотрим настойки сети
> ifconfig

### Монтируем tempfs в каталог /tmp
> mount -t tmpfs tmpfs /tmp
### Загружаем Image файл CHR RouterOS с сайта MikroTik.
> cd /tmp
> wget https://download.mikrotik.com/routeros/7.1.5/chr-7.1.5.img.zip
### Распаковываем скачанный образ из архива
> unzip chr-7.1.5.img.zip
### Записываем образ на жесткий диск
> dd if=chr-7.1.5.img of=/dev/vda bs=4M oflag=sync
### Где vda диск системы, узнать диск можно командой fdisk -l
### Принудительная перезагрузка
> echo 1 > /proc/sys/kernel/sysrq
> echo b > /proc/sysrq-trigger

### Устанавливаем настройки интерфейсов, настройки берем из ранее записанных.
> /ip address add interface=ether1 address=XXX.XXX.XXX.XXX/YY
### Добавляем маршрут по умолчанию:
> /ip route add dst-address=0.0.0.0/0 gateway=ZZZ.ZZZ.ZZZ.ZZZ/32
