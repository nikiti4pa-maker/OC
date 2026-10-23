###### Виконав: Пивовар Нікіта Андрійович
#### Словник:
- Peripheral device — периферійний пристрій (флешка, принтер, сканер тощо)
- Mount / Mounting — монтування (підключення файлової системи пристрою до дерева каталогів Linux)
- Unmount / Umount — розмонтування (безпечне відключення файлової системи)
- Mount point — точка монтування (каталог, до якого підключається пристрій)
- File system — файлова система (ext4, NTFS, FAT32, exFAT тощо)
- Device file — файл пристрою (спеціальний файл у /dev, наприклад /dev/sdb1)
- udev — підсистема ядра Linux для динамічного створення файлів пристроїв
- udisks / udisks2 — сервіс автоматичного монтування знімних носіїв
- CUPS — Common Unix Printing System (система друку в Linux)
- Printer queue — черга друку
- Driver — драйвер (програма для взаємодії ОС з обладнанням)
- Hotplug — гаряче підключення (підключення/відключення без перезавантаження)
- Removable media — знімний носій (флешка, зовнішній диск)
- Block device — блоковий пристрій (диски, флешки)
- Character device — символьний пристрій
- lsblk — команда перегляду блокових пристроїв
- fdisk / parted — утиліти для роботи з розділами диска
- lp / lpr — команди відправки файлів на друк
- lpstat — перегляд стану принтерів і черги друку
- lpadmin — адміністрування принтерів у CUPS
- USB — Universal Serial Bus
- IPP — Internet Printing Protocol (протокол мережевого друку)
 ### 1. Механізм роботи ОС Linux з периферійним обладнанням.
Суть операції монтуванняМонтування (mount) — це процес підключення файлової системи зовнішнього пристрою (флешки, жорсткого диска, CD/DVD, мережевої папки тощо) до дерева каталогів Linux.

У Linux усе є файлом. Периферійні пристрої з’являються у системі як спеціальні файли пристроїв у каталозі /dev. Щоб отримати доступ до даних на пристрої, його файлову систему потрібно «приєднати» (змонтувати) до певної точки монтування
#### Для чого використовується:
- отримати доступ до файлів на зовнішньому носії;
- забезпечити єдине дерево каталогів;
- контролювати права доступу, тип файлової системи та параметри (тільки читання, синхронізація тощо).
#### Як виконується:Автоматично (через udev + udisks2 / GNOME Disks / файловий менеджер):
- при підключенні флешки система визначає пристрій;
- створює точку монтування (наприклад, /media/user/USB_NAME);
- монтує файлову систему.
### 2.1. Підключення флешки до віртуальної машиниУ VirtualBox:
1. Вставте флешку в USB-порт комп’ютера.
2. У вікні VirtualBox: Пристрої → USB → виберіть вашу флешку.
3. У гостьовій Ubuntu флешка з’явиться в файловому менеджері (Nautilus) або в /media/.

- Перевірка в терміналі:

lsblk

- .# або

sudo fdisk -l

dmesg | tail
#### Копіювання файлу через графічний інтерфейс
1. Відкрийте Файли (Files / Nautilus).
2. Зліва з’явиться підключена флешка.
3. Відкрийте її, знайдіть потрібний файл.
4. Скопіюйте (Ctrl+C) і вставте (Ctrl+V) у домашню теку або Documents.
#### Копіювання файлу через термінал
- Дізнатися ім’я пристрою та точку монтування

lsblk

df -h

- Якщо не змонтовано автоматично

sudo mkdir -p /mnt/usb

sudo mount /dev/sdb1 /mnt/usb

- Копіювання

cp /mnt/usb/document.pdf ~/Documents/

- Перевірка

ls -l ~/Documents/document.pdf

- Розмонтування

sudo umount /mnt/usb
#### Робота з принтером.
##### Через графічний інтерфейс:
1. Settings → Printers → Add Printer.
2. Система має виявити USB- або мережевий принтер.
3. Виберіть драйвер (або Generic / CUPS).
4. Відкрийте файл → Print.
#### Через термінал (CUPS):
- Перегляд доступних принтерів

lpstat -p -d

lpinfo -v

- Додавання принтера (приклад)

sudo lpadmin -p MyPrinter -E -v usb://... -m everywhere

-  Друк файлу
 
lp ~/Documents/document.pdf

- або з параметрами

lp -d MyPrinter -o media=A4 -n 1 file.txt

- Перегляд черги
 
lpq
### Висновки:

In this work, the mechanisms of working with peripheral devices in the Linux operating system were examined using a USB flash drive and a printer as examples.
The key concept of mounting was analyzed — the process of attaching a device’s file system to the Linux directory tree. The differences between Linux and Windows approaches to handling peripherals were highlighted: Linux uses a unified file hierarchy and requires explicit mounting/unmounting, while Windows assigns drive letters automatically.

The methodology for connecting a flash drive to a virtual machine, copying files via both the graphical interface and the terminal, and printing documents using CUPS was described in detail.
As a result, practical understanding of device management, mounting procedures, and printing configuration in Linux was obtained. These skills are essential for everyday system administration and working with external hardware.
