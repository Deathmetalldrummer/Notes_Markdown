Четвертый слой ITCSS — **`4-elements`** (Base) — задаёт базовое визуальное оформление для чистых HTML-тегов без использования классов, идентификаторов и глобального `!important`.

```
src/styles/4-elements/
├── _base.scss             # html, body, a, hr, ::selection
├── _typography.scss       # h1-h6, p, blockquote, code, pre
├── _lists.scss            # ul, ol без классов
├── _tables.scss           # table, th, td, caption
├── _forms.scss            # input, button, textarea, select, label
├── _media.scss            # figure, figcaption, svg
├── _dialogs.scss          # dialog, ::backdrop
├── _interactive.scss      # details, summary
├── _feedback.scss        # progress, meter
├── _text-formatting.scss # mark, ins, del, sub, sup, time
└── _index.scss            # Полный экспорт слоя
```

### 1. src/styles/4-elements/\_base.scss

Этот файл задает базовые системные параметры документа, поведение страницы и стилизацию интерактивных базовых элементов.

```scss
/* ==========================================================================
   4-ELEMENTS: BASE
   ========================================================================== */

html {
  /* 1rem = 16px при дефолтных настройках браузера */
  font-size: 100%;

  /* Плавная прокрутка к якорям */
  scroll-behavior: smooth;

  /* Избавляет от сдвигов интерфейса при появлении/исчезновении вертикального скролла */
  scrollbar-gutter: stable;
}

body {
  font-family: var(--font-family-sans, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif);
  font-size: var(--font-size-base, 1rem);
  font-weight: var(--font-weight-regular, 400);
  line-height: var(--line-height-base, 1.5);
  color: var(--color-text-main, #212529);
  background-color: var(--color-bg-main, #ffffff);
}

/* Ссылки */
a {
  color: var(--color-primary, #1976d2);
  text-decoration: underline;
  /* Оптимальный отступ линии подчеркивания от текста */
  text-underline-offset: 0.2em;
  transition: color var(--duration-fast, 150ms) ease-in-out,
              text-decoration-color var(--duration-fast, 150ms) ease-in-out;

  &:hover {
    color: var(--color-primary-hover, #115293);
  }

  /* Доступность: отображение фокуса при навигации с клавиатуры */
  &:focus-visible {
    outline: 2px solid var(--color-primary, #1976d2);
    outline-offset: 3px;
    border-radius: var(--radius-sm, 2px);
  }
}

/* Разделительные линии */
hr {
  border: none;
  border-top: 1px solid var(--color-border, #e0e0e0);
  margin: var(--spacing-xl, 32px) 0;
}

/* Стилизация выделения текста пользователем */
::selection {
  background-color: var(--color-primary-light, #e3f2fd);
  color: var(--color-primary-dark, #0d47a1);
}
```

### 2. src/styles/4-elements/\_typography.scss

Определяет типографику текстовых блоков, цитат, заголовков и преформатированного кода на странице.

```scss
/* ==========================================================================
   4-ELEMENTS: TYPOGRAPHY
   ========================================================================== */

/* 1. Заголовки с адаптивными размерами через clamp() */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-heading, var(--font-family-sans));
  font-weight: var(--font-weight-bold, 700);
  line-height: var(--line-height-heading, 1.2);
  color: var(--color-text-heading, #111827);
  margin-bottom: 0.5em;
}

h1 { font-size: clamp(2rem, 4vw + 1rem, 3.25rem); }
h2 { font-size: clamp(1.65rem, 2.5vw + 1rem, 2.25rem); }
h3 { font-size: clamp(1.35rem, 1.5vw + 1rem, 1.75rem); }
h4 { font-size: clamp(1.15rem, 0.8vw + 1rem, 1.35rem); }
h5 { font-size: 1.1rem; }
h6 { font-size: 1rem; text-transform: uppercase; letter-spacing: 0.05em; }

/* 2. Текстовые блоки */
p {
  margin-bottom: 1em;

  &:last-child {
    margin-bottom: 0;
  }
}

b, strong {
  font-weight: var(--font-weight-bold, 700);
}

small {
  font-size: var(--font-size-sm, 0.875rem);
}

/* 3. Цитаты */
blockquote {
  margin: var(--spacing-lg, 24px) 0;
  padding: var(--spacing-md, 16px) var(--spacing-lg, 24px);
  border-left: 4px solid var(--color-primary, #1976d2);
  background-color: var(--color-surface-variant, #f8f9fa);
  border-radius: 0 var(--radius-md, 6px) var(--radius-md, 6px) 0;

  p:last-child {
    margin-bottom: 0;
  }
}

/* 4. Код и преформатированный текст */
code, kbd, pre, samp {
  font-family: var(--font-family-mono, ui-monospace, 'Cascadia Code', monospace);
  font-size: 0.875em;
}

code {
  padding: 0.2em 0.4em;
  background-color: var(--color-surface-variant, #f1f3f5);
  border-radius: var(--radius-sm, 4px);
  color: var(--color-text-code, #d63384);
}

pre {
  display: block;
  padding: var(--spacing-md, 16px);
  margin-bottom: 1em;
  overflow-x: auto;
  background-color: var(--color-surface-dark, #1e1e1e);
  color: #f8f8f2;
  border-radius: var(--radius-md, 8px);

  code {
    padding: 0;
    background-color: transparent;
    color: inherit;
  }
}
```

### 3. src/styles/4-elements/\_lists.scss

Задает стилизацию для стандартных нумерованных и маркированных списков, не имеющих классов.

```scss
/* ==========================================================================
   4-ELEMENTS: LISTS
   ========================================================================== */

/* Применяется строго к семантическим спискам без классов */
ul:not([class]),
ol:not([class]) {
  margin-bottom: 1em;
  padding-left: 1.5em;

  li {
    margin-bottom: 0.25em;

    /* Окрашивание маркеров списка в акцентный цвет */
    &::marker {
      color: var(--color-primary, #1976d2);
    }
  }
}

ul:not([class]) { list-style-type: disc; }
ol:not([class]) { list-style-type: decimal; }
```

### 4. src/styles/4-elements/\_tables.scss

Задает правила оформления таблиц данных, ячеек заголовков и подписей по умолчанию.

```scss
/* ==========================================================================
   4-ELEMENTS: TABLES
   ========================================================================== */

table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 1em;
  text-align: left;
}

th, td {
  padding: var(--spacing-sm, 8px) var(--spacing-md, 12px);
  border-bottom: 1px solid var(--color-border, #e0e0e0);
}

th {
  font-weight: var(--font-weight-bold, 700);
  background-color: var(--color-surface-variant, #f8f9fa);
  color: var(--color-text-heading, #111827);
}

caption {
  padding: var(--spacing-xs, 4px);
  font-size: var(--font-size-sm, 0.875rem);
  color: var(--color-text-muted, #6c757d);
  text-align: left;
}
```

### 5. src/styles/4-elements/\_forms.scss

Задает аккуратный базовый внешний вид элементов форм при их использовании без сторонних UI-библиотек.

```scss
/* ==========================================================================
   4-ELEMENTS: FORMS
   ========================================================================== */

/* Базовые текстовые поля ввода и выпадающие списки */
input,
textarea,
select {
  width: 100%;
  padding: var(--spacing-sm, 8px) var(--spacing-md, 12px);
  border: 1px solid var(--color-border, #ccc);
  border-radius: var(--radius-md, 6px);
  background-color: var(--color-surface, #ffffff);
  color: var(--color-text-main, #212529);
  transition: border-color var(--duration-fast, 150ms) ease,
              box-shadow var(--duration-fast, 150ms) ease;

  &::placeholder {
    color: var(--color-text-muted, #6c757d);
    opacity: 1;
  }

  &:focus {
    outline: none;
    border-color: var(--color-primary, #1976d2);
    box-shadow: 0 0 0 3px var(--color-primary-focus, rgba(25, 118, 210, 0.25));
  }

  &:disabled {
    background-color: var(--color-surface-disabled, #e9ecef);
    color: var(--color-text-disabled, #adb5bd);
    cursor: not-allowed;
  }
}

/* Чекбоксы и радиокнопки с акцентным цветом */
input[type="checkbox"],
input[type="radio"] {
  width: auto;
  margin-right: 0.5em;
  cursor: pointer;
  accent-color: var(--color-primary, #1976d2);
}

/* Базовые кнопки */
button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-sm, 8px) var(--spacing-md, 16px);
  font-weight: var(--font-weight-medium, 500);
  border-radius: var(--radius-md, 6px);
  border: 1px solid transparent;
  background-color: var(--color-primary, #1976d2);
  color: #ffffff;
  transition: background-color var(--duration-fast, 150ms) ease,
              transform var(--duration-fast, 150ms) ease;

  &:hover {
    background-color: var(--color-primary-hover, #115293);
  }

  &:active {
    transform: translateY(1px);
  }

  &:focus-visible {
    outline: none;
    box-shadow: 0 0 0 3px var(--color-primary-focus, rgba(25, 118, 210, 0.4));
  }

  &:disabled {
    opacity: 0.6;
    cursor: not-allowed;
    transform: none;
  }
}

/* Текстовая область с вертикальным изменением размера */
textarea {
  min-height: 100px;
  resize: vertical;
}

/* Подписи к полям ввода */
label {
  display: inline-block;
  margin-bottom: var(--spacing-xs, 4px);
  font-weight: var(--font-weight-medium, 500);
  font-size: var(--font-size-sm, 0.875rem);
}
```

### 6. src/styles/4-elements/\_media.scss

Определяет стилизацию иллюстраций figure, подписей к ним и векторной графики svg.

```scss
/* ==========================================================================
   4-ELEMENTS: MEDIA
   ========================================================================== */

figure {
  margin: var(--spacing-lg, 24px) 0;

  figcaption {
    margin-top: var(--spacing-xs, 4px);
    font-size: var(--font-size-sm, 0.875rem);
    color: var(--color-text-muted, #6c757d);
    text-align: center;
  }
}

svg {
  /* Автоматически наследует цвет текста родительского контекста */
  fill: currentColor;
}
```

### 7. src/styles/4-elements/\_dialogs.scss

Задает стилизацию для нативного HTML5-тега `<dialog>` и затемнения фона страницы `::backdrop`.

```scss
/* ==========================================================================
   4-ELEMENTS: DIALOGS
   ========================================================================== */

dialog {
  padding: var(--spacing-xl, 32px);
  border: 1px solid var(--color-border, #e0e0e0);
  border-radius: var(--radius-lg, 12px);
  background-color: var(--color-surface, #ffffff);
  color: var(--color-text-main, #212529);
  box-shadow: var(--shadow-lg, 0 10px 15px -3px rgba(0, 0, 0, 0.1));
  max-width: min(90vw, 600px);

  /* Эффект матового затемнения фона под модальным окном */
  &::backdrop {
    background-color: rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(4px);
  }
}
```

### 8. src/styles/4-elements/\_interactive.scss

Оформляет нативные интерактивные элементы раскрывающегося контента `<details>` и `<summary>`.

```scss
/* ==========================================================================
   4-ELEMENTS: INTERACTIVE
   ========================================================================== */

details {
  padding: var(--spacing-md, 16px);
  border: 1px solid var(--color-border, #e0e0e0);
  border-radius: var(--radius-md, 8px);
  background-color: var(--color-surface, #ffffff);

  &[open] {
    padding-bottom: var(--spacing-md, 16px);

    summary {
      margin-bottom: var(--spacing-sm, 8px);
      border-bottom: 1px solid var(--color-border, #e0e0e0);
      padding-bottom: var(--spacing-xs, 4px);
    }
  }
}

summary {
  font-weight: var(--font-weight-medium, 500);
  color: var(--color-text-heading, #111827);
  user-select: none;
  transition: color var(--duration-fast, 150ms) ease;

  &:hover {
    color: var(--color-primary, #1976d2);
  }
}
```

### 9. src/styles/4-elements/\_feedback.scss

Определяет кроссбраузерное оформление полос прогресса `<progress>` и измерительных шкал `<meter>`.

```scss
/* ==========================================================================
   4-ELEMENTS: FEEDBACK
   ========================================================================== */

progress,
meter {
  width: 100%;
  height: 8px;
  border: none;
  border-radius: var(--radius-full, 9999px);
  background-color: var(--color-surface-variant, #f1f3f5);
  overflow: hidden;

  /* Blink / WebKit */
  &::-webkit-progress-bar {
    background-color: var(--color-surface-variant, #f1f3f5);
  }

  &::-webkit-progress-value {
    background-color: var(--color-primary, #1976d2);
    border-radius: var(--radius-full, 9999px);
  }

  /* Firefox */
  &::-moz-progress-bar {
    background-color: var(--color-primary, #1976d2);
    border-radius: var(--radius-full, 9999px);
  }
}
```

### 10. src/styles/4-elements/\_text-formatting.scss

Задает стилизацию для семантических элементов разметки текста: сносок, цитат, правок и меток времени.

```scss
/* ==========================================================================
   4-ELEMENTS: TEXT FORMATTING
   ========================================================================== */

mark {
  background-color: var(--color-warning-light, #fef08a);
  color: var(--color-warning-dark, #854d0e);
  padding: 0.1em 0.3em;
  border-radius: var(--radius-sm, 2px);
}

ins {
  text-decoration: underline;
  background-color: var(--color-success-light, #dcfce7);
  color: var(--color-success-dark, #166534);
}

del {
  text-decoration: line-through;
  opacity: 0.7;
}

sub,
sup {
  font-size: 0.75em;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sup { top: -0.5em; }
sub { bottom: -0.25em; }

time {
  /* Фиксированная ширина цифр для равномерного отображения дат и времени */
  font-variant-numeric: tabular-nums;
}
```

### 11. src/styles/4-elements/\_index.scss

Объединяет все стили слоя `4-elements` для подключения в основной файл стилей приложения.

```scss
/* ==========================================================================
   4-ELEMENTS: INDEX
   ========================================================================== */

@use 'base';
@use 'typography';
@use 'lists';
@use 'tables';
@use 'forms';
@use 'media';
@use 'dialogs';
@use 'interactive';
@use 'feedback';
@use 'text-formatting';
```
