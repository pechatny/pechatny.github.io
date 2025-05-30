---
layout: post
title:  "Как сделать PowerShell красивым как \"Oh My ZSH!\""
date:   2025-05-30 20:00:00 +0300
categories: windows
---
Сначала необходимо установить Windows Terminal.

## Устанавливаем Oh My Posh
В большинстве случаев будет достаточно инструкции с официального сайта:
https://ohmyposh.dev/

Для тяжелых случаев, как у меня, когда надо установить на windows компьютер без админских прав, подойдут следующие шаги:
- Скачиваем установщик под ходящий под вашу систему с этой страницы:
  - https://github.com/JanDeDobbeleer/oh-my-posh/releases
  - Под мой процессор подходит этот устанровщик install-arm64.exe
- Устанавливаем
- Далее действуем по этой инструкции
  - https://ohmyposh.dev/docs/installation/prompt
  - Открываем файл с профилем
    - `notepad $PROFILE`
  - Если не открылся, то сначала создаем его командой
    - `New-Item -Path $PROFILE -Type File -Force`
    - А потом открываем
      - `notepad $PROFILE`
  - Вставляем в файл профиля эту строчку
    - `oh-my-posh init pwsh | Invoke-Expression`
  - Перезагружаем профиль
    - `. $PROFILE`
  - Готово

## Установка шрифтов
- Скачивание шрифтов
  - `oh-my-posh font install`
  - Выбираем шрифт Meslo
- Настройка шрифта в терминале
  - Открыть Windows Terminal
  - Открыть файл с настройками сочетанием клавиш в английской раскладке
    - CTRL + SHIFT + ,
  - и изменить секцию defaults на:
    - ```"defaults":  
			{  
			"font":  
				{  
				"face": "MesloLGM Nerd Font"  
				}  
			}```
- Готово
## Установка темы
- Скачиваем тему в любую удобную папку отсюда https://github.com/JanDeDobbeleer/oh-my-posh/tree/main/themes
- Открываем профиль `notepad $PROFILE`
- И модифицируем строчку инициализации терминала, добавив --config="путь к теме"
  - `oh-my-posh init pwsh --config=~/soft/agnoster.omp.json | Invoke-Expression`
## Как укоротить имя в терминале
Открываем установленную тему и в сегменте  "type": "session" в template ставим пробел.
```json
{
  "background": "#ffffff",
  "foreground": "#100e23",
  "powerline_symbol": "\ue0b0",
  "style": "powerline",
  "template": " ",
  "type": "session"
}
```

## Установка автокомплита для git
https://github.com/dahlbyk/posh-git
Выполнить эту команду и все.
```
PowerShellGet\Install-Module posh-git -Scope CurrentUser -Force
```

## Установка Vim
Скачать vim с официального сайта, установить в любую папку куда есть доступ.
https://www.vim.org/download.php

И в Path прописать путь до файла vim
И выполнить эту команду, чтобы включить этот модуль.
```
Add-PoshGitToProfile
```