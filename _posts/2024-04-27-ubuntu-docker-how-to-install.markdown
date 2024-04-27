---
layout: post
title:  "Как установить Docker в Ubuntu"
date:   2024-04-27 14:29:00
categories: jekyll update
---

Я выбрал вариант установки через используя Docker Desktop.
Сначала добавляем официальный репозиторий с пакетами Docker. 
Без него не установится deb пакет.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Ссылка с инструкцией:
https://docs.docker.com/engine/install/ubuntu/

Скачать deb пакет приложения и установить.
```bash
sudo apt-get update
sudo apt install ./docker-desktop-4.29.0-amd64.deb
```
Ссылка для скачивания на той же странице:
https://docs.docker.com/engine/install/ubuntu/

## Запуск Docker Desktop
```bash
systemctl --user start docker-desktop
```

## Как залогиниться на Docker Hub
Если не получается, то надо проинициализировать хранилище паролей в системе.
```bash
pass init "Diesel Password Storage Key"
```

После этого логинимся через кнопку в GUI

## Автозапуск при входе в систему
```bash
systemctl --user enable docker-desktop
```

## Остановка Docker Desktop
Либо кнопкой в GUI, либо командой:
```bash
systemctl --user stop docker-desktop
```