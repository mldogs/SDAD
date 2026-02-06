# RUNBOOK: Git (автокоммиты для SDAD)

Цель: дать агенту возможность работать автономно, но оставлять **понятные чекпойнты** (коммиты), чтобы:

- легко откатываться,
- легко ревьюить,
- сохранять прогресс при перезапуске агента.

---

## TL;DR (рекомендуемый протокол)

1) Делай “thin slice” по ExecPlan.
2) Запускай проверки из `docs/constitution/QUALITY_GATES.md`.
3) Обновляй `docs/execplans/pilot_execplan.md` (progress + evidence).
4) Делай **локальный commit**.
5) **Не пушь** в remote без Ask‑first.

---

## Branching

Если в репозитории настроен remote и ты находишься на `main`/`master`, создай рабочую ветку:

```bash
git checkout -b agent/<short-slug>
```

Если ветка уже не `main`/`master` — продолжай в текущей.

---

## Commit cadence (когда коммитить)

Коммить только “зелёные” изменения:

- после завершения одного пункта в `Progress` (или другого атомарного шага),
- когда соответствующие проверки прошли.

Избегай WIP‑коммитов с падающими тестами. Если очень нужен чекпойнт при сломанном состоянии — Ask‑first.

---

## Commit messages

Рекомендуемый формат: Conventional Commits (коротко, в повелительном наклонении):

```text
docs: bootstrap SDAD doc pack
feat(server): serve /s/<site_id>/ static sites
fix(security): block ground_truth.json over HTTP
refactor(gen): extract deterministic asset helpers
test(validation): add traversal negative cases
chore: update tooling commands
```

Evidence (команды и результаты) держи в ExecPlan, а не в теле коммита.

---

## Перед коммитом (минимум)

Выполни релевантные gates (минимум — на изменённый модуль):

```bash
# пример
ruff format . && ruff check . && pytest -q
```

Затем:

```bash
git status --porcelain
git add -A
git commit -m "<message>"
git status --porcelain
```

Ожидаемо: после коммита `git status --porcelain` пустой.

---

## Запрещено без явного запроса

- `git push`, открытие PR, любые операции с remote.
- переписывание истории (`rebase`, `commit --amend`, `reset --hard`, `push --force`).
