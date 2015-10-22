title: Briefly cabbage for Node js
date: 2013-10-02 16:37:17
tags: Hexo.js, Node.js
---

![Node Package Manager ](/images/npm.png)
new ntest

Testing Image
Inserts an image in posts with specified size.

{% img [image_node_class] /images/npm.png [200] [10] [Node Package Manager Title [Node Package Manager]] %}


NPM � �������� �������� ��� node.js, ������ GEM � RoR. � ������ ��������� ������� �� ��� �������������.

��������� �������

��� ����� 

```
# ������������� ����� express
$ npm install express
```

����� �������� ��� ����?
```
# ������������� ��� ������, ������������� � package.json
$ npm install
```


```
# ������������� express � ������ ������ � ��� � package.json � ������ dependencies
$ npm install express --save
```

```
# ������������� grunt � ������ ������ � ��� � package.json � ������ devDependencies
$ npm install grunt --save-dev
```

�������� � --save � --save-dev ������� ������ � package.json ������, ���� �� ��� ����������.

����� �� ��������� ����, ������ ��� �������� --save, ����� ���������:
```
# ��� - ������ ��� ��������������� ������ ����� ��������� ������������� � package.json
$ npm config set save true
```

������, ������ --save
```
# ����� ����, ��� ��� ������ ���������, ���� � package.json � �������� 
# ������ ���� ��������� "*" - ������ ���� ������� ���������� ������
$ npm update --save
```

����������� �������� ������

��� ��������� �������� ����� ������ ������ ������������ ����������. ����� �������� � ���� ��������:
����	����������
install	i
uninstall	r
config	c
update	up
list	ls
--save	-S
--save-dev	-D

������:
npm install express --save

```
# ���������� �� �� �����
$ npm i express -S
```

���������� � npm init

�� ����� ������ ��� �������� package.json ��� ������ npm init ������ ��� ������� ������������ ������. ����� ����� ��������, ������� ���������:
```
# ������ ���������� �� ������ "�� ���������"
$ npm set init.author.name "$NAME"
$ npm set init.author.email "$EMAIL"
$ npm set init.author.url "$SITE"
```

������ ���������� ����� $NAME � �.�. ����� ������ � ���� ������. ���, ������ �� ������ � npm init

� ��� ��� ����� �����������?

```
# ������� ������ ���� ��������� ��������
$ npm config ls -l
```

���������, �� �������� �� ������

```
# ������ ������� ������� ������ ��� ������ update
$ npm outdated
```

��������� ������ �������

```
# ���, ����� ���������� � ���������
$ npm shrinkwrap
```

������ ��� ���������� ������� � ������������ ������������, �� ��������, ����� ������������� ������ ������ ������� � �������� ��� 100% ��������. ��� ������� ��� � �������. ����� �� ���������� ����� ������ shrinkwrap.json, � ������� ����� ��������� ������ ������ ����� �������, ������ npm install ����� ������������� ������ ��.

���������� ������ NPM

```
# NPM ������ ����� ��������� ���� ����
$ npm update npm -g
```


