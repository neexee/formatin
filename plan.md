# Unix shell essential capabilities

Это небольшое руководство по основам командной строки и идеям Unix-like операционных систем.
В развёрнутом виде почти то же самое можно почитать [здесь](https://www.learnenough.com/command-line-tutorial).

Знание командной строки абсолютно необходимо опытному программисту. Некоторые из причин:
* Большинство консольных программ сделаны для людей, которые знают, что делают. Как правило, в них нет «защиты от дурака». Консольные программы обычно требуют минимум интерактивного взаимодействия. Нет никаких всплывающих раковых опухолей с сообщениями уровня «Обновитесь до версии 1.001». Поэтому использование командной строки часто экономит время и нервы.
* Программисты часто оказываются в ситуации, когда нужно проделать одинаковую последовательность действий над пачкой файлов. Писать отдельную программу, естественно, оверкилл. Если в GUI не предусмотрена нужная фича, придётся ходить по выпадающим меню и проделывать нужные операции вручную, что не сильно интересно, да ещё и отнимает кучу времени. Командная строка здесь может выручить, потому что легко автоматизируется. 
* Сделать что-то полезное в Вебе невозможно без знания командной строки. Фронтенд-разработчик не сможет запустить менеджер зависимостей (например, `npm`) и собрать свой код, бэкенд-разработчик не сможет сделать _почти ничего_.
* Множество книг по программированию подразумевают, что читатель умеет пользоваться командной строкой.
* Командная строка – основа философии Unix. Философией Unix пропитано всё в Интернете и Вебе.
* Командная строка – это море фана.

## Шелл
Типичный шелл Unix - интерпретатор специального языка программирования. Обычно шелл запускается в интерактивном режиме после того, как пользователь залогинился, а потом просто выполняет введённые пользователем команды. Типичная команда принимает аргументом путь к файлу и что-нибудь с делает c этим файлом.  
Справку по почти всем командам можно получить с помощью `man <команда>`.

## Файловая система #1
* Навигация по файловой системе: `cd`, `ls`, `pwd`, `mc`. Скрытые файлы.
* Операции с файлами и каталогами: `touch`, `cp`, `mv`, `rm`, `mkdir`.
* Просмотр файлов: `cat`, `less`. Обычно программу можно прервать по сигналу из шелла: `^C`.
* Редактирование файлов: `mcedit`.

Задания:
* Что произойдёт, если попытаться удалить непустой каталог?
* Каков полный путь до вашего домашнего каталога?
* Что делает команда `cd` без параметров?
* Чем `cat` отличается от `less`?
* Какие скрытые файлы и каталоги находятся в вашем домашнем каталоге?
* Создать файл, имя которого начинается с точки. Убедиться, что `ls` его не показывает.

## Полезные возможности шелла
* История. `⇅`, `history`, `^R`.
* Автокомплит. `⇆`.
* Передвижение по строке: `^A`, `^E`, `^W`.
* Очистка экрана. `^L`.

## Композиция программ #1
* Программы `head` `tail`.
* Программы `wc` и `nl`.
* Перенаправление вывода с помощью `>`, `>>`, `|`. `stdin` и `stderr`. `echo`.

Задания:
* Скачать текст «Робинзона Крузо» `wget http://factorized.net/crusoe.txt`.
* Распечатать строки с 5 по 10 из `crusoe.txt`.
* С помощью `>` и `>>` записать в текстовый файл фразу «Hello world!».
* Пересчитать файлы в `/usr/bin` с помощью пайпа из `ls -1` и `wc -l` (`nl`).

## Композиция программ #2
* Программы `find` и `grep`.
* Программа `sed`.

Задания:
* Найти все строки «Friday» в тексте.
* Найти все файлы `*.txt` в каталоге `/tmp`.
* Ищет ли `find` скрытые файлы и каталоги?
* Найти количество упоминаний слова «Friday» в `crusoe.txt`.
* Заменить в `crusoe.txt` все слова «Friday» на «Saturday».
* Попробовать найти все файлы `*.txt` на всём диске. Отфильтровать файлы по одному из критериев:
  * Содержание определённой подстроки в имени.
  * Размер файла.
  * Время создания файла.

## Файловая система #2
* Пользователи и группы в Unix. Программы `whoami`, `who` и `groups`.
* Права доступа к файлам и каталогам. Программы `chmod` и `chown`.

Задания:
* Создать в своём домашнем каталоге файл под названием `shared.txt`. Какими правами доступа он обладает? (Смотри `ls -la`).
* C помощью `chmod` сделать так, чтобы `shared.txt` был доступен только его владельцу и только на чтение.
* С помощью `chown` сделать вашего соседа справа владельцем файла `shared.txt`, затем вернуть соседу слева полученный от него файл.
* Допустим, `chmod` и `chown` можно запускать любому пользователю над любым файлом. Какие проблемы безопасности это имеет?

## Пайпы и процессы
* Процессы. Программы `ps`, `top` и `htop`.
* Коды возврата. `true` и `false`. `$?`.
* Программы `awk`, `sort` и `uniq`.

Задания:
* Посчитать число запущённых вами процессов с помощью `ps`, `grep` и `wc -l`.
* С помощью `ps`, `awk`, `sort` и `uniq` найти всех уникальных пользователей в системе, от имени которых запущен хотя бы один процесс.

## Всё есть файл
* `/proc`. `/proc/uptime`, `/proc/cpuinfo` и `/proc/{pid}/mem`.
* `/dev`. `/dev/sd*`, `/dev/urandom` и `/dev/null`.
* `/etc`. `/etc/hosts`, `/etc/passwd`, `/etc/fstab` и `/etc/cron.d`.
* `/tmp`. tmpfs

## Окружение
* Программы `which` и `whereis`.
* Программа `gcc`.
* Переменная окружения `$PATH`.

Задания:
* Выяснить, в каких каталогах находятся программы `ls` и `grep`.
* Написать программу `hello` («Hello, World!») на C, скомпилировать и запустить, находясь в том же каталоге. Запустить `hello` из другого каталога.
* Добавить каталог c `hello` в `$PATH` (`export PATH=$PATH:<новый каталог>`). Запустить `hello`.

## Сетевые основы
* IP: `ip` и `ifconfig`.
* ICMP: `ping`, `traceroute`.
* DNS: `dig` и `nslookup`.

Задания:
* Приведите пример использования `ping` и `traceroute`.
* Как проще всего определить IP-адрес у `yandex.ru`?

## vim
* Моды. Навигация.
* Копирование и вставка.
* Удаление строк, символов и слов.
* Замена строк.

## Скрипты на Bash
* shabang.
* `$N`, `$@`.
* `if`, `test` и `for`.

### Задание «Repeater»
Написать скрипт, выводящий на экран строку `Hello` указанное число раз.
```
$ ./repeat.sh 3
Hello
Hello
Hello
```
### Задание «Summator»
Написать скрипт, суммирующий два числа, переданных в качестве параметров командной строки.
```
$ ./add.sh 2 3
5
$ ./add.sh 10 15
25
```
### Задание «Roulette»
Написать русскую рулетку для файлов с помощью переменной `$RANDOM` и программы `rm`. Револьвер шестизарядный, патрон нужно заряжать один.
```
$ ./roulette.sh main.c
Maybe next time
```

## Регулярные выражения.
* Синтаксис регулярных выражений.

### Задание «Warmup»
С помощью `egrep` и регулярных выражений найти в `http://factorized.net/crusoe.txt`:

* Все слова, начинающиеся на 'z'.
* Все слова из 16 букв.
* Все слова, начинающиеся на 'a' и заканчивающиеся на 'c'.
* Все слова, начинающиеся на 'ab', у которых третья буква не 'o'.

Словом считать любую последовательность символов, ограниченную с двух сторон пробельными символами, либо следующими знаками препинания: `.,;>?!'"`.

### Задание «Sequences»
Найти в файле `http://factorized.net/patterns.txt` строки, которые:
* Cостоят только из цифр.
* Cостоят только из букв.

### Задание «License plates»
Найти в `patterns.txt` все строки, которые могут являться валидными российскими автомобильными номерами (используя заглавные английские буквы). В российских автомобильных номерах могут использоваться только буквы, имеющие латинские графические аналоги: А, В, Е, К, М, Н, О, Р, С, Т, У и Х.

Валидным номером считается следующая комбинация:
* буква
* три цифры
* две буквы
* две или три цифры

Примеры валидных номеров: `В532OT154`, `X151BT00`, `Y010MK999`.
