# Памятка агенту: bx-shef/skills

Навыки к модулям shef.* — по правилам https://github.com/bx-shef/skills-standard/blob/main/STANDARD.md.
Здесь только `skills/<имя>/SKILL.md` + `evals/selection.json`; кода модулей нет.

Проверка перед сдачей — то же, что CI:

```bash
for m in options problems insync; do git clone --depth 1 https://github.com/bx-shef/$m modules/$m; done
npx bxshef lint --dir skills --code modules
BXSHEF_EVAL_KEY=… npx bxshef eval --dir skills --repeat 3     # ключ — из окружения
```

Нельзя: менять `description` без прогона `eval`; писать класс или сигнатуру по памяти —
только из `modules/<модуль>`; писать ключи в файлы. Один навык — один PR.
