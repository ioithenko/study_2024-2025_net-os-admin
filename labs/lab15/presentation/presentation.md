---
## Front matter
lang: ru-RU
title: Лабораторная работа №15
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

Получение навыков по работе с журналами системных событий.

# Выполнение лабораторной работы

## Настройка сервера сетевого журнала

На сервере создадим файл конфигурации сетевого хранения журналов:

```
cd /etc/rsyslog.d
touch netlog-server.conf
```

## Настройка сервера сетевого журнала

![Включение журналирования по TCP-порту 514](image/1.png){#fig:001 width=70%}

## Настройка сервера сетевого журнала

![Перезапуск `rsyslog` и просмотр прослушиваемых портов](image/2.png){#fig:002 width=70%}

## Настройка сервера сетевого журнала

![Настройка межсетевого экрана для работы с TCP-портом 514](image/3.png)

## Настройка клиента сетевого журнала

На клиенте создадим файл конфигурации сетевого хранения журналов:

```
cd /etc/rsyslog.d
touch netlog-client.conf
```

## Настройка клиента сетевого журнала

![Редактирование файла конфигурации сетевого хранения журналов на клиенте: включение перенаправления на 514 порт](image/4.png){#fig:004 width=70%}

## Настройка клиента сетевого журнала

```
systemctl restart rsyslog
```

## Просмотр журнала

![Просмотр файла журнала на сервере](image/5.png){#fig:005 width=70%}

## Просмотр журнала

![Запуск графической программы для просмотра журналов](image/6.png){#fig:006 width=50%}

## Просмотр журнала

```
dnf -y install lnav
```

## Просмотр журнала

![Использование `lnav` для просмотра логов](image/7.png){#fig:007 width=40%}

## Выводы

В ходе выполнения лабораторной работы я приобрела практические навыки по работе с журналами системных событий.