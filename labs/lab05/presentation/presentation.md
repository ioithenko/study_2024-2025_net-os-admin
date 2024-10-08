---
## Front matter
lang: ru-RU
title: Лабораторная работа №5
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

Приобретение практических навыков по расширенному конфигурированию HTTP-сервера Apache в части безопасности и возможности использования PHP.

# Выполнение лабораторной работы

##

![создание каталога](image/1.png){#fig:1 width=70%}

##

![Заполнение сертификата](image/2.png){#fig:2 width=70%}

##

![Содержимое каталогов `/etc/ssl/private` и `/etc/ssl/certs`](image/3.png){#fig:3 width=70%}

##

![Редактирование файла  `/etc/httpd/conf.d/www.ioithenko.net`](image/4.png){#fig:4 width=70%}

##

![Внесение изменений в настройки межсетевого экрана, перезапуск веб-сервера](image/5.png){#fig:5 width=70%}

##

![Сообщение о незащищенности соединения](image/6.png){#fig:6 width=70%}

##

![Информация о веб-странице](image/7.png){#fig:7 width=70%}

##

![Содержимое сертификата](image/8.png){#fig:8 width=70%}

##

![PHP](image/9.png){#fig:9 width=70%}

##

![Редактирование `index.php` ](image/10.png){#fig:10 width=70%}

##

![Права доступа, контекст безопасности](image/11.png){#fig:11 width=70%}

##

![Веб-страница с информацией об используемой версии PHP](image/12.png){#fig:12 width=70%}

##

![Внутреннее окружение](image/13.png){#fig:13 width=70%}

##

![Внесение изменений в скрипт http.sh](image/14.png){#fig:14 width=70%}

# Выводы

В ходе лабораторной работы я приобрела практические навыки по расширенному конфигурированию HTTP-сервера Apache в части безопасности и возможности использования PHP.