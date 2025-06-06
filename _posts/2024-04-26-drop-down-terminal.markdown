---
layout: post
title:  "Как настроить Drop Down Terminal в Ubuntu"
date:   2024-04-26 08:28:00 +0300
categories: [ubuntu]
---
## ddterm (Drop Down Terminal)
1. В центре приложений выбрать и установить "Менеджер расширений"
2. Через **менеджер расширений** установить ddterm.
3. F12 нажимаем и терминал выпадает. Готово.

## zsh

### Установка zsh
```bash
sudo apt install zsh
```

### Установка omyzsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Настройка omyzsh
- Добавим плагинов в  .zshrc
- Поменяем тему на agnoster
- Установим пользователя по умолчанию DEFAULT_USER=имя_пользователя, чтобы надпись в командной строке была покороче

```
ZSH_THEME="agnoster"
DEFAULT_USER=diesel

plugins=(git copybuffer copyfile sublime)
```

### Список плагинов:
- git сокращения для работы с гитом
- copybuffer копирует команду в буфер при сочетании ctrl+o
- copyfile копирует файл в буфер
- sublime сокращения для открывания файла в sublime

### Настройка темы zsh
По умолчанию в теме agnoster специальные символы отображаются коряво. Поэтому надо установить шрифты.

В любую папку скачиваем шрифты
```bash
git clone https://github.com/powerline/fonts.git
```

Запускаем скрипт установки
```bash
./install.sh
```

В настройках ddterm  выбираем шрифт **Noto Mono for Powerline Regular 12**

https://ohmyz.sh/

---
### Что можно улучшить?
Установить zoxide
https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/zoxide

thefuck
https://github.com/nvbn/thefuck