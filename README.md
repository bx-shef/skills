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

| навык | что делает |
|---|---|
| `shef-feedback` | отзыв о навыке после задачи — что пригодилось, чего не хватило; обязателен в наборе |

Остальные навыки переезжают сюда из репозиториев модулей.

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

После задачи с навыком ИИ-агент по `shef-feedback` сам отправляет отзыв одним вызовом
`npx bxshef feedback send --skill … --outcome … --task … --helped … --issue …` — без файла и без
человека. Адрес — `{"feedback": "https://…"}` в `.bxshef.json` корня проекта или переменная
окружения `BXSHEF_FEEDBACK_URL` (приёмник — `https://skills.bx-shef.by/feedback`).

## Лицензия

MIT.
