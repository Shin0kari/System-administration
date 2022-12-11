# Выполнения задач в Linux по расписанию.

***

Для выполнения задач в Linux по расписанию используется служба cron или утилита at.

Утилита at запускает задачи не по расписанию, а в заданное время один раз. Но при администрировании иногда удобно сделать отложенный запуск команды. Кроме того, при использовании этой утилиты команда будет выполняться польность в том же окружении, где работал системный администратор при формировании задания

Синтаксис запуска:

`at 11:01`

После этого откроется консоль, в которую надо будет ввести команды, которые необходимо выполнить в это время. После ввода команд нужно нажать комбинацию клавишь `Ctrl-D`

Работа со службой cron несколько сложнее, потому что нужно знать правила описания времени запуска.

В cron можно использовать только 1 команду и запуск производится из упрощённого окружения. 

Для взаимодействия со службой используется утилита crontab. С параметром -l она печатает очередь  регулярных заданий для текущего пользователя, с параметром -e запускает текстовый редактор для их редактирования.

Для каждого задания на отдельной строчке записывается время, когда оно будет выполняться и сама команда. Весь вывод команды будет выслан администратору на электронную почту. Чтобы этого не происходило, можно добавить к команде перенаправление в /dev/null.

Время задаётся в формате: минуты, часы, день месяца, месяц, день недели. Каждое из этих полей может принимать конкретное числовое значение (0 и 7 соответствуют воскресенью); * - любое значение (т.е. каждое целое число); `*`/5 - каждое целое количество, кратное 5; либо список 1,4,10. Разделяются поля пробелом или символом табуляции.

`*/5 * * 1 1,3,5 /root/backup.sh > /dev/null > 1>&2`

В приведённом примере скрипт /root/backup.sh будет выполняться каждые 5 минут каждый час, каждый день первого месяца (январь) в понедельник, среду и пятницу.

###### [`Вернутся вверх`](https://github.com/Shin0kari/System-administration/new/main/lections#%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B7%D0%B0%D0%B4%D0%B0%D1%87-%D0%B2-linux-%D0%BF%D0%BE-%D1%80%D0%B0%D1%81%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D1%8E)