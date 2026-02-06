# RUNBOOK: bootstrap‑генерация документации в новом проекте

Цель: имея только описание задачи/продукта, быстро создать первичный SDAD‑пакет документации (immutable + mutable), после чего можно передать проект “fresh” агенту на реализацию.

---

## 0) Подготовь проект (папка `<project_root>`)

Минимум:

- создай папку проекта
- (опционально) инициализируй git: `git init`

---

## 1) Скопируй шаблон SDAD

Из папки со starter pack (где лежит `template/`) выполни:

```bash
rsync -a template/ <project_root>/
```


## 2) Заполни входной бриф

Отредактируй:

- `<project_root>/PROJECT_BRIEF.md`

Правило: лучше 1 страница конкретики, чем 5 страниц “воды”.

---

## 3) Запусти Codex в режиме “docs only”

Рекомендуемый запуск, чтобы **не было лишних approvals**:

```bash
cd <project_root>
codex --sandbox workspace-write --ask-for-approval never
```

Далее вставь промпт из:

- `sdad_starter_pack/prompts/01_bootstrap_docs.md`

Важное ограничение: на этом шаге агент **не должен** писать продуктовый код — только документы и каркас.

---

## 4) Что дальше

1) (опционально) закоммить документы.
2) Запусти fresh агента на реализацию:
   - промпт: `sdad_starter_pack/prompts/02_fresh_agent_run.md`
   - режим Codex: `--ask-for-approval on-failure`
