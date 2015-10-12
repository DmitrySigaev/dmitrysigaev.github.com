title: Увеличение размера VHD файла под windows 10
date: 2015-10-12 20:34:25
tags: VirtualBox, VHD, Virtual Hard Disk 
categories:
 - Issues
---

![](/images/pinch_expand.jpg)

# Как увеличить размер VHD файла под windows 10. VirtualBox 5.0 такой возможности не дает, а жаль!

Когда я решил создать виртуальную машину в VirtualBox (Oracle VM VirtualBox — программный продукт виртуализации) я решил использовать под диск формат VHD (Virtual Hard Disk)

Почему? 

- Во-первых VirtualBox у меня установлен на Windows 10, а изначально VHD формат был создан компанией Connectix и позднее куплен Microsoft вместе с программой виртуализации Virtual PC. C июня 2005 Microsoft сделала спецификацию формата VHD доступной третьим фирмам в рамках Microsoft Open Specification Promise.
- Во-вторых он поддерживается, на текущий момент, очень многими программными продуктами для виртуализации. Например, VMware Workstation, Windows Virtual PC.

Но вот проблема. При создании диска я указал, что диск будет динамически-расширяемый, но максимальный размер установил в 100Gb. Естественно, данный объем у меня быстро закончился.

# Проблема (Issue): Как увеличить размер VHD файла под windows 10.

VirtualBox 5.0 такой возможности не дает, а жаль! Интернет мне в помощь, но все что выдают мне поисковики это - утилита VHDResizer. Вопрос: Зачем мне засорять свою систему этим VHDResizer? Неужели windows 10 не справиться с этим!?

# Решение (Resolve)

Использовать утилиту diskpart.exe входящую в Windows 10

Command Prompt

``` 
cmd.exe
diskpart.exe

```

```
select vdisk file="полный путь к файлу"
expand vdisk maximum="размер в мб

```

На самом деле есть целый список команд в утилите diskpart для работы с виртуальном диском VHD:

- Attach  vdisk 
- Compact vdisk 
- Create  vdisk 
- Detail  vdisk 
- Expand  vdisk 
- Merge   vdisk 
- Select  vdisk 

# Поэкспериментируем

Запускаем из командной строки DiskPart:
```
Microsoft DiskPart version 10.0.10240

Copyright (C) 1999-2013 Microsoft Corporation.
On computer: EPRUPET

DISKPART> list vdisk

There are no virtual disks to show.

```

Перемещаем фокус на виртуальный диск:

```
DISKPART> select vdisk file="f:\VBDisks\W7\W7.vhd"

DiskPart successfully selected the virtual disk file.
```
Вводим команду лист:
```
DISKPART> list vdisk

  VDisk ###  Disk ###  State                 Type       File
  ---------  --------  --------------------  ---------  ----
* VDisk 0    Disk ---  Added                 Unknown     f:\VBDisks\W7\W7.vhd
```
Смотрим детальную информацию:

```
DISKPART> detail vdisk

Device type ID: 0 (Unknown)
Vendor ID: {00000000-0000-0000-0000-000000000000} (Unknown)
State: Added
Virtual size:  102 GB
Physical size:   28 GB
Filename: f:\VBDisks\W7\W7.vhd
Is Child: No
Parent Filename:
Associated disk#: Not found.

DISKPART>
```
