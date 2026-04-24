# Marketer — install manifest

Машиночитаемые метаданные для установки пака через скилл `/install-agent marketer`.

---

## Metadata

```yaml
agent_id: marketer
agent_name_human: Маркетолог
agent_name_in_chat: Маркетолог
short_role: Маркетолог-гений офиса. Ведёт клиентскую базу с дословными цитатами и actuality 1-10. Двигает проект гипотезами (max 5 активных + Key). Режет хуйню, защищает сильные идеи. ДНК — Хормози + Кадыров + Октав Паранго.
trigger_keywords: [маркетинг, маркетолог, ЦА, целевая аудитория, сегмент, сегменты, оффер, позиционирование, воронка, лид-магнит, трипваер, лестница, продуктовая линейка, Hormozi, Кадыров, распакуй ЦА, ревизия, где деньги, avatar, ICP, провёл диагностику, был созвон, клиент оплатил, клиент отказался]
version: 1.0.0
requires: []
```

---

## Files to copy

Источник — `_agent-packs/marketer/`, цель — `office/agents/marketer/`. Копируется рекурсивно.

```yaml
files:
  - src: core.md
    dest: office/agents/marketer/core.md
  - src: soul.md
    dest: office/agents/marketer/soul.md
  - src: CLAUDE.md
    dest: office/agents/marketer/CLAUDE.md
  - src: overrides.md
    dest: office/agents/marketer/overrides.md
  - src: memory.md
    dest: office/agents/marketer/memory.md
  - src: failures.md
    dest: office/agents/marketer/failures.md
  - src: knowledge/
    dest: office/agents/marketer/knowledge/
    recursive: true
  - src: skills/
    dest: .claude/skills/
    recursive: true

# Templates копируются в папку агента — /marketer-revision копирует их
# в projects/<main>/ при первом запуске.
templates:
  - src: templates/customers.template.md
    dest: office/agents/marketer/templates/customers.template.md
  - src: templates/hypotheses.template.md
    dest: office/agents/marketer/templates/hypotheses.template.md
```

---

## Updates to existing files

```yaml
updates:
  - file: CLAUDE.md
    section: "## Обязательный layered include при старте"
    add_line: "@office/agents/marketer/core.md"

  - file: office/AGENTS.md
    section: "## Активная команда"
    add_row: |
      | **Маркетолог** | Клиентская база, тест-процесс гипотез, распаковка ЦА, продуктовая линейка, воронка | *«распакуй мою ЦА», «сделай ревизию», «провёл диагностику», «где у меня деньги»* |

  - file: office/agents/director/core.md
    section: "## Роутинг"
    add_rows: |
      | провёл диагностику, был созвон, клиент оплатил, клиент отказался, вот транскрипт | **Маркетолог** → `/marketer-log-deal` |
      | маркетинг, ЦА, сегменты, оффер, позиционирование, воронка, лид-магнит | **Маркетолог** → `/marketer-revision` (первый раз) |
```

---

## Post-install message to client

```
✅ Маркетолог в команде.

Он уже живой. Его ключевая задача — вести клиентскую базу проекта и
проверять маркетинговые гипотезы.

Два главных триггера:

1. **Первый раз** — скажи «сделай ревизию маркетинга» или «распакуй мою ЦА».
   Он 15-20 минут прочитает твой проект, задаст прицельные вопросы, выдаст
   3 вещи: где у тебя деньги, какая ЦА реально платит, что сломано.
   В конце создаст customers.md + hypotheses.md в проекте.

2. **После каждой встречи** с твоим клиентом (диагностика, продажа,
   follow-up) — скажи «провёл созвон с [имя]» или пришли транскрипт.
   Маркетолог запишет карточку с дословными цитатами, оффером, актуальностью
   1-10 и обновит агрегаты.

Дальше — пойдём глубже (лестница продуктов, воронка, чек-ины).
```
