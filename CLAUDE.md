# Памятка агенту: bx-shef/skills

Навыки к модулям shef.* — по правилам https://github.com/bx-shef/skills-standard/blob/main/STANDARD.md.
Здесь только `skills/<имя>/SKILL.md` + `evals/selection.json`; кода модулей нет.

Проверка перед сдачей — то же, что CI:

```bash
for m in options problems; do git clone --depth 1 https://github.com/bx-shef/$m modules/$m; done
npx bxshef lint --dir skills --code modules
BXSHEF_EVAL_KEY=… npx bxshef eval --dir skills --repeat 3     # ключ — из окружения
```

Нельзя: менять `description` без прогона `eval`; писать класс или сигнатуру по памяти —
только из `modules/<модуль>`; писать ключи в файлы. Один навык — один PR.

## Документация и практики Битрикс

### Источники
Документацию Битрикс берём из локальных клонов официальных репозиториев, а не из памяти модели и не со сторонних сайтов:

- `.bitrix-docs/framework-docs/` — Bitrix Framework (D7, ORM, модули, компоненты, контроллеры, события ядра). Исходник: https://github.com/bitrix-tools/framework-docs
- `.bitrix-docs/b24-rest-docs/` — REST API Битрикс24 (методы, события, вебхуки, приложения). Исходник: https://github.com/bitrix-tools/b24-rest-docs

Скиллы с правилами написания кода: https://github.com/bitrix-tools/best-practice
- `bitrix-best-practice-core` — контроллеры, роутинг, конфигурация, базовые сущности
- `bitrix-best-practice-sql` — работа с БД и ORM

### Первичная настройка (если папки `.bitrix-docs/` нет)
1. Склонировать документацию:
   ```bash
   mkdir -p .bitrix-docs
   git clone --depth 1 https://github.com/bitrix-tools/framework-docs.git .bitrix-docs/framework-docs
   git clone --depth 1 https://github.com/bitrix-tools/b24-rest-docs.git .bitrix-docs/b24-rest-docs
   ```
   Общий клон линейки уже лежит уровнем выше — `../.bitrix-docs/` (каталог `tools-ai`); можно пользоваться им.
2. `.bitrix-docs/` — в `.gitignore` проекта (уже добавлено).
3. Установить скиллы:
   ```bash
   npx skills add bitrix-tools/best-practice --skill bitrix-best-practice-core
   npx skills add bitrix-tools/best-practice --skill bitrix-best-practice-sql
   ```

### Правила работы
- Перед тем как писать код с API Битрикса, найди нужную статью поиском (grep/rg) по соответствующему клону и опирайся на неё. Не выдумывай классы, методы, параметры и поля.
- Задачи по D7, ORM, модулям и компонентам решай по `framework-docs` вместе с исходниками ядра проекта в `/bitrix/modules/`. Если документация и код ядра расходятся, прав код ядра (он соответствует установленной версии). Расхождение отметь в ответе.
- Задачи по REST-методам, событиям и приложениям Битрикс24 решай по `b24-rest-docs`. Если подключён MCP `b24-dev-mcp`, им тоже можно пользоваться.
- Для решений «как правильно писать» (структура, контроллеры, запросы к БД, ORM) применяй скиллы `bitrix-best-practice-core` и `bitrix-best-practice-sql`.
- Не используй устаревшие API (старое ядро `C*`-классов), если в D7 есть замена. Исключение: проект явно требует старое API.
- В ответе указывай путь к файлу документации, на который опирался.
- Обновление коробки из консоли — `php bitrix.php update:modules` (`framework-docs/pages/framework/console-commands.md`).
