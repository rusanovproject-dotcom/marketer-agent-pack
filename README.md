# Marketer Agent Pack

**AI-маркетолог для клиентских офисов.** Смесь Хормози + стиль 99 франков.

Ведёт клиентскую базу с дословными цитатами и метрикой actuality 1-10. Двигает проект гипотезами (max 5 активных + Key Hypothesis). Режет красивые пустышки, защищает сильные идеи.

---

## Установка

Скопируй содержимое пака в свой клиентский AI-офис:

```bash
# Из репозитория AI-офиса (клонированного локально)
cp -r /path/to/marketer-agent-pack/* _agent-packs/marketer/
```

Потом в Claude Code — запусти:
```
/install-agent marketer
```

Если у офиса нет скилла `/install-agent` — скопируй файлы вручную по путям из `install.md`.

---

## Как работает

### Два главных триггера

**1. Первый раз — ревизия.** Клиент говорит:
- *«сделай ревизию маркетинга»*
- *«распакуй мою ЦА»*
- *«где у меня деньги»*

→ Агент 15-20 мин читает проект, задаёт вопросы, выдаёт:
- 3 главные находки (что увидел)
- Рекомендованный сегмент ЦА (из 3 проверенных через Starving Crowd тест)
- 3 гипотезы для проверки
- Создаёт в проекте: `ICP.md` + `audience.md` + `customers.md` + `hypotheses.md`

**2. После каждой встречи — log-deal.** Клиент говорит:
- *«провёл диагностику»* / *«был созвон»*
- *«клиент оплатил»* / *«клиент отказался»*
- *«вот транскрипт встречи»*

→ Агент записывает карточку клиента с:
- Ссылкой на транскрипт (wiki-связь)
- Дословными цитатами (боль / желание / возражения / про конкурентов)
- Оффером как Никита реально сказал клиенту
- **Actuality 1-10** — метрика силы оффера
- **«Что не хватает до 10»** → автоматом в возражения

---

## Структура

```
marketer/
├── CLAUDE.md                          @soul + @core + @overrides
├── soul.md                            🔥 Душа (≤50 строк)
├── core.md                            Операционный мозг (≤200 строк)
├── overrides.md                       Client template (клиент правит сам)
├── memory.md                          Память агента (append-only)
├── failures.md                        Лог фейлов
├── install.md                         Манифест установки
│
├── knowledge/                         Библия агента (клиент не читает)
│   ├── hormozi-offer-market.md       Value Equation, Grand Slam, Starving Crowd
│   ├── audience-framework.md         3W, БПСВ, 4 уровня осознанности, продуктовая матрица
│   ├── schwartz-awareness.md         5 Levels, Market Sophistication
│   └── classics-compact.md           Kennedy, Dunford, Christensen, Goldratt
│
├── templates/                         Шаблоны для проекта клиента
│   ├── customers.template.md         Клиентская база с actuality 1-10
│   └── hypotheses.template.md        Тест-процесс (5 active + Key + теги)
│
└── skills/  (6 скиллов)
    ├── marketer-revision/SKILL.md    Первичная ревизия (знакомство → ревью → план)
    ├── marketer-log-deal/SKILL.md    Запись клиента после встречи
    ├── marketer-audience/SKILL.md    Глубокая распаковка ЦА
    ├── marketer-ladder/SKILL.md      Продуктовая лестница
    ├── marketer-funnel/SKILL.md      Воронка под лестницу
    └── marketer-checkin/SKILL.md     Еженедельный ревью
```

---

## Ключевые принципы агента

### Hypothesis-Driven System
- Макс **5 активных** гипотез
- Одна **⭐ Key Hypothesis** — главная сейчас
- 8 тегов типов → автосинхронизация с файлами воронки (`[PRODUCT]`, `[PRICE]`, `[OFFER]`, `[CHANNEL]`, `[LM]`, `[FUNNEL]`, `[MESSAGE]`, `[POSITIONING]`)
- Жизненный цикл: NEW → 🧪 TESTING → ✅ VALIDATED / ❌ INVALIDATED

### Customer Intelligence
- Линк на транскрипт в каждой карточке
- **Дословные цитаты** (не перефразировки)
- Оффер как был озвучен клиенту
- Actuality 1-10 — главный прибор силы оффера
- «Что не хватает до 10» автоматом в возражения на доработку оффера

### Layered Architecture
- `core.md` обновляется из template при апдейте агента
- `overrides.md` — клиент правит, не затирается
- `memory.md` агент пишет сам append-only
- `CLAUDE.md` = точка входа с `@imports`

---

## Статус

**v1.0** — готовы все 6 скиллов:

| Скилл | Статус | Что делает |
|-------|--------|------------|
| `/marketer-revision` | ✅ v1 | Первичная ревизия проекта |
| `/marketer-log-deal` | ✅ v1 | Запись клиента после встречи |
| `/marketer-audience` | ✅ v1 | Глубокая распаковка ЦА (БПСВ + awareness + VoC) |
| `/marketer-ladder` | ✅ v1 | Продуктовая лестница LM→TW→Core→PM |
| `/marketer-funnel` | ✅ v1 | Воронка + Channel-First + bottleneck |
| `/marketer-checkin` | ✅ v1 | Еженедельный ревью гипотез + customers |

---

## ДНК

- **Хормози** — Value Equation, Grand Slam, Starving Crowd, *«specificity is credibility»*
- **3W+БПСВ фреймворк** — 3W, БПСВ, 4 уровня осознанности, *«подотрись портретом ЦА»*, *«маркетинг = гипотезы»*
- **Schwartz** — 5 Levels of Awareness, Market Sophistication
- **Kennedy / Dunford / Christensen / Goldratt** — Magnificent 7, позиционирование, JTBD, bottleneck

---

*Создано Никитой Русановым + Claude. MIT License.*
