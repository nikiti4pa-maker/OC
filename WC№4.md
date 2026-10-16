###### Виконав: Пивовар Нікіта Андрійович

**Пакет** — це архів, що містить:
- скомпільовані бінарні файли програми (або вихідний код);
- метадані (назва, версія, опис, залежності, архітектура);
- скрипти встановлення/видалення;
- файли конфігурації, документацію, іконки тощо.

1. **Пакет** дозволяє встановлювати, оновлювати та видаляти програмне забезпечення разом з усіма його залежностями однією командою, замість ручного збирання з вихідників.

2. **Репозиторій (сховище)** — це офіційне або стороннє онлайн-сховище пакетів. Воно містить індекс пакетів (метадані) і самі файли пакетів. Менеджер пакетів завантажує з репозиторію потрібні пакети та їхні залежності.

### Огляд основних менеджерів пакетів Linux:

| Менеджер | Дистрибутиви | Основні можливості |
|-------------------|---------------------------------------|--------------------|
| **apt** + **dpkg** | Debian, Ubuntu, Linux Mint, Pop!_OS  | Високорівневий (apt) + низькорівневий (dpkg). Пошук, встановлення, оновлення, видалення, вирішення залежностей, робота з репозиторіями. |
| **dnf** / **yum** | Fedora, RHEL, CentOS, Rocky, AlmaLinux| dnf — сучасна заміна yum. Робота з модулями, групами пакетів, історією транзакцій, rollback. |
| **pacman** | Arch Linux, Manjaro, EndeavourOS | Швидкий, простий синтаксис. Підтримка AUR через helper-и (yay, paru). |
| **zypper** | openSUSE, SUSE Linux Enterprise | Підтримка патернів, репозиторіїв, snapshot-ів (Btrfs). |
| **apk** | Alpine Linux | Легкий, мінімалістичний, часто використовується в Docker. |
| **Snap / Flatpak / AppImage** | Крос-дистрибутивні | Ізольовані пакети (sandbox). Snap — від Canonical, Flatpak — універсальний, AppImage — portable. |
### 2. Менеджер пакетів у системі та основні команди

Система використовує **apt**.
#### Пошук пакетів: 
- apt search vlc
- apt-cache search --names-only '^vlc$'
- apt show vlc
#### Оновлення індексів репозиторіїв
- apt update
#### Встановлення пакетів (із репозиторію)
- apt install vlc
- apt install g++
#### Додавання нового репозиторію і встановлення з нього
- apt install software-properties-common
- add-apt-repository ppa:назва/ppa
- apt update
- apt install потрібний-пакет
#### Перегляд інформації про пакети
- apt list --installed
- apt list --upgradable
- dpkg -l | grep vlc
- apt show vlc
#### Видалення пакетів
- apt remove vlc
- apt purge vlc
- apt autoremove
#### Оновлення системи
- apt update
- apt upgrade
- apt full-upgrade
### Встановлення програм через термінал (методика)

Встановлення відео/аудіоплеєра (VLC)

Методика виконання:
##### 1. apt update
##### 2. apt install -y vlc
Після встановлення можна перевірити наявність програми:
##### 1. which vlc
##### 2. vlc --version
##### 3. dpkg -l | grep vlc
### Встановлення середовища для мови програмування C++
#### Для роботи з C++ у Ubuntu зазвичай встановлюють компілятор g++.
Методика виконання:
##### 1. apt update
##### 2. apt install -y g++
#### Додатково можна встановити повний набір інструментів для розробки:
##### apt install -y build-essential
Пакет build-essential включає g++, gcc, make та інші необхідні утиліти.

Перевірка після встановлення:
##### 1. g++ --version
##### 2. which g++
### Встановлення через графічні магазини додатків
#### У Ubuntu (GNOME) доступні такі інструменти:

#### Ubuntu Software (GNOME Software)
- Відкривається з меню програм.
- Підтримує deb-пакети (через apt) та Snap.
#### Snap Store
- Спеціалізований магазин для Snap-пакетів.
#### Приклади:
- Ubuntu Software → пошук «VLC» → Install.
- Для C++: можна встановити Visual Studio Code через Ubuntu Software / Snap, а компілятор g++ — через термінал або магазин.
### Висновки:
In this work, the concepts of a software package and a repository were examined, and an overview of the main package managers used in Linux distributions was provided.  
The system under study runs Ubuntu and uses the **apt** package manager. The basic commands for searching, installing, updating, and removing packages were described, including the procedure for adding new repositories.  
The methodology for installing a media player (VLC) and a C++ development environment (g++ / build-essential) via the terminal was outlined. Additionally, the process of installing applications through graphical package managers and software stores (Ubuntu Software, Snap Store,) was considered.  
Overall, package managers significantly simplify software management in Linux by automating dependency resolution and ensuring system consistency.
