# Навыки для ИИ-агентов: модули shef.* на Битриксе

![skills](https://github.com/bx-shef/skills/actions/workflows/skills.yml/badge.svg)

Навыки к модулям [shef.options](https://github.com/bx-shef/options),
[shef.problems](https://github.com/bx-shef/problems), [shef.insync](https://github.com/bx-shef/insync)
по методологии [bx-shef/skills-standard](https://github.com/bx-shef/skills-standard).
Навык — папка со `SKILL.md` по стандарту [Agent Skills](https://agentskills.io); ИИ-агент
берёт его сам по описанию и делает по канону модуля.

## Установка в проект

```bash
npx skills add bx-shef/skills
```

Обновление — `npx skills update`. Файлы навыков в проекте не правят: замечания идут отзывом.

## Навыки

Справочные — «как устроено»:

| навык | о чём |
|---|---|
| `shef-options-blocks` | синглетон, реестр настроек, объект из массива, pid-блокировка |
| `shef-options-traits` | трейты shef.options: что даёт, когда брать |
| `shef-options-components` | `AComponent`, ajax, `Builder`, фильтры прав |
| `shef-options-settings` | страница настроек на `ShOptionsConfig` |
| `shef-options-installer` | установка смарт-процессов, UF и пресетов |

Операционные — «сделай по канону»:

| навык | что делает |
|---|---|
| `shef-new-module` | скелет нового модуля на базе `shef.options` |
| `shef-new-component` | компонент на `AComponent` |
| `shef-new-ajax-action` | ajax-действие с правильными фильтрами |
| `shef-new-option` | опция на страницу настроек |
| `shef-new-agent` | агент или cron с блокировкой |
| `shef-use-component` | подключить готовый компонент из кода |
| `shef-use-logger` | логирование через `shef.problems` |
| `shef-feedback` | отзыв о навыке после задачи — что пригодилось, чего не хватило; обязателен в наборе |

## Проверка

На каждом PR — [Action](https://github.com/bx-shef/skills-standard/tree/main/action):
`bxshef lint` (форма, evals, классы против свежих `main` трёх модулей) и `bxshef eval`
(выбор навыка моделью по фразе, порог 0.9 при 3 повторах). Локально:

```bash
npx bxshef lint --dir skills --code <каталог с checkout'ами модулей>
BXSHEF_EVAL_KEY=… npx bxshef eval --dir skills --repeat 3
```

Правила навыка — [STANDARD.md](https://github.com/bx-shef/skills-standard/blob/main/STANDARD.md).

## Отзывы

После задачи с навыком ИИ-агент по `shef-feedback` сам отправляет отзыв — одной командой
`curl --data-urlencode …` (поля `category`, `title`, `body`, `skill`, `outcome`, `helped`) на адрес,
вписанный в навык: `https://skills.bx-shef.by/feedback`. Ни файлов, ни `bxshef`, ни настроек в
проекте не нужно. Приёмник — [skills-standard/feedback](https://github.com/bx-shef/skills-standard/tree/main/feedback);
секреты, адреса и пути он вычищает сам.

## Лицензия

MIT.
