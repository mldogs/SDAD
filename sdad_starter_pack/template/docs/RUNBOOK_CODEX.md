# RUNBOOK: запуск Codex в этом репозитории

Этот репозиторий оптимизирован под автономную разработку (SDAD).
Цель настроек — **минимум вопросов** при сохранении “песочницы” и предсказуемости.

---

## TL;DR (рекомендуемо)

После того как Codex пометил проект как trusted, просто запускай:

```bash
codex
```

По умолчанию используется `.codex/config.toml`:

- `--sandbox workspace-write`
- `--ask-for-approval on-failure` (вопросы только если нужна эскалация)
- `web_search = "cached"`

---

## Профили

```bash
codex --profile full_auto
codex --profile quiet
codex --profile readonly_review
```

Что делают профили см. `.codex/config.toml`.

---

## В интерактивной сессии

- `/permissions` — посмотреть/изменить sandbox и approvals
- `/status` — быстрый статус текущих режимов

---

## Если нужно больше прав

- Добавь доступ к конкретной папке: `codex --add-dir <path>`
- Не используй `--yolo` / `--dangerously-bypass-approvals-and-sandbox` без отдельного решения (это выключает ключевые safety‑гарантии)

---

## Официальные справки OpenAI

- Security: https://developers.openai.com/codex/cli/security/
- CLI Reference: https://developers.openai.com/codex/cli/reference/
- Config: https://developers.openai.com/codex/cli/config
