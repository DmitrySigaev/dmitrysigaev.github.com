title: Node JS Version Manager
date: 2014-10-22 20:51:50
tags: Node JS
categories:
 - Issues
---
Кросплатформенная разработа на Node JS требует углубленных знаний.
Предварительно я разработывал Node JS обертку для Indigo под Windows,
но так как сама Indigo кросплатформеная, то пришлось и мне переместить разработку 
на Linux. В качесте платформы я выбрал Ubuntu 14.04.

Сначала я установил Node JS как это было описано на сайте [NodeJS.ORG](https://nodejs.org/en/download/package-manager/)
Т.е.

Setup with Ubuntu:
```
$ curl --silent --location https://deb.nodesource.com/setup_4.x | sudo bash -
```
Then install with Ubuntu:
```
$ sudo apt-get install --yes nodejs
```
И что вы думаете, все встало. 
следующим этапом я решил взять свой репозиторий с github.com
Тоже все загрузилось без проблем. 
Я пошел дальше и решил установить node-inspector для удаленной отладки моего проекта.
```
$ npm install -g node-inspector (если буду проблемы, то через sudo)
```
и тут все хорошо встало....
следующим этапом было отладка кода.

Запускаем сервер отладки
```
$ node-inspector
Node Inspector v0.12.3
Visit http://127.0.0.1:8080/?ws=127.0.0.1:8080&port=5858 to start debugging.
```
Из другой консоли запускаем саму ноду.

You can either start Node with a debug flag like:
```
$ node --debug your/node/program.js
```
я решил отлаживаться по шагам:
or, to pause your script on the first line:
```
$ node --debug-brk your/short/node/script.js
```
можно также послать сигнал во время выполнения ноды и включить отладку.
Or you can enable debugging on a node that is already running by sending it a signal:
это можно сделать двумя способами:
1. Get the PID of the node process using your favorite method. pgrep or ps -ef are good
```
$ pgrep -l node
2345 node your/node/server.js
```
2. Send it the USR1 signal
```
$ kill -s USR1 2345
```

ДО этого все работало хорошо, но тут нода мне говорит что она не знает
модуль ffi

не беда, в каталоге есть волшебный файл проекта ноды. package.json 
в котором говориться какие дополнительные модули использует наш проект

Запуская менеджер пакетов ноды (npm) следюуим образом
```
$ npm cache clear - это мы чистим кеш.
```
хотя некоторые поступают более радикальным способом
```
$ rm -rf node_modules -удаляя рекурсивно папку смодулями. я не советую так делать
```
Лучше просто взять и обновить модули путем удаление их из системы 
```
$ npm uninstall имя_модуля -save -этот ключ нужно для записи в файл package.json версии молуля.
```
Все это игры с бубном.

Главное суть этого поста в Node JS Version Manager (nvm)
Он помогает нам переключаться с между самими нодами.
Например у нас есть весия 

```
$ node -v
v0.10.25 установлная системой.
```
Но версия уже устарела, так как node-inspector ее не поддерживает.
Нам нужна новая и последняя, например.
Чтобы узнать, какие версии Node.js доступны для установки, набераем:
```
$ nvm ls-remote
```
выдаюет ограмны список:


```
        v0.1.14
        v0.1.15
            ...
         v0.3.0
         v0.3.1
         v0.3.4
            ...
         v0.7.7
         v0.7.8
         v0.7.9
            ...
         v4.0.0
         v4.1.2
         v4.2.0
         v4.2.1
```
Устанавливаем последнюю:
```
$ nvm install  v4.2.1
```
Теперь переключеся на нее:
```
$ nvm use v4.2.1
Now using node v4.2.1 (npm v2.14.7)
```

Смотрим список на нашей ubunte:

```
$ nvm ls
->       v4.2.1
         system
node -> stable (-> v4.2.1) (default)
stable -> 4.2 (-> v4.2.1) (default)
iojs -> N/A (default)
```

Проверяем:
```
$ node -v
v4.2.1
```
Можно создать свою метку. Например, любимая(favorite)
```
$nvm alias favorite v4.2.1
favorite -> v4.2.1
```
Что нам даст команда список: ls
```
$ nvm ls
->       v4.2.1
         system
favorite -> v4.2.1
node -> stable (-> v4.2.1) (default)
stable -> 4.2 (-> v4.2.1) (default)
iojs -> N/A (default)
```






