# Стандарты на расположение каталогов файловой системы
# Темы, затронутые в лекции 3: 

1. [`Круг обязанностей системного администратора`](https://github.com/Shin0kari/System-administration/new/main/lections#windows)
1. [`Круг обязанностей системного администратора`](https://github.com/Shin0kari/System-administration/new/main/lections#linux)

***

## Windows.
###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/new/main/lections#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-3)

Рассмотрим настройки по умолчанию.
Важно помнить: **прописные и строчные буквы в Windows в названиях каталогов и переменных окружения не различаются**

Сама ОС устанавливается в каталог "c:\Windows". 
Переменная окружения, соответствующая этому каталогу %SystemRoot%. 

В этом каталоге содержится ядро ОС, драйверы и основные службы. 

Устанавливаемые программы обычно копируются в каталог "c:\Program Files" (%ProgramFiles%) или "c:\Program Files (x86)" 
(%ProgramFiles(x86)%) дял 32-х разрядных программ в 64-х разрядной ОС. 

Профили пользователей располагаются в каталоге "c:\Users".
Напрямую этому каталогу не назначена никакая переменная окружения. 
Но для каждого пользователя есть путь к его профилю, расположенному в этой папке - %UserProfile%.

Каталог для временных файлов есть глобальный "%SystemRoot%/temp", 
но обычным пользователям он не доступен и индивидуальный для каждого пользователя в его профиле - 
"%USERPROFILE%\AppData\Local\Temp". Ему соответствует две переменные окружения - %TEMP% и %TMP%.

Загрузчик ОС обычно выносится на отдельный раздел, но может создавать для себя каталог "c:\Boot" на системном диске. 

Кроме видимых пользователям каталогов есть несколько скрытых, располагающихся на каждом диске. 

Это "$RecycleBin" - корзина, куда копируются удаляемые файлы и "$System Volume Information", 
которая хранит часть служебной информации о файловой системе на разделе и мгновенные снимки раздела.

Из важных файлов, располагаемых на системном диске нужно знать загрузчик - bootmgr 
(загрузчик, вместе с каталогом boot может быть вынесен на другой раздел); 
pagefile.sys - файл подкачки, используемый для расширения объёма оперативной памяти и hiberfile.sys, 
используемый для перехода компьютер в глубокий сон.

Для устанавливаемых в Windows программ нет каких-то чётких соглашений на размещение их файлов, 
кроме расположения в одном общем каталоге. 
Внутри своего каталога программа может располагать файлы и каталоги как угодно.

## Linux.
###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/new/main/lections#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-3)

Правила, которые придерживаются всеми дистрибутивами:

Важно помнить: **прописные и строчные буквы в Linux в названиях каталогов и переменных окружения различаются**

**"/bin"** - каталог с исполняемыми файлами основных утилит, 
доступных пользователям. 

Кроме него есть каталог "/usr/bin", в который помещаются исполняемые файлы. 

Аналогичные 2 каталоги используются для хранения исполняемых файлов системных утилит - **"/sbin" и "/usr/sbin"**. 

**Каталог "/etc/"** используется для хранения файлов настроек системы и служб. 
В нём могут быть подкаталоги для отдельных служб.

Файлы настроек в Linux представляют из себя обычные текстовые файлы.

**Каталог /home** используется для хранения профилей пользователей. 

Для каждого создаётся своя отдельная папка, по умолчанию кроме неё пользователь никуда сохранять свои файлы не может.

**Каталог /lib** используется для хранения общих библиотек и модулей ядра.

**Каталог /usr** хранит большую часть файлов установленных программ. 
Кроме исполняемых файлов в нём хранятся дополнительные библиотеки (/usr/lib), 
файлы данных (/usr/share) и документация для программ (/usr/doc).

**Каталог /var** используется для хранения изменяемых данных.

Журналы системы и работы программ хранятся в **каталоге /var/log**.

Файлы субд mysql в **/var/lib/mysql**.

Файлы с идентификаторами запущенных процессов служб в **/var/run**.

Каталог /srv должен использоваться для данных, которые используются для работы серверных служб (веб серверы, ftp и прочее). 
Но ряд дистрибутивов может отходить от этого правила, например в debian данные веб сервера хранятся в /var/www.

Временные файлы всех пользователей хранятся в одном каталоге - /tmp. 
С одной тсороны это создаёт сложности с распределением прав в этом каталоге для защиты данных пользователей, 
с другой стороны позволяет использовать для этого каталога быстрое устройство хранения для ускорения работы.

Перечисленные выше каталоги хранят обычные файлы. 

Кроме них в linux присутствует несколько каталогов со специальными фалами:

**/dev** - содержит файлы устройств.

**/proc** - содержит файлы, соответствующие процессам и текущим настройкам ядра
**/sys** - используется для доступа к ресурсам ядра.

###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/new/main/lections#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-3)