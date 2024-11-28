---
## Front matter
lang: ru-RU
title: Лабораторная работа №13
subtitle: Администрирование сетевых подсистем
author:
  - Ищенко Ирина НПИбд-02-22
institute:
  - Российский университет дружбы народов, Москва, Россия

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

## Цель работы

Приобретение практических навыков настройки сервера NFS для удалённого доступа к ресурсам.

# Выполнение лабораторной работы

##

![Подключение через NFS каталога только на чтение](image/1.png){#fig:001 width=70%}

##

![Запуск NFS-сервера](image/2.png){#fig:002 width=70%}

##

![Просмотр подмонтированных удалённых ресурсов на клиенте](image/3.png){#fig:003 width=70%}

##

![Остановка сервиса межсетевого экрана](image/4.png){#fig:004 width=70%}

##

![Просмотр подмонтированных удалённых ресурсов на клиенте](image/5.png){#fig:005 width=70%}

##

![Просмотр задействованных при удалённом монтировании служб](image/6.png){#fig:006 width=70%}

##

![Просмотр задействованных при удалённом монтировании служб](image/7.png){#fig:007 width=70%}

##

![Добавление служб rpc-bind и mountd в настройки межсетевого экрана](image/8.png){#fig:008 width=70%}

##

![Проверка подключения удалённого ресурса на клиенте](image/9.png){#fig:009 width=70%}

##

![Монтирование дерева NFS](image/10.png){#fig:010 width=70%}

##

![Проверка подключения ресурса](image/11.png){#fig:011 width=70%}

##

![Добавление записи в файл /etc/fstab на клиенте](image/12.png){#fig:012 width=70%}

##

![Проверка наличия автоматического монтирования удалённых ресурсов при запуске ОС](image/13.png){#fig:013 width=70%}

##

![Проверка автоматического подключения удалённого ресурса](image/14.png){#fig:014 width=70%}

##

![Проверка содержимого /srv/nfs](image/15.png){#fig:015 width=70%}

##

![Проверка содержимого /mnt/nfs](image/16.png){#fig:016 width=70%}

##

![Добавление в файл /etc/exports экспорт каталога веб-сервера](image/17.png){#fig:017 width=70%}

##

![Проверка содержимого /mnt/nfs](image/18.png){#fig:018 width=70%}

##

![Добавление записи в файл /etc/fstab](image/19.png){#fig:019 width=70%}

##

![Проверка содержимого /mnt/nfs](image/20.png){#fig:020 width=70%}

##

![Проверка прав доступа на каталог](image/21.png){#fig:021 width=70%}

##

![Подключение каталога пользователя в файле /etc/exports](image/22.png){#fig:022 width=70%}

##

![Добавление записи в файл /etc/fstab](image/23.png){#fig:023 width=70%}

##

![Проверка содержимого /mnt/nfs](image/24.png){#fig:024 width=70%}

##

![Скрипта файла /vagrant/provision/server/nfs.sh](image/25.png){#fig:025 width=70%}

## Выводы

В результате выполнения лабораторной работы я приобрела практические навыки настройки сервера NFS для удалённого доступа к ресурсам.