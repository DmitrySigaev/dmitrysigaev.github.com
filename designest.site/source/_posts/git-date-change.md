title: git. How to change the date of your commit.
date: 2016-01-22 10:58:49
tags: Git.
---

Так случилось, что я решил себя заставить каждый день что-нибудь в носить в свой сайт.
Сайт у меня хоститься на бесплатном ресурсе GitHUB. Там легко проследить историю коммитов.
Но если что-то пошло не так, то трудно потом себя превозмоч и продолжить все в том же ключе.
Т.е. продолжать постить как и задумал - каждый божий день. Но твоя история коммитов будет
тебе говорить что ты - бездорь и не выполняешь свои обещанию. Чтобы успокоить свои нервы и
все испарвить разработчики git'a придумали как все исправить. тут я привиду пример такоей правки.

Так как обычный человек редко стакивается с терминальный окном, это пост расчитан как
раз на обычного пользователя windows. Все превыкли наводить мышкой на файл в проводнике,
нажимать правую кнопку мыши и смотрить свойсва файла. И те кто раньше может пользовался линкусом,
так сказать, лет 20 назад, уже забыли что нужно просто набрать команду (stat)[mingw32/stat.md].

```
$ stat git-date-change.md
  File: 'git-date-change.md'
  Size: 1846            Blocks: 4          IO Block: 65536  regular file
Device: c04ef804h/3226400772d   Inode: 3377699720973401  Links: 1
Access: (0644/-rw-r--r--)  Uid: (1062029/Dmitry_Sigaev)   Gid: (1049089/Domain Users)
Access: 2016-01-25 18:04:51.339701300 +0300
Modify: 2016-01-25 19:02:09.077443700 +0300
Change: 2016-01-25 19:02:09.077443700 +0300
 Birth: 2016-01-25 18:04:51.339701300 +0300

``` 
Или кратко:

```
$ stat -c %y git-date-change.md
2016-01-25 19:03:54.037367200 +0300

```                       
Незнаю как в других средах, но mingw32 поставляемый с Git работает с локалными переменными.
Поэтому я покажу сейчас как легко можно использовать данные локальные переменные для своих целей.

Вот например, я ставлю себе задачу:
Исправить текущей дату создания 'git-date-change.md' файла на дату соответсвующей месечной давности.
Другими словами мне нужно поменять месяц создания файла. 

Приступим:
записываем в current_date дату 
$  current_date=$(stat -c %y git-date-change.md)
Другими словами, в коммандной строке набираем выше приведенный текст и нажимаем enter.
проверяем дату:
$echo $current_date
2016-01-25 19:05:40.999021600 +0300
Таким образом, получил в current_date дату 2016-01-25 19:05:40.999021600 +0300

Исправлять дату файла мы будем с помощью комманды (touch)[mingw32/touch.md]. Что дословно
переводится как прикосновение. add a touch of vinegar. Добавить ноку уксуса. т.е в значении: a small amount; a trace.
а если использвать как глагол, то: come so close to (an object) as to be or come into contact with it.
Для тех кто любит углубляться в английский смотрите занчение (touch)[vocabulary.engaud.com/touch]

Так как я считаю, что нужно все делать маленькими шагами и каждый такой шаг проверять, то
я предлагаю создать новую переменную $new_date:
```
$ new_date=$(date -d "$current_date - 1 month" --rfc-2822)
```
Разберемся, что в этой строке делается. 
1. Смотрим спавку по комманде (date)[mingw/date.md] (здесь)[mingw/date.md].
2. в двойных ковычках из $current_date считывается время и затем отнимается один месяц.
3. операция 2. скармливается команде 1. (date)[mingw/date.md] через опцию -d.
4. далее команда 1. (date)[mingw/date.md] обрабатывает 3. и выдает строку в формате rfc-2822

Результат можно проверить:

```
$ echo $new_date
Fri, 25 Dec 2015 19:05:40 +0300

```
Выше приведенное значение соответсвует формату. смотри тег.
  -R, --rfc-2822            output date and time in RFC 2822 format.
                            Example: Mon, 07 Aug 2006 12:34:56 -0600

Далее скармливаем $new_date переменную комманде (touch)[mingw32/touch.md] следующим образом:

```
$ touch -d "$new_date" git-date-change.md

``` 

Смотрим что было до и что стало после:

```
$ stat git-date-change.md
  File: 'git-date-change.md'
  Size: 5638            Blocks: 8          IO Block: 65536  regular file
Device: c04ef804h/3226400772d   Inode: 3377699720973401  Links: 1
Access: (0644/-rw-r--r--)  Uid: (1062029/Dmitry_Sigaev)   Gid: (1049089/Domain Users)
Access: 2016-01-25 18:04:51.339701300 +0300
Modify: 2016-01-25 20:36:55.276689200 +0300
Change: 2016-01-25 20:36:55.276689200 +0300
 Birth: 2016-01-25 18:04:51.339701300 +0300


$ touch -d "$new_date" git-date-change.md

$ stat git-date-change.md
  File: 'git-date-change.md'
  Size: 5638            Blocks: 8          IO Block: 65536  regular file
Device: c04ef804h/3226400772d   Inode: 3377699720973401  Links: 1
Access: (0644/-rw-r--r--)  Uid: (1062029/Dmitry_Sigaev)   Gid: (1049089/Domain Users)
Access: 2015-12-25 19:05:40.000000000 +0300
Modify: 2015-12-25 19:05:40.000000000 +0300
Change: 2016-01-25 20:37:42.908028600 +0300
 Birth: 2016-01-25 18:04:51.339701300 +0300
```
Поменялась дата модификации файла.

Давайте теперь перейдем к сути топика, т.е. сделаем коммит в git.

```
$ git add git-date-change.md
```

Смотрим статус:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   git-date-change.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        mingw32/
```
Исправляем дату коммита:
```
$ git commit --date="$new_date" -m "How to change date of commit"
[master 4bce82a] How to change date of commit
 Date: Fri Dec 25 19:05:40 2015 +0300
 1 file changed, 122 insertions(+)
 create mode 100644 designest.site/source/_posts/git-date-change.md
```
Смторим в лог гита:
```
$ git --no-pager log -1 --stat --pretty=fuller
commit 4bce82af9122ba1f497b13e9cfd0863eacb05662
Author:     Dmitry Sigaev <Dmitry_Sigaev@epam.com>
AuthorDate: Fri Dec 25 19:05:40 2015 +0300
Commit:     Dmitry Sigaev <Dmitry_Sigaev@epam.com>
CommitDate: Mon Jan 25 20:52:00 2016 +0300

    How to change date of commit

 designest.site/source/_posts/git-date-change.md | 122 ++++++++++++++++++++++++
 1 file changed, 122 insertions(+)
```
Правим дату последнего коммит без правки комминтария к комиту

```
$ git commit --amend --date="$new_date" -C HEAD
[master 9a5f902] How to change date of commit
 Date: Fri Dec 25 19:05:40 2015 +0300
 1 file changed, 122 insertions(+)
 create mode 100644 designest.site/source/_posts/git-date-change.md

```
Опять смотрим лог:
```
$ git --no-pager log -1 --stat --pretty=fuller
commit 9a5f9025ed3d399d5f1ba324bb08db1357442cd1
Author:     Dmitry Sigaev <Dmitry_Sigaev@epam.com>
AuthorDate: Fri Dec 25 19:05:40 2015 +0300
Commit:     Dmitry Sigaev <Dmitry_Sigaev@epam.com>
CommitDate: Mon Jan 25 20:55:49 2016 +0300

    How to change date of commit

 designest.site/source/_posts/git-date-change.md | 122 ++++++++++++++++++++++++
 1 file changed, 122 insertions(+)
```
Как видно CommitDate остается прежним.
Я бы хотел бы поправить и эту запись. Поэтому правим:
```
$  GIT_COMMITTER_DATE="$new_date"  git commit --amend --date="$new_date" -C HEAD
[master 0ea5418] How to change date of commit
 Date: Fri Dec 25 19:05:40 2015 +0300
 1 file changed, 122 insertions(+)
 create mode 100644 designest.site/source/_posts/git-date-change.md
```
вот что получилось в логе:
```
$ git --no-pager log -1 --stat --pretty=fuller
commit 0ea541838d6777f5f1618efb5d9713282042da7e
Author:     Dmitry Sigaev <Dmitry_Sigaev@epam.com>
AuthorDate: Fri Dec 25 19:05:40 2015 +0300
Commit:     Dmitry Sigaev <Dmitry_Sigaev@epam.com>
CommitDate: Fri Dec 25 19:05:40 2015 +0300

    How to change date of commit

 designest.site/source/_posts/git-date-change.md | 122 ++++++++++++++++++++++++
 1 file changed, 122 insertions(+)
```
ну далее пушим в origin

Вывод: 
пять команд, которые нужно запомнить:
```
$ new_date=$(stat -c %y git-date-change.md)
$ git add git-date-change.md
$ git commit --date="$new_date" -m "The 5 command to remember"
$ GIT_COMMITTER_DATE="$new_date"  git commit --amend --date="$new_date" -C HEAD
$ git push
```
                                             