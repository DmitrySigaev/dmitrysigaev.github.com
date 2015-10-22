title: Briefly cabbage for Node js
date: 2013-10-02 16:37:17
tags: Hexo.js, Node.js
---

![Node Package Manager ](/images/npm.png)
new ntest

Testing Image
Inserts an image in posts with specified size.

{% img [image_node_class] /images/npm.png [200] [10] [Node Package Manager Title [Node Package Manager]] %}


NPM — пакетный менеджер для node.js, аналог GEM в RoR. В статье несколько советов по его использованию.

Установка пакетов

Все знают 

```
# Устанавливает пакет express
$ npm install express
```

Какие варианты еще есть?
```
# Устанавливает все пакеты, перечисленные в package.json
$ npm install
```


```
# Устанавливает express и вносит запись о нем в package.json в секцию dependencies
$ npm install express --save
```

```
# Устанавливает grunt и вносит запись о нем в package.json в секцию devDependencies
$ npm install grunt --save-dev
```

Варианты с --save и --save-dev сделают запись в package.json только, если он уже существует.

Чтобы не утруждать себя, каждый раз указывая --save, можно прописать:
```
# Все - теперь все устанавливаемый пакеты будут автоматом прописываться в package.json
$ npm config set save true
```

Кстати, насчет --save
```
# Кроме того, что все пакеты обновятся, если в package.json в качестве 
# версии была прописана "*" - теперь туда попадут конкретные версии
$ npm update --save
```

Сокращенные варианты команд

Для ускорения процесса ввода команд удобно использовать сокращения. Самое полезное в виде таблички:
Ключ	Сокращение
install	i
uninstall	r
config	c
update	up
list	ls
--save	-S
--save-dev	-D

Пример:
npm install express --save

```
# Совершенно то же самое
$ npm i express -S
```

Подготовка к npm init

Не очень удобно при создании package.json при помощи npm init каждый раз вводить персональные данные. Чтобы этого избежать, сделаем настройку:
```
# Внесем информацию об авторе "по умолчанию"
$ npm set init.author.name "$NAME"
$ npm set init.author.email "$EMAIL"
$ npm set init.author.url "$SITE"
```

Вместо переменных среды $NAME и т.д. можно внести и сами данные. Все, теперь мы готовы к npm init

А что еще можно настраивать?

```
# Выведет список всех возможных настроек
$ npm config ls -l
```

Проверить, не устарели ли пакеты

```
# Бывает полезно сделать прежде чем делать update
$ npm outdated
```

Фиксируем версии пакетов

```
# Все, можно передавать в продакшен
$ npm shrinkwrap
```

Прежде чем передавать продукт в промышленную эксплуатацию, по хорошему, нужно зафиксировать точные версии пакетов с которыми все 100% работает. Эта команда так и сделает. После ее выполнения будет создан shrinkwrap.json, в котором будут прописаны точные версии ваших пакетов, теперь npm install будет устанавливать именно их.

Обновление версии NPM

```
# NPM вполне может обновлять сама себя
$ npm update npm -g
```


