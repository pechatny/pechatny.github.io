---
layout: post
title:  "Как настроить ssh-key и git в PowerShell"
date:   2025-05-30 19:39:00 +0300
categories: [windows]
comments: true
---
Настройка SSH-ключа и Git в PowerShell включает несколько шагов. Вот подробное руководство:

---

### 1. **Установка Git**
Если Git ещё не установлен, скачайте его с [официального сайта](https://git-scm.com/) и установите, выбрав опцию **"Git from the command line and also from 3rd-party software"** (чтобы `git` и `ssh` были доступны в PowerShell).

---

### 2. **Проверка установки Git**
Откройте **PowerShell** и выполните:
```powershell
git --version
```
Если версия отображается, Git установлен корректно.

---

### 3. **Генерация SSH-ключа**
#### Проверка существующих ключей:
```powershell
ls ~/.ssh/
```
Если есть файлы `id_rsa` и `id_rsa.pub`, можно использовать их. Если нет — создайте новые.

#### Генерация нового ключа:
```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- Нажмите `Enter`, чтобы сохранить ключ в стандартной папке (`~/.ssh/id_ed25519`).
- Укажите пароль (опционально, но рекомендуется для безопасности).

#### Альтернатива (если Ed25519 не поддерживается):
```powershell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

---

### 4. **Добавление ключа в ssh-agent**
#### Запуск ssh-agent:
```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic -PassThru | Start-Service
```
#### Добавление ключа:
```powershell
ssh-add ~/.ssh/id_ed25519
```
(или `id_rsa`, если использовали RSA).

---

### 5. **Копирование SSH-ключа в буфер**
Покажите ключ и скопируйте его (откройте файл и скопируйте содержимое):
```powershell
cat ~/.ssh/id_ed25519.pub
```
Или для копирования в буфер:
```powershell
Get-Content ~/.ssh/id_ed25519.pub | clip
```

---

### 6. **Добавление ключа на GitHub/GitLab**
- Откройте настройки аккаунта на [GitHub](https://github.com/settings/keys) или [GitLab](https://gitlab.com/-/profile/keys).
- Вставьте ключ из буфера в раздел **SSH Keys**.

---

### 7. **Проверка подключения**
```powershell
ssh -T git@github.com
```
Если всё настроено верно, увидите сообщение:
```
Hi username! You've successfully authenticated...
```

---

### 8. **Настройка Git в PowerShell**
Укажите имя и email (обязательно для коммитов):
```powershell
git config --global user.name "Your Nambe"
git config --global user.email "your_email@example.com"
```
Проверьте настройки:
```powershell
git config --list
```

---

### 9. **Использование Git с SSH**
Теперь можно клонировать репозитории по SSH-ссылке (например):
```powershell
git clone git@github.com:username/repo.git
```

---

### 10. **Дополнительные настройки (опционально)**
- **Сохранение пароля для SSH**:  
  Если не хотите вводить пароль каждый раз, добавьте его в `ssh-agent` (см. шаг 4).
- **Использование GPG для подписи коммитов**:  
  Настройка требует отдельного руководства.

---

### 🔥 Важно:
- Если `ssh` или `git` не распознаются, закройте и снова откройте PowerShell.
- Для работы с SSH в корпоративных сетях может потребоваться настройка прокси.

Готово! Теперь Git и SSH настроены в PowerShell. 🚀