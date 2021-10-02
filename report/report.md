---
# Front matter
title: "Информационная безопасность."
subtitle: "Лабораторная работа №2."
author: "Филиппова Вероника Сергеевна"

# Generic otions
lang: ru-RU
toc-title: "Содержание"

# Bibliography

# Pdf output format
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n
polyglossia-lang:
  name: russian
  options:
  - spelling=modern
  - babelshorthands=true
polyglossia-otherlangs:
  name: english
### Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
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
## Misc options
indent: true
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получение практических навыков работы в консоли с атрибутами файлов, закрепление теоретических основ дискреционного разграничения доступа в современных системах с открытым кодом на базе ОС Linux

# Задание

1) Выполнить пункты по порядку выполнения работы
2) Заполнить таблицу с правами доступа 
3) Заполнить таблицу с минимальными правами для совершения операций


# Выполнение лабораторной работы

1. С помощью команды 'useradd guest' создала учетную запись гостя. 
2. Задала пароль для пользователя \guest\ командой 'passwd guest' 

![Создание учетной записи гостя $\label{fig1}$](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/1.jpg){ #fig:001 width=70% }

3. Зашла от имени пользователя \guest\.

![Учетная запись guest](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/2.jpg){ #fig:002 width=70% }

4. Определила директорию комндой `pwd`. Получила директорию `/home/guest` , которая является домшней директорией пользователя guest.

![Результат вывода команды `pwd`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/3.jpg){ #fig:003 width=70% }

5. Уточнила имя пользователя командой `whoami`.

![Результат команды `whoami`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/4.jpg){ #fig:004 width=70% }


6. Уточнила имя пользователя, его группу, а также группы, куда входит пользователь, командой `id`. Также выполнила команду `groups`. Эта команда выводит название группы, команда `id` даёт расширенную информацию.

![Результат команды `id`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/5.jpg){ #fig:005 width=70% }

![Результат команды `groups`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/6.jpg){ #fig:006 width=70% }

7. Имя пользователя \guest\  было получено с помощью пунктов 5 и 6

8. Просмотрела файл `/etc/passwd` командой `cat /etc/passwd`. Нашла в нём свою учетную запись, определил uid  = 501 и gid = 501, эти значения совпадают со значениями, полученными ранее.

![Результат команды `cat /etc/passwd`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/7.jpg){ #fig:007 width=70% }

Получила данные о пользователе с помощью команды `cat /etc/passwd | grep guest`

![Результат команды `cat /etc/passwd | grep guest`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/8.jpg){ #fig:008 width=70% }

9. Определила существующие в системе директории командой `ls -l /home/`. Удалось получить список поддиректорий, на директориях установлены все права только для владельца.

![Результат команды `ls -l /home/`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/9.jpg){ #fig:009 width=70% }

10. Проверила, какие расширенные атрибуты установлены на поддиректориях, находящихся в директории `/home`, командой: `lsattr /home`. Для пользователя guest был получен вывод.

![Результат команды `lsattr /home/`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/10.jpg){ #fig:010 width=70% }

11. Создала в домашней директории поддиректорию dir1 командой `mkdir dir1`. 

![Результат команды `mkdir dir1`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/12.jpg){ #fig:011 width=70% }

12. Сняла с директории dir1 все атрибуты командой `chmod 000 dir1`, и проверил её с помощью команды `ls -l`

![Результат команды `mkdir dir1` и `ls -l`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/13.jpg){ #fig:012 width=70% }

13. Попыталась создать в директории dir1 файл file1 командой `echo "test" > /home/guest/dir1/file1`. Недостаточно прав даже для чтения. Командой `ls -l /home/guest/dir1` не удалось узнать, создался ли файл, потому что на папке установлены нулевые права.

![Результат команды `echo "test" > /home/guest/dir1/file1`](https://github.com/vsfilippova/Lab02InfS/blob/main/scr/14.jpg){ #fig:013 width=70% }

14. Заполнила таблицу 2.1. "Установленные права и разрешённые действия". 

|Пр дир                   |Пр ф|Созд ф|Уд ф|Зап в ф|Чт ф|Смена дир|Просм ф-в в дир|Переим ф|См атриб ф|
|-------------|----|------|----|-------|----|---------|---------------|--------|----------|
|000                      |000 |-     |-   |-      |-   |-        |-              |-       |-         |
|100                      |000 |-     |-   |-      |-   |+        |-              |-       |+         |
|300                      |000 |+     |+   |-      |-   |+        |-              |+       |+         |
|700                      |000 |+     |+   |-      |-   |+        |+              |+       |+         |
|010                      |000 |-     |-   |-      |-   |-        |-              |-       |-         |
|030                      |000 |-     |-   |-      |-   |-        |-              |-       |-         |
|070                      |000 |-     |-   |-      |-   |-        |-              |-       |-         |
|710                      |000 |+     |+   |-      |-   |+        |+              |+       |+         |
|730                      |000 |+     |+   |-      |-   |+        |+              |+       |+         |
|770                      |000 |+     |+   |-      |-   |+        |+              |+       |+         |
|000                      |100 |-     |-   |-      |-   |-        |-              |-       |-         |
|100                      |100 |-     |-   |-      |-   |+        |-              |-       |+         |
|300                      |100 |+     |+   |-      |-   |+        |-              |+       |+         |
|700                      |100 |+     |+   |-      |-   |+        |+              |+       |+         |
|010                      |100 |-     |-   |-      |-   |-        |-              |-       |-         |
|030                      |100 |-     |-   |-      |-   |-        |-              |-       |-         |
|070                      |100 |-     |-   |-      |-   |-        |-              |-       |-         |
|710                      |100 |+     |+   |-      |-   |+        |+              |+       |+         |
|730                      |100 |+     |+   |-      |-   |+        |+              |+       |+         |
|770                      |100 |+     |+   |-      |-   |+        |+              |+       |+         |
|000                      |300 |-     |-   |-      |-   |-        |-              |-       |-         |
|300                      |300 |+     |+   |+      |-   |+        |-              |+       |+         |
|100                      |300 |-     |-   |+      |-   |+        |-              |-       |+         |
|700                      |300 |+     |+   |+      |-   |+        |+              |+       |+         |
|010                      |300 |-     |-   |-      |-   |-        |-              |-       |-         |
|030                      |300 |-     |-   |-      |-   |-        |-              |-       |-         |
|070                      |300 |-     |-   |-      |-   |-        |-              |-       |-         |
|710                      |300 |+     |+   |+      |-   |+        |+              |+       |+         |
|730                      |300 |+     |+   |+      |-   |+        |+              |+       |+         |
|770                      |300 |+     |+   |+      |-   |+        |+              |+       |+         |
|000                      |700 |-     |-   |-      |-   |-        |-              |-       |-         |
|100                      |700 |-     |-   |+      |+   |+        |-              |-       |+         |
|300                      |700 |+     |+   |+      |+   |+        |-              |+       |+         |
|700                      |700 |+     |+   |+      |+   |+        |+              |+       |+         |
|010                      |700 |-     |-   |-      |-   |-        |-              |-       |-         |
|030                      |700 |-     |-   |-      |-   |-        |-              |-       |-         |
|070                      |700 |-     |-   |-      |-   |-        |-              |-       |-         |
|710                      |700 |+     |+   |+      |+   |+        |+              |+       |+         |
|730                      |700 |+     |+   |+      |+   |+        |+              |+       |+         |
|770                      |700 |+     |+   |+      |+   |+        |+              |+       |+         |
|000                      |710 |-     |-   |-      |-   |-        |-              |-       |-         |
|100                      |710 |-     |-   |+      |+   |+        |-              |-       |+         |
|300                      |710 |+     |+   |+      |+   |+        |-              |+       |+         |
|700                      |710 |+     |+   |+      |+   |+        |+              |+       |+         |
|010                      |710 |      |    |       |    |         |               |        |          |
|030                      |710 |      |    |       |    |         |               |        |          |
|070                      |710 |      |    |       |    |         |               |        |          |
|710                      |710 |      |    |       |    |         |               |        |          |
|730                      |710 |      |    |       |    |         |               |        |          |
|770                      |710 |      |    |       |    |         |               |        |          |
|000                      |730 |      |    |       |    |         |               |        |          |
|100                      |730 |      |    |       |    |         |               |        |          |
|300                      |730 |      |    |       |    |         |               |        |          |
|700                      |730 |      |    |       |    |         |               |        |          |
|010                      |730 |      |    |       |    |         |               |        |          |
|030                      |730 |      |    |       |    |         |               |        |          |
|070                      |730 |      |    |       |    |         |               |        |          |
|710                      |730 |      |    |       |    |         |               |        |          |
|730                      |730 |      |    |       |    |         |               |        |          |
|770                      |730 |      |    |       |    |         |               |        |          |
|000                      |770 |-     |-   |-      |-   |-        |-              |-       |-         |




15. Заполнила таблицу 2.2 "Минимальные права для совершения операций" .

|Операция                 |Мин пр на дир|Мин пр на ф|
|-------------------------|-------------------------|-------------------|
|Создание файла           |wx                       |rw (default when crating the file)|
|Удаление файла           |wx                             |w                        |
|Чтение файла             |x                              |r                        |
|Запись в файл            |x                              |w                        |
|Переименование файла     |wx                       |- - -                    |
|Создание поддиректории   |wx                       |- - -                    |
|Удаление поддиректории   |wx                       |- - -                    |

# Выводы

Получила практические навыки работы в консоли с атрибутами файлов, закрепил теоретические основы дискреционного разграничения доступа в современных системах с открытым кодом на базе ОС Linux.

