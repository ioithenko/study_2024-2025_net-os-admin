---
## Front matter
title: "Отчёт по лабораторной работе №7"
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

Получить навыки настройки межсетевого экрана в Linux в части переадресации
портов и настройки Masquerading.


# Выполнение лабораторной работы

Запускаем ВМ через рабочий каталог. На ВМ `server` входим под собственным пользователем и переходим в режим суперпользователя.  На основе существующего файла описания службы ssh создаем файл с собственным описанием. Просматриваем содержимое файла (рис. [-@fig:1]).

![Создание собственного файла описания службы и просмотр](image/1.png){#fig:1 width=70%}

Открываем файл на редактирование и меняем порт 22 на порт 2022, в описании службы указав, что порт был изменен (рис. [-@fig:2])

![Редактирование файла описания службы](image/2.png){#fig:2 width=70%}

Просматриваем список доступных служб (новой службы пока нет) (рис. [-@fig:3]).

![Список доступных служб](image/3.png){#fig:3 width=70%}

Перезагружаем правила межсетевого экрана, снова просматриваем список доступных служб и видим новую (рис. [-@fig:4]).

![Новая служба в списке доступных служб](image/4.png){#fig:4 width=70%}

Новая служба отображается в списке доступных, но пока не активирована. Добавляем новую службу в FirewallD и просматриваем список активных служб (служба появилась). Перегружаем правила межсетевого экрана с сохранением информации о состоянии (рис. [-@fig:5])

![Добавление новой службы и просмотр списка активных служб, сохранение информации о состоянии](image/5.png){#fig:5 width=70%}

Организовываем переадресацию с порта 2022 на порт 22 на сервере(рис. [-@fig:6]).

![Переадресация](image/6.png){#fig:6 width=70%}

На клиенте пробуем получить доступ по SSH через порт 2022. Доступ получен (рис. [-@fig:7]). 

![Доступ по SSH к серверу через порт 2022 на клиенте](image/7.png){#fig:7 width=70%}

На сервере просматриваем, активирована ли в ядре системы возможность перенаправления IPv4-пакетов пакетов (рис. [-@fig:8]). Включаем перенаправление пакетов на сервере. Включаем маскарадинг на сервере (рис. [-@fig:9]). Убеждимся, что на клиенте доступен выход в интернет (доступен) (рис. [-@fig:10]).

![Возможность перенаправления пакетов](image/8.png){#fig:8 width=70%}

![Включение перенаправления пакетов и включение маскарадинга](image/9.png){#fig:9 width=70%}

![Браузер клиента](image/10.png){#fig:10 width=70%}

На ВМ `server` перехожу в каталог для внесения изменений в настройки внутреннего окружения `/vagrant/provision/server/` и копирую в соответствующие каталоги конфигурационные файлы (рис. [-@fig:11]).

![Внесение изменений в настройки внутреннего окружения](image/11.png){#fig:11 width=70%}

Создаю скрипт `firewall.sh` (рис. [-@fig:12]). 

![Создание скрипта firewall.sh](image/12.png){#fig:12 width=70%}

Для отработки созданного скрипта во время загрузки виртуальной машины server в конфигурационном файле Vagrantfile добавляем в разделе конфигурации для сервера следующую запись (рис. [-@fig:13]):

![Vagrantfile](image/13.png){#fig:13 width=70%}

# Выводы

В ходе лабораторной работы я получила навыки настройки межсетевого экрана в Linux в части переадресации портов и настройки Masquerading.

# Ответы на контрольные вопросы

1. Где хранятся пользовательские файлы firewalld? 

- В firewalld пользовательские файлы хранятся в директории `/etc/firewalld/`.

2. Какую строку надо включить в пользовательский файл службы, чтобы указать порт TCP 2022? 

- Для указания порта TCP 2022 в пользовательском файле службы, вы можете добавить строку в секцию port следующим образом:

`<port protocol="tcp" port="2022"/>`

3. Какая команда позволяет вам перечислить все службы, доступные в настоящее время на вашем сервере? 

- `firewall-cmd --get-services`

4. В чем разница между трансляцией сетевых адресов (NAT) и маскарадингом (masquerading)? 

- Разница между трансляцией сетевых адресов (NAT) и маскарадингом (masquerading)
заключается в том, что в случае NAT исходный IP-адрес пакета заменяется на IP-адрес маршрутизатора, а в случае маскарадинга используется маршрутизатора.

5. Какая команда разрешает входящий трафик на порт 4404 и перенаправляет его в службу ssh по IP-адресу 10.0.0.10? 

```
firewall-cmd --zone=public --add-port=4404/tcp --permanent
firewall-cmd --zone=public --add-forward-port=port=4404
            ↪:proto=tcp:toport=22:toaddr=10.0.0.10 --permanent
firewall-cmd --reload
```

6. Какая команда используется для включения маcкарадинга IP-пакетов для всех пакетов, выходящих в зону public? 

- `firewall-cmd --zone=public --add-masquerade --permanent`
- `firewall-cmd --reload`
