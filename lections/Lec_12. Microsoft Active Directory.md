# Microsoft Active Directory

# Темы, затронутые в лекции 12: 

1. [`Microsoft Active Directory`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#microsoft-active-directory-1)

1. [`Domain Services`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#domain-services)

1. [`Group Policy`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#group-policy)

1. [`Подключение клиентов`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BB%D0%B8%D0%B5%D0%BD%D1%82%D0%BE%D0%B2)

***

## Microsoft Active Directory.
###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-12)

Центральным компонентом Microsoft Active Directory (MS AD) является служба Domain Services.

Это иерархическая база данных, предназначенная для хранения информации о пользователях, компьютерах и других объектов в сети.

Эта база используется другими службами для аутентификации и авторизации пользователей при входе на рабочие станции и доступе к сетевым ресурсам. Кроме этого в MS AD входит компонент управления групповыми политиками (Group Policy) для автоматизации настроек операционных систем и окружения пользователей, служба управления сертификатами (Certificate Services), службу единого входа (Federation Services) и службу управления правами (Rights Management Services) для управления доступа к различным объектам информационных систем.

Federation Services позволяет организовать хранение учётных записей любых служб, даже не интегрированных с MS AD. Это позволяет авторизоваться в любых службах со всех компьютерах в домене, введя только один пароль от учётной записи.

Rights Management Services требует интеграции на уровне программного обеспечения, поэтому на данный момент поддерживается в ограниченном количестве программ.

Вместе с Certificate Services эти три службы расширяют возможности, но не являются обязательными для функционирования MS AD.

Несмотря на то, что MS AD рассчитана на использование в качестве клиентов и серверов только ОС Microsift, существуют реализации клиентов и серверов для GNU/Linux и MacOS X. Уровень поддерживаемого функционала этих решений сильно разнится, но как минимум позволяет авторизоваться на рабочей станции или в информационной системе используя учётную запись из домена MS AD.

## Domain Services.
###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-12)

Domaion Services представляет собой комбинацию из сетевых служб LDAP для хранения информации об объектах и Kerberos для аутентификации. 

Информация о политиках хранится в базе LDAP, сами политики представляют собой текстовые файлы на сетевом ресурсе, доступном всем пользователям домена. LDAP база является упрощённой реализацией распределённого каталога Х.500.

## Group Policy.
###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-12)

Групповые политики используются для централизованной настройки окружения пользователя, рабочих станций и серверов. Каждая групповая политика представляет собой тестовый файл с перечислением пунктов и значением настроек, которые могут быть применены.

Настройки можно разделить на две большие группы - для компьютеров и для пользователей. За применение настроек на локальной машине отвечает специальный клиент. Политики обновляются каждый раз при перезагрузке компьютера, при входе пользователя в систему, раз в примерно 2 часа или принудительно запуском утилиты gpupdate.exe.

Чтобы связать групповую политику с объектами MS AD используются организационные единицы (organizational unit). 

Это контейнеры в каталоге MS AD, позволяющие группировать другие объекты. Ближайшая аналогия для организационных единиц - каталоги на файловой системе, по которым группируются файлы. 

Главное применение организационных единиц - связывание сгруппированных в них объектов с действующими на них политиками. По аналогии с каталогами файловой системы, групповая политика действует на все объекты внутри организационной единицы и на все объекты во вложенных организационных единицах.

Для создания политик, внесения в них изменений и связывания с объектами каталога существует специальная оснастка в mmc консоли на сервере MS AD - Group Policy Management.

## Подключение клиентов.
###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-12)

Для ввода в домен нового компьютера потребуется корректно установленный контроллер домена.

Корректность его установки проверяется с помощью запуска утилиты dcdiag в командной строке. При отсутствии ошибок в выводе домен установлен корректно.

Наиболее частая ошибка при установке - некорректная настройка DNS сервера. Для работы MS AD желательно разрешить домен-контроллеру вносить изменения в DNS записи, в идеале иметь на каждом домен контроллере свой DNS сервер от MS. Если это не возможно, допускается ручная регистрация записей.

Для виртуальных машин в системе oVirt для корректной работы сети и службы DNS обязательно нужно выключить адресацию IPv6. Иначе всегда будет ошибка с невозможностью определения адреса домена.

Для каждого клиента в качестве DNS сервера должен быть установлен адрес домен-контроллера.

Для входа в домен потребуется учётная запись домена с правами, достаточными для этого действия. С настройками по умолчанию обычный пользователь может ввести в домен 3 компьютера, администратор без ограничений.

При подключении Linux в домен будет доступна централизованная аутентификация через базу домена и возможность локально использовать группы безопасности из домена. Групповые политики в Linux не поддерживаются. Существует два варианта включения Linxu в домен MS AD: с помощью sssd или winbind/samba.

###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/blob/main/lections/Lec_12.%20Microsoft%20Active%20Directory.md#%D1%82%D0%B5%D0%BC%D1%8B-%D0%B7%D0%B0%D1%82%D1%80%D0%BE%D0%BD%D1%83%D1%82%D1%8B%D0%B5-%D0%B2-%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-12)
