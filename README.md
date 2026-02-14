# The Roman Chronicle — Hugo‑блог

Исторический блог о Древнем Риме, созданный на Hugo с использованием темы Charaka и автоматическим деплоем через GitHub Pages.

## Структура проекта

```
├── .github/workflows/hugo.yml    # GitHub Actions workflow для сборки и деплоя
├── archetypes/                   # Шаблоны для новых постов
│   ├── default.md
│   └── posts.md                  # Основной шаблон поста с кастомными полями
├── content/posts/                # Посты (каждый пост — папка‑bundle)
│   └── 001-tarquins-forum/
│       ├── index.md              # Текст поста
│       └── *.jpg/png             # Изображения, относящиеся к посту
├── layouts/                      # Переопределённые шаблоны темы
│   ├── _default/
│   │   ├── single.html           # Шаблон отдельного поста
│   │   └── list.html             # Шаблон списка постов
│   ├── index.html                # Шаблон главной страницы
│   └── partials/                 # Частичные шаблоны (хедер, футер и т.д.)
├── static/                       # Статические файлы (иконки, CSS, JS)
│   ├── css/styles.css            # Дополнительные стили
│   └── favicon.*                 # Иконки сайта
└── hugo.toml                     # Конфигурация Hugo
```

## Создание нового поста

1. **Создай папку поста (bundle)**:

```bash
   hugo new posts/002-issue-title/index.md
```

   Эта команда создаст папку `content/posts/002-issue-title/` и внутри неё файл `index.md`, заполненный по шаблону `archetypes/posts.md`.

2. **Заполни фронт‑маттер**:

   Открой `content/posts/002-issue-title/index.md`. Вверху файла будет блок:

```yaml
title: "002 Issue Title"
date: 2023-10-27T10:00:00Z
draft: true
params:
  location: "Рим"
  roman_year_auc: ""
  era: "Царский период"
  lede: ""
```

   - `title` — заголовок поста.
   - `date` — дата публикации (можно править).
   - `draft: true` — черновик. **Перед публикацией измени на `false`**.
   - `params.location` — место действия (обычно «Рим»).
   - `params.roman_year_auc` — год от основания Рима (AUC).
   - `params.era` — исторический период (напр., «Царский период»).
   - `params.lede` — краткое вступление (выводится под заголовком).

3. **Напиши текст**:

   После фронт‑маттера пиши текст в формате Markdown.

4. **Добавь изображения**:

   Положи изображения в ту же папку поста (`content/posts/002-issue-title/`).

   В тексте поста ссылайся на них относительным путём:

```markdown
![Описание изображения](image-name.jpg)
```

   Для контроля размера можно использовать HTML:

```html
<img src="image-name.jpg" alt="Описание" width="400">
```

   **Важно:** чтобы HTML работал, в `hugo.toml` должна быть строка:

```toml
[markup.goldmark.renderer]
unsafe = true
```

## Работа с черновиками

- Пока `draft: true`, пост **не публикуется** на GitHub Pages (хотя локально виден при `hugo server -D`).
- Чтобы опубликовать, измени на `draft: false` или удали строку.

## Стилизация

- Заголовки `h2` и `h3` внутри поста автоматически центрируются и имеют отступ сверху.
- Дополнительные стили можно добавлять в `static/css/styles.css`, оборачивая их в класс `.post-body` (чтобы не затронуть остальной сайт).

## Локальная разработка

1. Убедись, что тема установлена:

```bash
git clone https://github.com/natarajmb/charaka-hugo-theme.git themes/charaka-hugo-theme
```

2. Запусти локальный сервер:

```bash
hugo server -D      # с черновиками
# или
hugo server         # только опубликованные
```

   Сайт будет доступен по адресу `http://localhost:1313/roman-chronicle/`.

## Деплой

При пуше в ветку `main` автоматически запускается GitHub Actions workflow (файл `.github/workflows/hugo.yml`), который:

1. Устанавливает Hugo.
2. Клонирует тему.
3. Собирает сайт (только посты с `draft: false`).
4. Деплоит результат на GitHub Pages.

Сайт доступен по адресу: `https://chermet90.github.io/roman-chronicle/`

## Настройки

Основные настройки сайта хранятся в `hugo.toml`:

- `baseURL` — базовый адрес сайта (важно для корректных ссылок).
- `title` — название сайта.
- `theme` — используемая тема.
- `relativeURLs` — относительные ссылки (включено для работы на GitHub Pages).

## Полезные ссылки

- [Hugo документация](https://gohugo.io/documentation/)
- [Charaka Hugo Theme](https://github.com/natarajmb/charaka-hugo-theme)
- [GitHub Pages](https://pages.github.com/)