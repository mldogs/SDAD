# SDAD Starter Repository

`**Spec-Driven Agent Development**: подход, где разработка агентом управляется спецификациями, ограничениями и проверяемым планом исполнения.

Этот репозиторий содержит стартовый набор документов и промптов для быстрого запуска нового проекта в SDAD-процессе.

## Что внутри

- `sdad_starter_pack/template/` - шаблон структуры проекта (документы, конституция, runbooks, execplan).
- `sdad_starter_pack/prompts/01_bootstrap_docs.md` - промпт для генерации первичного SDAD-пакета из `PROJECT_BRIEF.md`.
- `sdad_starter_pack/prompts/02_fresh_agent_run.md` - промпт для свежего агента на автономную реализацию.
- `sdad_starter_pack/README.md` - детальный runbook по bootstrap-сценарию.

## Быстрый старт

1. Создайте целевой репозиторий/папку проекта.
2. Скопируйте шаблон в корень целевого проекта:

```bash
rsync -a sdad_starter_pack/template/ <project_root>/
```

3. Заполните `<project_root>/PROJECT_BRIEF.md`.
4. Запустите Codex в целевом проекте и вставьте промпт bootstrap:

```bash
cd <project_root>
codex --sandbox workspace-write --ask-for-approval never
```

Промпт: `sdad_starter_pack/prompts/01_bootstrap_docs.md`

5. После генерации docs-пакета запустите свежего агента для реализации:

Промпт: `sdad_starter_pack/prompts/02_fresh_agent_run.md`

## SDAD-модель работы

- `docs/constitution/*` - immutable-правила (цели, ограничения, архитектурные границы, quality gates).
- `docs/execplans/pilot_execplan.md` - живой план исполнения (обновляется по мере работы).
- Агент работает итеративно: один шаг -> проверка командами -> обновление плана -> локальный коммит.

## Рекомендуемый порядок для fresh-агента

1. `docs/START_HERE.md`
2. `docs/constitution/*`
3. `.agent/AGENTS.md` и `CLAUDE.md`
4. `docs/execplans/pilot_execplan.md`

## Зачем это нужно

SDAD снижает зависимость от "памяти" агента и делает работу воспроизводимой: решения, ограничения и критерии готовности фиксируются в репозитории и проверяются командами.
