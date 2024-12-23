---
## Front matter
title: "Отчёт по лабораторной работе №5"
subtitle: "Администрирование сетевых подсистем"
author: "Ищенко Ирина НПИбд-02-22"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---


# Цель работы

Приобретение практических навыков по расширенному конфигурированию HTTP-сервера Apache в части безопасности и возможности использования PHP.

# Выполнение лабораторной работы

Запускаем ВМ через рабочий каталог. На ВМ `server` входим под собственным пользователем и переходим в режим суперпользователя. В каталоге `/etc/ssl` создаем каталог `private` (рис. [-@fig:1]):

![создание каталога](image/1.png){#fig:1 width=70%}

Генерируем ключ и сертификат (рис. [-@fig:2]), введя следующую команду:
openssl req -x509 -nodes -newkey rsa:2048 -keyout www.ioithenko.net.key -out www.ioithenko.net.crt

![Заполнение сертификата](image/2.png){#fig:2 width=70%}

Сгенерированные ключ и сертификат появляются в соответствующем каталоге `/etc/ssl/private`. Копируем сертификат в каталог `/etc/ssl/certs` (рис. [-@fig:3])

![Содержимое каталогов `/etc/ssl/private` и `/etc/ssl/certs`](image/3.png){#fig:3 width=70%}

Редактируем конфигурационный файл  `/etc/httpd/conf.d/www.ioithenko.net` (рис. [-@fig:4])

![Редактирование файла  `/etc/httpd/conf.d/www.ioithenko.net`](image/4.png){#fig:4 width=70%}

Вносим изменения в настройки межсетевого экрана на сервере, перезапускаем веб-сервер (рис. [-@fig:5])

![Внесение изменений в настройки межсетевого экрана, перезапуск веб-сервера](image/5.png){#fig:5 width=70%}

На ВМ `client` открываем в браузере страницу `www.ioithenko.net` с сообщением о незащищенности соединения (рис. [-@fig:6]). Добавив страницу в исключения, просматриваем информацию о сертификате (рис. [-@fig:7]), (рис. [-@fig:8]). 

![Сообщение о незащищенности соединения](image/6.png){#fig:6 width=70%}

![Информация о веб-странице](image/7.png){#fig:7 width=70%}

![Содержимое сертификата](image/8.png){#fig:8 width=70%}

Устанавливаю пакеты для работы с PHP: `dnf -y install php` (рис. [-@fig:9]).

![PHP](image/9.png){#fig:9 width=70%}

В каталоге `/var/www/html/www.ioithenko.net` заменяю `index.html` на `index.php`.

Редактирую `index.php` (рис. [-@fig:10]).

![Редактирование `index.php` ](image/10.png){#fig:10 width=70%}

Корректирую права доступа в каталог с веб-контентом, восстанавливаю контекст безопасности в SELinux, перезагружаю HTTP-сервер (рис. [-@fig:11]).

![Права доступа, контекст безопасности](image/11.png){#fig:11 width=70%}

На ВМ `client` ввожу в адресную строку браузера `www.ioithenko.net` и вижу веб-страницу с информацией об используемой версии PHP (рис. [-@fig:12]).

![Веб-страница с информацией об используемой версии PHP](image/12.png){#fig:12 width=70%}

На ВМ `server` перехожу в каталог для внесения изменений в настройки внутреннего окружения `/vagrant/provision/server/` и копирую в соответствующие каталоги конфигурационные файлы (рис. [-@fig:13]).

![Внутреннее окружение](image/13.png){#fig:13 width=70%}

В скрипт `/vagrant/provision/server/http.sh` вношу изменения, добавив установку PHP и настройку межсетевого экрана для работы с `https` (рис. [-@fig:14]).

![Внесение изменений в скрипт http.sh](image/14.png){#fig:14 width=70%}

# Выводы

В ходе лабораторной работы я приобрела практические навыки по расширенному конфигурированию HTTP-сервера Apache в части безопасности и возможности использования PHP.

# Ответы на контрольные вопросы

1. В чём отличие HTTP от HTTPS? 

**HTTP** (HyperText Transfer Protocol) – это протокол передачи
данных, который используется для передачи информации
между клиентом (например, веб-браузером) и сервером. Однако
он не обеспечивает шифрование данных, что делает их
уязвимыми к перехвату злоумышленниками. 

**HTTPS** (HyperText Transfer Protocol Secure) - это расширение
протокола HTTP с добавлением шифрования, обеспечивающее
безопасную передачу данных между клиентом и сервером. Протокол HTTPS использует SSL (Secure Sockets Layer) или более современный TLS (Transport Layer Security) для
шифрования данных.

2. Каким образом обеспечивается безопасность контента веб-сервера при работе через HTTPS? 

Шифрование данных: при использовании HTTPS данные,
передаваемые между клиентом и сервером, шифруются, что
делает их невозможными для прочтения злоумышленниками,
перехватывающими трафик.

Идентификация сервера: сервер предоставляет цифровой
сертификат, подтверждающий его легитимность. Этот
сертификат выдается сертификационным центром и содержит
информацию о владельце сертификата, публичный ключ для
шифрования и подпись, подтверждающую подлинность
сертификата.

3. Что такое сертификационный центр? 

Сертификационный центр (Центр сертификации) - это доверенная сторона, которая выдает цифровые
сертификаты, подтверждающие подлинность владельца сертификата.
Пример: Одним из известных сертификационных центров
является "Let's Encrypt". Он предоставляет бесплатные SSL-
сертификаты, которые используются для обеспечения безопасного соединения на множестве веб-сайтов. Владельцы
веб-сайтов могут получить сертификат от Let's Encrypt, чтобы
обеспечить шифрование и подтвердить свою легитимность в
онлайн-среде.


