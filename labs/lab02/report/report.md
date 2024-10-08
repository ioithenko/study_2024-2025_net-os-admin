---
## Front matter
title: "Отчёт по лабораторной работе №2"
subtitle: "Администрирование сетевых подсистем"
author: "Ищенко Ирина Олеговна"

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

Приобретение практических навыков по установке и конфигурированию DNSсервера, усвоение принципов работы системы доменных имён.

# Выполнение лабораторной работы

Загрузим нашу операционную систему и перейдем в рабочий каталог с
проектом:
cd /var/tmp/ioithenko/vagrant
Далее запустим виртуальную машину server:
vagrant up server (рис. [-@fig:001]).

![Запуск ВМ](image/1.png){#fig:001 width=70%}

Перейдём в режим суперпользователя:
sudo -i
И установим bind и bind-utils (рис. [-@fig:002]):
dnf -y install bind bind-utils

![Установка bind](image/2.png){#fig:002 width=70%}

С помощью утилиты dig сделаем запрос к DNSадресу www.yandex.ru (рис. [-@fig:003]):
dig www.yandex.ru

![dig](image/3.png){#fig:003 width=70%}

Просмотрим содержание файлов /etc/resolv.conf, /etc/named.conf
(рис. [-@fig:004]), /var/named/named.ca (рис. [-@fig:005]), /var/named/named.localhost,
/var/named/named.loopback (рис. [-@fig:006]).

![named.conf](image/4.png){#fig:004 width=70%}

![named.ca](image/5.png){#fig:005 width=70%}

![named.localhost](image/6.png){#fig:006 width=70%}

Запустим DNS-сервер:
systemctl start named
Включим запуск DNS-сервера в автозапуск при загрузке системы (рис. [-@fig:007]):
systemctl enable named

![Запуск сервера](image/7.png){#fig:007 width=70%}

dig @127.0.0.1 www.yandex.ru. Выводится более подробная информация (рис. [-@fig:008]):

![dig](image/8.png){#fig:008 width=70%}

Сделаем DNS-сервер сервером по умолчанию для хоста `server` и внутренней виртуальной сети. Для этого требуется изменить настройки сетевого соединения `eth0` в NetworkManager, переключив его на работу с внутренней сетью и указав для него
в качестве DNS-сервера по умолчанию адрес `127.0.0.1` (рис. [-@fig:9]).

Перезапускаем NetworkManager и проверяем наличие изменений в файле `/etc/resolv.conf` (рис. [-@fig:10]).

![Изменение настроек сетевого соединения `eth0`](image/9.png){#fig:9 width=80%}

![Перезапуск NetworkManager и просмотр файла](image/10.png){#fig:10 width=70%}

Вносим изменения в файл `/etc/named.conf`  (рис. [-@fig:11]).

![Внесение изменений в файл `/etc/named.conf`](image/11.png){#fig:11 width=70%}

Вносим изменения в настройки межсетевого экрана узла `server`, разрешив работу с DNS. Убеждаемся, что DNS-запросы идут через узел `server`, который прослушивает порт 53 (рис. [-@fig:12]).

![Внесение изменений в настройки межсетевого экрана узла `server`, проверка](image/12.png){#fig:12 width=70%}

Для конфигурирования кэширующего DNS-сервера при наличии фильтрации DNS-запросов маршрутизаторами вносим изменения в файл `named.conf` (рис. [-@fig:13])

![Редактирование `named.conf`](image/13.png){#fig:13 width=70%}

Вводим команды(рис. [-@fig:14]):
cp /etc/named.rfc1912.zones /etc/named/
cd /etc/named
mv /etc/named/named.rfc1912.zones /etc/named/ioithenko.net

![Команды](image/14.png){#fig:14 width=70%}


Включаем файл описания зоны `/etc/named/ioithenko.net` в конфигурационном файле
DNS `/etc/named.conf`, добавив в нём в конце строку:
`include "/etc/named/ioithenko.net";`. 

Редактируем файл `/etc/named/ioithenko.net` (рис. [-@fig:15])

![Редактирование файла `/etc/named/ioithenko.net`](image/15.png){#fig:15 width=70%}

В каталоге `/var/named` создаем подкаталоги `master/fz` и `master/rz`, в которых будут
располагаться файлы прямой и обратной зоны соответственно. Копируем шаблон прямой DNS-зоны `named.localhost` из каталога `/var/named` в каталог `/var/named/master/fz`, переименовав его в `ioithenko.net` (рис. [-@fig:16]).

![Создание каталогов, копирование шаблона прямой зоны, переименование](image/17.png){#fig:16 width=70%}

Изменяем файл `/var/named/master/fz/ioithenko.net` (рис. [-@fig:17]).

![Редактирование `/var/named/master/fz/ioithenko.net` ](image/18.png){#fig:17 width=70%}

Копируем шаблон обратной DNS-зоны `named.loopback` из каталога
`/var/named` в каталог `/var/named/master/rz` и переименуйте его в `192.168.1` (рис. [-@fig:18]).

![Копирование шаблона обратной зоны, переименование](image/19.png){#fig:18 width=70%}

Изменяем файл `/var/named/master/rz/192.168.1` (рис. [-@fig:19]).

![Редактирование `/var/named/master/rz/192.168.1`](image/20.png){#fig:19 width=70%}

Изменяем права доступа, восстанавливаем метки SELinux, проверяем (рис. [-@fig:20]).

![Изменение прав доступа, восстановление меток SELinux, проверка](image/21.png){#fig:20 width=70%}

Во втором терминале открываем лог системных сообщений. В первом терминале перезапускаем DNS-сервер. После исправления всех ошибок и опечаток DNS-сервер запускается успешно.
При помощи утилиты `dig` получаем описание DNS-зоны с сервера `ns.ioithenko.net` (рис. [-@fig:21]).

![Описание DNS-зоны с сервера `ns.ioithenko.net`](image/22.png){#fig:21 width=70%}

Анализируем корректность работы DNS-сервера (рис. [-@fig:22]),  (рис. [-@fig:23]),  (рис. [-@fig:24]).

![Анализ корректности работы DNS-сервера](image/23.png){#fig:22 width=70%}

![Анализ корректности работы DNS-сервера](image/24.png){#fig:23 width=70%}

![Анализ корректности работы DNS-сервера](image/25.png){#fig:24 width=70%}

Переходим в каталог для внесения изменений в настройки внутреннего окружения `/vagrant/provision/server/`, создаем в нём каталог `dns`, в который помещаем в соответствующие каталоги конфигурационные файлы DNS (рис. [-@fig:25]).

![Размещение конфигурационных файлов в каталог /vagrant/provision/server/dns](image/26.png){#fig:25 width=70%}

Создаем скрипт `dns.sh` (рис. [-@fig:26]).

![Редактирование скрипта dns.sh](image/27.png){#fig:26 width=70%}

Для отработки созданного скрипта во время загрузки виртуальной машины
в конфигурационном файле `Vagrantfile` вносим изменения в разделе конфигурации для сервера (рис. [-@fig:27]).

![Редактирование Vagrantfile](image/28.png){#fig:27 width=70%}

# Выводы

В ходе лабораторной работы я приобрела практические навыки по установке и конфигурированию DNSсервера, усвоила принципы работы системы доменных имён.

# Ответы на контрольные вопросы

1. Что такое DNS? 

DNS - это система, предназначенная для преобразования человекочитаемых доменных имен в IP-адреса компьютерами для идентификации друг друга в сети.

2. Каково назначение кэширующего DNS-сервера? 

Задача сервера - хранить результаты предыдущих DNS-запросов в памяти. Когда клиент делает запрос, кэширующий DNS проверяет свой кэш, и если он содержит соответствующую информацию, сервер возвращает ее без необходимости обращаться к другим DNS-серверам. Это ускоряет процесс запроса.

3. Чем отличается прямая DNS-зона от обратной? 

Прямая зона преобразует доменные имена в IP-адреса, обратная зона выполняет обратное: преобразует IP-адреса в доменные имена.

4. В каких каталогах и файлах располагаются настройки DNS-сервера? Кратко охарактеризуйте, за что они отвечают. 

В Linux-системах обычно используется файл /etc/named.conf для общих настроек. Зоны хранятся в файлах в каталоге /var/named/, например, /var/named/example.com.zone.

5.	Что указывается в файле resolv.conf? 

Содержит информацию о DNS-серверах, используемых системой, а также о параметрах конфигурации.

6.	Какие типы записи описания ресурсов есть в DNS и для чего они используются? 

A (IPv4-адрес), AAAA (IPv6-адрес), CNAME (каноническое имя), MX (почтовый сервер), NS (имя сервера), PTR (обратная запись), SOA (начальная запись зоны), TXT (текстовая информация).

7.	Для чего используется домен in-addr.arpa? 

Используется для обратного маппинга IP-адресов в доменные имена.

8.	Для чего нужен демон named? 

Это DNS-сервер, реализация BIND (Berkeley Internet Name Domain).

9.	В чём заключаются основные функции slave-сервера и master-сервера? 

Master-сервер хранит оригинальные записи зоны, slave-серверы получают копии данных от master-сервера.

10.	Какие параметры отвечают за время обновления зоны? 

refresh, retry, expire и minimum.

11.	Как обеспечить защиту зоны от скачивания и просмотра? 

Это может включать в себя использование TSIG (Transaction SIGnatures) для аутентификации между серверами.

12.	Какая запись RR применяется при создании почтовых серверов? 

MX (Mail Exchange).

13.	Как протестировать работу сервера доменных имён? 

Используйте команды nslookup, dig или host.

14.	Как запустить, перезапустить или остановить какую-либо службу в системе? 

systemctl start|stop|restart <service>.

15.	Как посмотреть отладочную информацию при запуске какого-либо сервиса или службы? 

Использовать опции -d или -v при запуске службы.

16.	Где хранится отладочная информация по работе системы и служб? Как её посмотреть?

В системных журналах, доступных через journalctl.
 
17.	Как посмотреть, какие файлы использует в своей работе тот или иной процесс? Приведите несколько примеров. 

lsof -p <pid> или fuser -v <file>.

18.	Приведите несколько примеров по изменению сетевого соединения при помощи командного интерфейса nmcli. 

Примеры включают nmcli connection up|down <connection_name>.

19.	Что такое SELinux? 

Это мандатный контроль доступа для ядра Linux.

20.	Что такое контекст (метка) SELinux? 

Метка, определяющая, какие ресурсы могут быть доступны процессу или объекту.

21.	Как восстановить контекст SELinux после внесения изменений в конфигурационные файлы? 

restorecon -Rv <directory>.

22.	Как создать разрешающие правила политики SELinux из файлов журналов, содержащих сообщения о запрете операций? 

Использовать audit2allow.

23.	Что такое булевый переключатель в SELinux? 

Это параметр, который включает или отключает определенные аспекты защиты SELinux.

24.	Как посмотреть список переключателей SELinux и их состояние? 

getsebool -a.

25.	Как изменить значение переключателя SELinux? 

setsebool -P <boolean_name> <on|off>.