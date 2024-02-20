# Домашнее задание к занятию «Репликация и масштабирование. Часть 1»


---


## Задание 1.

	На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

	Ответить в свободной форме.


## Решение 1


	Master-Slave репликация используется для отказоустойчивости, так же позволяет распределить нагрузку на базу данных, между несколькими серверами или репликами. Изменения данных возможны только на Master ноде, при изменениях они копируются на Slave ноду. Чтение данных возможны как с Master так и со Slave ноды.
	Master-Master репликация используется для добавления избыточности и повышает эффективность при обращении к данным. Изменения данных возможны на любой ноде, после чего они копируются на оставшиеся ноды. Чтение данных так же возможно с любой ноды


## Задание 2.

	Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

	Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.


## Решение 2.
	
	Конфигурация Master

![Конфигурация Master](https://github.com/vladrabbit/hw_img/blob/main/img/master-conf.png)

	Конфигурация Slave

![Конфигурация Slave](https://github.com/vladrabbit/hw_img/blob/main/img/slave-conf.png)

	Статус Master

![Статус Master](https://github.com/vladrabbit/hw_img/blob/main/img/master-1.png)

	Статус Slave

![Статус Slave](https://github.com/vladrabbit/hw_img/blob/main/img/slave-1.png)

	Статус Master после создания базы

![Статус Master после создания базы](https://github.com/vladrabbit/hw_img/blob/main/img/master-2.png)

	Статус Slave после создания базы

![Статус Slave после создания базы](https://github.com/vladrabbit/hw_img/blob/main/img/slave-2.png)



---
