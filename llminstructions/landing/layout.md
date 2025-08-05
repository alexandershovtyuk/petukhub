# 📐 layout/grid-columns.md — Grid Columns Specification (Full)

> **Версия:** `v5-full`  
> **Назначение:** Полное описание поведения сеток, контейнеров и токенов на всех брейкпоинтах.  
> **Подходит для:** CSS Grid, React, UI генерация через LLM (Gemini, GPT), Design Systems

---

## ✅ Архитектурные принципы

- Используется **Mobile First** стратегия (базовые стили от `0px`, адаптация вверх).
- Все layout‑структуры реализуются на **CSS Grid**, не Flexbox.
- Количество колонок, отступы (`gap`) и Safe Zone — строго фиксированы по брейкпоинтам.
- **Контейнер** — это центральный блок любого layout'а, центрируется через `margin: auto`.
- **Safe Zone** всегда задаётся **только через `padding-left` / `padding-right`**, ни при каких условиях не используется `margin`.
- Все значения параметров вынесены в **CSS Custom Properties** (aka Design Tokens).

---

## Матрица параметров по брейкпоинтам

| Брейкпоинт | Диапазон (px) | Grid Columns | Column Gap | Safe Zone | Container Padding | Container Max-Width |
|------------|----------------|--------------|------------|-----------|-------------------|----------------------|
| `base`     | 0 – 479        | 4            | 16px       | 16px      | 16px              | `none`              |
| `2xs`      | 480 – 639      | 4            | 16px       | 16px      | 16px              | `none`              |
| `xs`       | 640 – 767      | 6            | 16px       | 20px      | 20px              | `none`              |
| `s`        | 768 – 1023     | 6            | 16px       | 20px      | 20px              | `none`              |
| `m`        | 1024 – 1279    | 6            | 16px       | 20px      | 20px              | `none`              |
| `l`        | 1280 – 1439    | 12           | 24px       | 24px      | 24px              | `none`              |
| `xl`       | 1440 – 1535    | 12           | 24px       | 24px      | 24px              | `1440px`            |
| `2xl`      | 1536 – 1919    | 12           | 24px       | 24px      | 24px              | `1440px`            |
| `3xl`      | 1920+          | 12           | 24px       | 24px      | 24px              | `1440px`            |


### 📐 Breakpoints

| Название токена | Значение | Комментарий для LLM                                                                                     |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------- |
| `--bp-base`     | `0px`    | Минимальная ширина экрана по умолчанию (mobile-first). Используется, когда не задан ни один брейкпоинт. |
| `--bp-xs`       | `480px`  | Малые экраны, например, смартфоны в горизонтальной ориентации.                                          |
| `--bp-s`        | `640px`  | Малые планшеты или компактные десктопы.                                                                 |
| `--bp-m`        | `768px`  | Планшеты. Начальная точка для большинства layout-изменений.                                             |
| `--bp-l`        | `1024px` | Малые десктопы. Используется для перехода к 12-колоночной сетке.                                        |
| `--bp-xl`       | `1280px` | Стандартные десктопы. Применяется фиксированная ширина контейнера.                                      |
| `--bp-2xl`      | `1440px` | Широкие экраны. Максимальная ширина контейнера.                                                         |
| `--bp-3xl`      | `1920px` | FullHD и выше. Используется для высокоразрешённых layout.                                               |


### 📐 Breakpoints (max-width)

| Название токена | Значение | Комментарий для LLM                                                              |
| --------------- | -------- | -------------------------------------------------------------------------------- |
| `--bp-base-max` | `479px`  | Верхняя граница начального брейкпоинта (используется в max-width media-queries). |
| `--bp-xs-max`   | `639px`  | Верхняя граница для `--bp-xs`.                                                   |
| `--bp-s-max`    | `767px`  | Верхняя граница для `--bp-s`.                                                    |
| `--bp-m-max`    | `1023px` | Верхняя граница для `--bp-m`.                                                    |
| `--bp-l-max`    | `1279px` | Верхняя граница для `--bp-l`.                                                    |
| `--bp-xl-max`   | `1439px` | Верхняя граница для `--bp-xl`.                                                   |
| `--bp-2xl-max`  | `1919px` | Верхняя граница для `--bp-2xl`.                                                  |

### 📐 Grid Gap Tokens

| Название токена | Значение | Комментарий для LLM                                               |
| --------------- | -------- | ----------------------------------------------------------------- |
| `--gap-base`    | `16px`   | Базовый отступ между колонками сетки (используется по умолчанию). |
| `--gap-s`       | `16px`   | Используется при ширине от `--bp-s`.                              |
| `--gap-m`       | `16px`   | Используется при ширине от `--bp-m`.                              |
| `--gap-l`       | `24px`   | Применяется на десктопах от `--bp-l`.                             |
| `--gap-xl`      | `24px`   | Увеличенный отступ для больших экранов.                           |
| `--gap-2xl`     | `24px`   | Стабильный отступ для всех экранов ≥1440px.                       |

🧱 Safe Zone Padding (Horizontal Container Padding)


### 📐 Safe Zone Padding (Horizontal Container Padding)

| Название токена              | Значение | Комментарий для LLM                                            |
| ---------------------------- | -------- | -------------------------------------------------------------- |
| `--container-safe-zone-base` | `16px`   | Горизонтальный паддинг контейнера по умолчанию (mobile-first). |
| `--container-safe-zone-2xs`  | `16px`   | Используется для самых малых экранов (до `--bp-xs`).           |
| `--container-safe-zone-xs`   | `20px`   | Безопасная зона для экранов от `--bp-xs` (≥480px).             |
| `--container-safe-zone-s`    | `20px`   | Для малых планшетов и экранов от `--bp-s` (≥640px).            |
| `--container-safe-zone-m`    | `20px`   | Для стандартных планшетов и экранов от `--bp-m`.               |
| `--container-safe-zone-l`    | `24px`   | Увеличенный паддинг для десктопов от `--bp-l`.                 |
| `--container-safe-zone-xl`   | `24px`   | Используется на широких экранах от `--bp-xl`.                  |
| `--container-safe-zone-2xl`  | `24px`   | Используется на экранах от `--bp-2xl` (≥1440px).               |
| `--container-safe-zone-3xl`  | `24px`   | Используется на экранах от `--bp-3xl` (≥1920px).               |



---

## 🎛 :root переменные (CSS Custom Properties)

```css
:root {

  /* максимальная ширина контейнера */
  --container-max-width: 1440px;

  /* Минимальные брейкпоинты */
  --bp-base: 0px;
  --bp-2xs: 480px;
  --bp-xs: 640px;
  --bp-s: 768px;
  --bp-m: 1024px;
  --bp-l: 1280px;
  --bp-xl: 1440px;
  --bp-2xl: 1536px;
  --bp-3xl: 1920px;

  /* Максимальные брейкпоинты */
  --bp-base-max: 479px;
  --bp-2xs-max: 639px;
  --bp-xs-max: 767px;
  --bp-s-max: 1023px;
  --bp-m-max: 1279px;
  --bp-l-max: 1439px;
  --bp-xl-max: 1535px;
  --bp-2xl-max: 1919px;

  /* Safe Zone по брейкпоинтам (горизонтальные отступы контейнера) */
  --container-safe-zone-base: 16px;
  --container-safe-zone-2xs: 16px;
  --container-safe-zone-xs: 20px;
  --container-safe-zone-s: 20px;
  --container-safe-zone-m: 20px;
  --container-safe-zone-l: 24px;
  --container-safe-zone-xl: 24px;
  --container-safe-zone-2xl: 24px;
  --container-safe-zone-3xl: 24px;

 /* Gap по брейкпоинтам (отступы между колонками) */
  --gap-base: 16px;
  --gap-2xs: 16px;
  --gap-xs: 16px;
  --gap-s: 16px;
  --gap-m: 16px;
  --gap-l: 24px;
  --gap-xl: 24px;
  --gap-2xl: 24px;
  --gap-3xl: 24px;
}
```

---

## 📐 Поведение контейнера

- Контейнер всегда имеет `width: 100%`, **центрируется** через `margin-left/right: auto`.
- Safe Zone устанавливается через токены `--container-safe-zone-*`.
- Начиная с брейкпоинта `xl` (1440px), применяется `---container-max-width`.

---

## 🧩 Пример адаптивной сетки с токенами

```css
/* 🟢 None: 0–479px */
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: var(--gap-default);
  padding-left: var(--container-safe-zone-base);
  padding-right: var(--container-safe-zone-base);
  margin: 0 auto;
}

/* 🟢 XS: ≥640px */
@media (min-width: var(--bp-xs)) {
  .container {
    grid-template-columns: repeat(6, 1fr);
    column-gap: var(--gap-xs);
    padding-left: var(--container-safe-zone-xs);
    padding-right: var(--container-safe-zone-xs);
  }
}

/* 🟢 S: ≥768px */
@media (min-width: var(--bp-s)) {
  .container {
    grid-template-columns: repeat(6, 1fr);
    column-gap: var(--gap-s);
    padding-left: var(--container-safe-zone-s);
    padding-right: var(--container-safe-zone-s);
  }
}

/* 🟢 M: ≥1024px */
@media (min-width: var(--bp-m)) {
  .container {
    grid-template-columns: repeat(6, 1fr);
    column-gap: var(--gap-m);
    padding-left: var(--container-safe-zone-m);
    padding-right: var(--container-safe-zone-m);
  }
}

/* 🟢 L: ≥1280px */
@media (min-width: var(--bp-l)) {
  .container {
    grid-template-columns: repeat(12, 1fr);
    column-gap: var(--gap-l);
    padding-left: var(--container-safe-zone-l);
    padding-right: var(--container-safe-zone-l);
  }
}

/* 🟢 XL: ≥1440px */
@media (min-width: var(--bp-xl)) {
  .container {
    max-width: var(--container-max-width);
    column-gap: var(--gap-xl);
    padding-left: var(--container-safe-zone-xl);
    padding-right: var(--container-safe-zone-xl);
  }
}
```

---

## 🧱 Дополнительные токены и утилиты (расширение)

### 🔠 Поведение `grid-column: span`

LLM может использовать `grid-column: span N`:

- для 4‑колоночной сетки: допустимы `1–4`
- для 6‑колоночной: `1–6`
- для 12‑колоночной: `1–12`

```css
.card {
  grid-column: span 6;
}
```

---

### 🧩 Вложенные grid-сетки (nested grid)

Разрешено создавать вложенные сетки внутри карточек, секций, форм.

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}
```

> Вложенные гриды НЕ влияют на основной layout.

---

## ✅ Поведение генерации LLM

LLM обязана:

- Генерировать layout через `display: grid`
- Использовать `grid-template-columns: repeat(N, 1fr)` на основе брейкпоинтов
- Всегда центрировать контейнер (`margin: auto`)
- Применять отступы (`padding`) через `--container-safe-zone-*`
- Устанавливать `--container-max-width` на брейкпоинте `xl`
- Использовать `--bp-*` и `--bp-*-max` в медиазапросах
- Соблюдать **mobile-first** архитектуру
- Сопровождать код **комментариями**