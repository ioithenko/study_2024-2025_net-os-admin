---
## Front matter
lang: ru-RU
title: Лабораторная работа №9
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

Приобретение практических навыков по установке и простейшему конфигурированию POP3/IMAP-сервера.

# Выполнение лабораторной работы

##

![Установка Dovecot](image/1.png){#fig:001 width=70%}

##

![Редактирование файла /etc/dovecot/dovecot.conf](image/2.png){#fig:002 width=70%}

##

![Редактирование файла /etc/dovecot/conf.d/10-auth.conf](image/3.png){#fig:003 width=70%}

##

![Просмотр файла /etc/dovecot/conf.d/auth-system.conf.ext](image/4.png){#fig:004 width=70%}

##

![Редактирование файла /etc/dovecot/conf.d/10-mail.conf](image/5.png){#fig:005 width=70%}

##

![Конфигурация Postfix](image/6.png){#fig:006 width=70%}

##

![Конфигурация межсетевого экрана для работы с POP3 и IMAP и запуск Dovecot](image/7.png){#fig:007 width=70%}

##

![Просмотр почты](image/8.png){#fig:008 width=70%}

##

![Просмотр mailbox](image/9.png){#fig:009 width=70%}

##

![Настройка учетной записи почтового клиента](image/10.png){#fig:010 width=70%}

##

![Настройка IMAP-сервера для входящих сообщений](image/11.png){#fig:011 width=70%}

##

![Настройка SMTP-сервера для исходящих сообщений](image/12.png){#fig:012 width=70%}

##

![Проверка получения писем на почтовом клиенте](image/13.png){#fig:013 width=70%}

##

![Просмотр мониторинга почтовой службы на сервере](image/14.png){#fig:014 width=70%}

##

![Просмотр информации о почтовой службе с помощью mail](image/15.png){#fig:015 width=70%}

##

![Просмотр информации о почтовой службе с помощью doveadm](image/16.png){#fig:016 width=70%}

##

![Проверка почтовой службы с помощью протокола Telnet](image/17.png){#fig:017 width=70%}

##

![Создание окружения для внесения изменений в настройки окружающей среды](image/18.png){#fig:018 width=70%}


## Выводы

В ходе лабораторной работы я приобрела практические навыки по установке и простейшему конфигурированию POP3/IMAP-сервера.