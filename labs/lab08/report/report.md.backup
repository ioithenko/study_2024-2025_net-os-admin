---
## Front matter
title: "Отчёт по лабораторной работе №8"
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

Приобретение практических навыков по установке и конфигурированию SMTPсервера.

# Выполнение лабораторной работы

Запускаю ВМ через рабочий каталог. На ВМ `server` вхожу под собственным пользователем и перехожу в режим суперпользователя. Устанавливаю необходимые пакеты (рис. [-@fig:1]).

![Установка пакетов](image/1.png){#fig:1 width=70%}

Конфигурирую межсетевой экран, восстанавливаю контекст безопасности, запускаю Postfix (рис. [-@fig:2]).

![Конфигурация межсетевого экрана, восстановление контекста безопасности, запуск Postfix ](image/2.png){#fig:2 width=70%}

Просматриваю текущие настройки, введя `postconf`. Просматриваю значения `myorigin` и `mydomain`. Заменяю значение параметра `myorigin` на `mydomain` и проверяю замену. Проверяю корректность содержания конфигурационного файла, введя `postfix check`, перезагружаю конф. файлы Postfix, просматриваю все параметры со значением, отличным от значения по умолчанию (рис. [-@fig:3]). Задаю жестко значение домена, отключаю IPv6 в списке разрешенных в работе протоколов, оставив только IPv4, после чего перезагружаю Postfix (рис. [-@fig:4]).

![Текущие настройки](image/3.png){#fig:3 width=70%}

![Изменение параметров с помощью postconf](image/5.png){#fig:4 width=70%}

Ввожу команду для отправки себе письма (рис. [-@fig:5]).

![Текущие настройки](image/6.png){#fig:5 width=70%}

На втором терминале запускаю мониторинг работы почтовой службы и вижу сообщение о доставке (рис. [-@fig:6])

![Мониторинг работы почтовой службы: письмо доставлено](image/7.png){#fig:6 width=70%}

Просматриваю содержимое `/var/spool/mail` и убеждаюсь, что письмо в файле `ioithenko` появилось (рис. [-@fig:7]). 

![Проверка `/var/spool/mail` ](image/8.png){#fig:7 width=70%}

На ВМ `client` перехожу в режим суперпользователя и устанавливаю аналогично необходимые пакеты. Отключаю IPv6 в списке разрешенных в работе протоколов, оставив только IPv4, запускаю Postfix (рис. [-@fig:8]) и (рис. [-@fig:9]).

![Установка пакетов](image/10.png){#fig:8 width=70%}

![Изменение разрешенных в работе протоколов, запуск Postfix на клиенте](image/11.png){#fig:9 width=70%}

Аналогичным образом отправляю себе второе письмо через клиент. Письмо на сервер не доставлено (рис. [-@fig:10]) и (рис. [-@fig:11]).

![Установка пакетов](image/12.png){#fig:10 width=70%}
 
![Мониторинг почтовой службы](image/13.png){#fig:11 width=70%}

На сервере изменяю конфигурацию Postfix, разрешив Postfix прослушивать соединения не только с локального узла, но и с других интерфейсов сети. Добавляю адрес внутренней сети, разрешив пересылку между узлами сети. Перезагружаю конфигурацию Postfix и перезапускаю его (рис. [-@fig:12]).

![Изменение параметров](image/14.png){#fig:12 width=70%}

Повторяю отправку письма и проверяю. Вижу в журнале сообщения о том, что установлено соединение с сервером, письмо получено, соединение разорвано (рис. [-@fig:13]), (рис. [-@fig:14]) и (рис. [-@fig:15]).

![Отправка письма](image/15.png){#fig:13 width=70%}

![Письмо](image/16.png){#fig:14 width=70%}

![Мониторинг почтовой службы](image/17.png){#fig:15 width=70%}

С клиента отправляю письмо на свой доменный адрес (рис. [-@fig:16]).

![Отправка письма](image/18.png){#fig:16 width=70%}

Запустив мониторинг работы почтовой службы, вижу, что сообщение не доставлено (рис. [-@fig:17]).

![Мониторинг работы почтовой службы: сообщение не доставлено](image/19.png){#fig:17 width=70%}

Просматриваю очередь на отправление сообщений (рис. [-@fig:18]). Вношу изменения в файл прямой DNS-зоны (рис. [-@fig:19]).

![Отправка письма](image/20.png){#fig:18 width=70%}

![Изменение файла прямой DNS-зоны ](image/21.png){#fig:19 width=70%}

Вношу изменения в файл обратной DNS-зоны  (рис. [-@fig:20]).

![Изменение файла обратной DNS-зоны ](image/22.png){#fig:20 width=70%}

В конфигурации Postfix добавляю домен в список элементов сети, для которых данный сервер является конечной точкой доставки почты. Перезагружаю конфигурацию Postfix, восстанавливаю контекст безопасности в SELinux, перезапускаю DNS, пробую отправить сообщения из очереди на отправление (рис. [-@fig:21]).

![Конфигурация postfix ](image/23.png){#fig:21 width=70%}

Проверяю отправку почты с клиента на доменный адрес (рис. [-@fig:22]) и (рис. [-@fig:23]).

![Отправка письма](image/24.png){#fig:22 width=70%}

![Мониторинг работы почтовой службы: сообщение на доменный адрес доставлено](image/25.png){#fig:23 width=70%}

Дополнительно проверяю `/var/spool/mail/ioithenko` и убеждаюсь, что сообщение доставлено (рис. [-@fig:24])

![Cообщение на доменный адрес в /var/spool/mail/ioithenko](image/26.png){#fig:24 width=70%}

На ВМ `server` перехожу в каталог для внесения изменений в настройки внутреннего окружения `/vagrant/provision/server/` и заменяю конф. файлы DNS-сервера. Создаю скрипт `mail.sh` с правом на исполнение. Редактирую скрипт (рис. [-@fig:25]).

![Создание скрипта `mail.sh` на сервере](image/27.png){#fig:25 width=70%}

На ВМ `client` аналогично создаю скрипт `mail.sh' и редактирую его (рис. [-@fig:26]).

![Создание скрипта `mail.sh` на клиенте](image/28.png){#fig:26 width=70%}

Для отработки созданных скриптов во время загрузки виртуальных машин в конфигурационном файле `Vagrantfile` добавляю запись в конфигурации сервера 

```
server.vm.provision "server mail",
		type: "shell",
		preserve_order: true,
		path: "provision/server/mail.sh"
```
 
 и клиента
 
```
client.vm.provision "client mail",
		type: "shell",
		preserve_order: true,
		path: "provision/client/mail.sh"
```

# Выводы

В ходе лабораторной работы я приобрела практических навыков по установке и конфигурированию SMTPсервера.


# Ответы на контрольные вопросы

1. В каком каталоге и в каком файле следует смотреть конфигурацию Postfix?

- Конфигурация Postfix обычно хранится в файле `main.cf`, а путь к
этому файлу может различаться в разных системах. Однако, обычно
он находится в каталоге `/etc/postfix/`. Таким образом, путь к файлу
конфигурации будет `/etc/postfix/main.cf`.

2. Каким образом можно проверить корректность синтаксиса конфигурационном файле Postfix? 

- ` postfix check`

3. В каких параметрах конфигурации Postfix требуется внести изменения в значениях для настройки возможности отправки писем не на локальный хост, а на доменные адреса? 

- Для настройки возможности отправки
писем не на локальный хост, а на доменные адреса, вы можете
изменить параметры `myhostname` и `mydomain` в файле `main.cf`.

4. Приведите примеры работы с утилитой `mail` по отправке письма, просмотру имеющихся писем, удалению письма. 

- Отправка письма: `echo "Текст письма" user@example.com`

- Просмотр имеющихся писем: `mail`

- Удаление письма: `mail -d номер_письма`

5. Приведите примеры работы с утилитой postqueue. Как посмотреть очередь сообщений? Как определить число сообщений в очереди? Как отправить все сообщения, находящиеся в очереди? Как удалить письмо из очереди? 

- Просмотр очереди сообщений: `postqueue -p`

- Определение числа сообщений в очереди: `postqueue -p | grep -c "^[A-F0-9]"`

- Отправка всех сообщений из очереди: `postqueue -f`

- Удаление письма из очереди: `postsuper -d ID_СООБЩЕНИЯ`