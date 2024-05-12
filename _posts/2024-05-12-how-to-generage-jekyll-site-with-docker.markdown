---
layout: post
title: "Как создать блог Jekyll с помощью Docker" 
date:   2024-05-11 00:00:00 -0500
---

## Создаю новый сайт:
```bash
docker run --rm \
  --volume="$PWD:/srv/jekyll" \
  -it jekyll/jekyll \
  sh -c "jekyll new --skip-bundle ."
```

Открываю файл Gemfile и редактирую закомментированную строчку
```
gem "github-pages", "~> 231", group: :jekyll_plugins
gem "jekyll", "~> 3.9.5"
```

Добавляю Webrick
```bash
docker run --rm --volume="$PWD:/srv/jekyll"  -it jekyll/jekyll sh -c "bundle add webrick"
```

Устанавливаю правильные версии зависимостей
```bash
docker run --rm --volume="$PWD:/srv/jekyll"  -it jekyll/jekyll sh -c "bundle install"
```
## Локальная разработка
Из папки с проектом запускаю. Работает сервер. На хосте можно смотреть как будет выглядеть сайт, при перезагрузке страницы будет билдится сайт заново.
```bash
docker run --rm -v $PWD:/srv/jekyll:Z --publish 4000:4000 jekyll/jekyll jekyll serve
```

Короткая версия команды без удаления контейнера.
```bash
docker run --name jekyll -v $PWD:/srv/jekyll:Z -p 4000:4000 jekyll/jekyll jekyll serve
```

Перезапуск контейнера с сервером для локальной разработки
```bash
docker start -i jekyll
```

---
## Jenkins
Собирать можно этой командой
```bash
export JEKYLL_VERSION=3.8
docker run --rm \
  --volume="$PWD:/srv/jekyll:Z" \
  -it jekyll/builder:$JEKYLL_VERSION \
  jekyll build
```

---

## Ссылки
- https://hub.docker.com/r/jekyll/jekyll/
- https://github.com/envygeeks/jekyll-docker/blob/master/README.md