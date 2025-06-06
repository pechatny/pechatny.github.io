---
layout: post
title:  "Как создать шаблон файла в Intellij Idea"
date:   2025-06-04 19:50:39 +0300
categories: [common]
comments: true
---

# Как создать шаблон файла в Intellij Idea

## File Templates (Шаблоны файлов)**
Позволяют задать стандартное содержимое для новых файлов (классов, интерфейсов и т. д.).

**Как создать File Template:**
1. **Откройте настройки**:
    - `File → Settings` → `Editor → File and Code Templates`.

2. **Выберите вкладку `Files` или `Includes`**:
    - Можно изменить шаблон для `Class`, `Interface` и др.
    - Или добавить свой (`+` → ввести имя и шаблон).

3. **Используйте переменные**:
    - `${NAME}` – имя файла,
    - `${DATE}` – текущая дата,
    - `${USER}` – имя пользователя.

Пример шаблона для поста Jekyll:
```markdown
---
layout: post
title:  "${POST_TITLE}"
date:   ${YEAR}-${MONTH}-${DAY} ${HOUR}:${MINUTE}:${SECOND} +0300
categories: [common]
comments: true
---
# ${POST_TITLE}
```

Шаблон для имени файла:
```markdown
${YEAR}-${MONTH}-${DAY}-${FILENAME}
```
