# Домашнее задание к занятию "`Disaster recovery и Keepalived`" - `Владлен Зайцев`


---

### Задание 1

Задание 1

    Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.
    На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
    Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
    Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
    На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.


### Решение 1

![Routers config — Зайцев.В.А](https://github.com/vladrabbit/hw_img/blob/main/img/hsrp.png)


### Задание 2


    Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.
    Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
    Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
    Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
    На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

### Решение 2

####keepalived.conf Server1

```
vrrp_script check_nginx {
script "/home/blade/test.sh -k check"
interval 3
}

vrrp_instance VI_1 {
        state MASTER
        interface enp0s3
        virtual_router_id 10
        priority 255
        advert_int 1

        virtual_ipaddress {
              192.168.31.10/24
        }
	track_script {
	check_nginx
	}

}

```

####keepalived.conf Server2

```
vrrp_script check_nginx {
script "/home/blade/test.sh -k check"
interval 3
}

vrrp_instance VI_1 {
        state BACKUP
        interface enp0s3
        virtual_router_id 10
        priority 200
        advert_int 1

        virtual_ipaddress {
              192.168.31.10/24
        }
	track_script {
        check_nginx
        }

}

```

####bash-скрипт

```bash
#!/bin/bash
if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.nginx-debian.html ]]; then
   exit 0
else
   exit 1
fi
```


####Скриншот переезда Master

![Master — Зайцев.В.А](https://github.com/vladrabbit/hw_img/blob/main/img/nginx-k1.png)

####Скриншот переезда Backup

![Backup1 — Зайцев.В.А](https://github.com/vladrabbit/hw_img/blob/main/img/nginx-k2.png)
![Backup2 — Зайцев.В.А](https://github.com/vladrabbit/hw_img/blob/main/img/nginx-k3.png)


---
