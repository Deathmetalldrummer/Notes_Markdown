Третий слой ITCSS — **`3-generic`** — это первый слой в каскаде, который генерирует реальный CSS-код. Его задача — обнулить браузерные различия (Reset, Normalize) и заложить фундамент с минимальной специфичностью без использования классов и ID.

```
src/styles/3-generic/
├── _box-sizing.scss      # Единый алгоритм расчета border-box
├── _reset.scss           # Современный сброс стилей (Modern CSS Reset)
├── _normalize.scss       # Коррекция межбраузерных аномалий
├── _scroll.scss          # Поведение скролла и кастомный скроллбар
├── _mobile-fixes.scss    # Фиксы под мобильные браузеры (iOS/Android)
├── _print.scss           # Базовые стили для печати
├── _a11y-contrast.scss   # Поддержка режима высокой контрастности
└── _index.scss           # Централизованный импорт слоя через @use
```

### 1. src/styles/3-generic/\_box-sizing.scss

Устанавливает глобальный алгоритм расчета геометрии блоков `border-box` для всех элементов дерева DOM, включая псевдоэлементы.

```scss
/* ==========================================================================
   3-GENERIC: BOX-SIZING
   ========================================================================== */

/* Включает учет внутренних отступов и рамок в общую ширину и высоту */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### 2. src/styles/3-generic/\_reset.scss

Реализует современный сброс дефолтных стилей браузера для нормализации отступов, адаптивности контента и элементов форм.

```scss
/* ==========================================================================
   3-GENERIC: RESET
   ========================================================================== */

/* 1. Обнуляем дефолтные внешние отступы */
* {
  margin: 0;
}

/* 2. Высота 100% для корневых элементов */
html,
body {
  height: 100%;
}

/* 3. Базовые параметры документа и сглаживание шрифтов */
body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeSpeed;
}

/* 4. Адаптивный медиа-контент */
img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

/* 5. Наследование параметров шрифта элементами форм */
input,
button,
textarea,
select {
  font: inherit;
  color: inherit;
}

/* 6. Убираем рамки и стандартный фон для элементов ввода */
button,
input,
textarea {
  border: none;
  background: none;
}

/* 7. Указатель мыши для интерактивных элементов */
button,
select,
a {
  cursor: pointer;
}

/* 8. Запрет изменения размера textarea по горизонтали */
textarea {
  resize: vertical;
}

/* 9. Сброс маркеров только для списков, ИМЕЮЩИХ класс
   (сохраняет маркеры для стандартного семантического текста без классов) */
ul[class],
ol[class] {
  list-style: none;
  padding: 0;
}

/* 10. Предотвращение вылезания длинных слов за границы контейнеров */
p, h1, h2, h3, h4, h5, h6 {
  overflow-wrap: break-word;
}

/* 11. Адаптация под корневой элемент Angular */
app-root {
  /* Изолирует локальный контекст наложения z-index */
  isolation: isolate;
  min-height: 100%;
  display: flex;
  flex-direction: column;
}
```

### 3. src/styles/3-generic/\_normalize.scss

Исправляет кроссбраузерные баги рендеринга и обеспечивает поддержку доступности для пользователей с ограничениями моторики.

```scss
/* ==========================================================================
   3-GENERIC: NORMALIZE
   ========================================================================== */

/* Корректное скрытие элементов с атрибутом hidden */
[hidden] {
  display: none !important;
}

/* Сброс нестандартных элементов управления поиском в Safari/WebKit */
input[type="search"]::-webkit-search-decoration,
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-results-button,
input[type="search"]::-webkit-search-results-decoration {
  -webkit-appearance: none;
}

/* Нормализация отображения маркера summary в Safari */
summary {
  display: list-item;
  cursor: pointer;
}

/* Отключение анимаций при системном требовании пользователя (A11y) */
@media (prefers-reduced-motion: reduce) {
  html:focus-within {
    scroll-behavior: auto;
  }
  
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### 4. src/styles/3-generic/\_scroll.scss

Управляет поведением горизонтальной прокрутки страницы и задает кастомную стилизацию полос прокрутки для браузеров WebKit/Blink.

```scss
/* ==========================================================================
   3-GENERIC: SCROLL
   ========================================================================== */

/* 1. Предотвращает нежелательный горизонтальный скролл страницы */
html {
  overflow-x: hidden;
}

/* 2. Кастомизация скроллбара для браузеров на базе Blink/WebKit */
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background-color: var(--color-surface-variant, #f1f1f1);
}

::-webkit-scrollbar-thumb {
  background-color: var(--color-border, #ccc);
  border-radius: var(--radius-full, 9999px);

  &:hover {
    background-color: var(--color-text-muted, #888);
  }
}
```

### 5. src/styles/3-generic/\_mobile-fixes.scss

Устраняет специфические визуальные артефакты мобильных браузеров на iOS и Android.

```scss
/* ==========================================================================
   3-GENERIC: MOBILE FIXES
   ========================================================================== */

/* 1. Убирает полупрозрачное серое подсвечивание при тапе в iOS Safari */
a,
button,
input,
select,
textarea {
  -webkit-tap-highlight-color: transparent;
}

/* 2. Убирает принудительные скругления iOS Safari для элементов форм */
input,
textarea {
  -webkit-appearance: none;
  border-radius: 0;
}

/* 3. Предотвращает автоувеличение размера шрифта при повороте экрана в iOS */
html {
  -webkit-text-size-adjust: 100%;
}
```

### 6. src/styles/3-generic/\_print.scss

Определяет оптимизированные стили страницы при выводе документа на печать.

```scss
/* ==========================================================================
   3-GENERIC: PRINT
   ========================================================================== */

@media print {
  *,
  *::before,
  *::after {
    background: transparent !important;
    color: #000000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }

  /* Печатает абсолютный URL рядом с текстом ссылки */
  a[href]::after {
    content: " (" attr(href) ")";
  }

  /* Предотвращает разрыв страницы внутри ключевых блоков */
  pre,
  blockquote,
  tr,
  img {
    break-inside: avoid;
    page-break-inside: avoid;
  }
}
```

### 7. src/styles/3-generic/\_a11y-contrast.scss

Обеспечивает четкую видимость фокуса клавиатуры в режиме высокой контрастности Windows High Contrast Mode.

```scss
/* ==========================================================================
   3-GENERIC: A11Y CONTRAST
   ========================================================================== */

@media (forced-colors: active) {
  /* CanvasText — системный цвет текста ОС в режиме высокой контрастности */
  *:focus-visible {
    outline: 2px solid CanvasText !important;
  }
}
```

### 8. src/styles/3-generic/\_index.scss

Подключает все файлы сброса и нормализации слоя `3-generic` через директиву `@use` для включения в результирующий CSS.

```scss
/* ==========================================================================
   3-GENERIC: INDEX
   ========================================================================== */

@use 'box-sizing';
@use 'reset';
@use 'normalize';
@use 'scroll';
@use 'mobile-fixes';
@use 'print';
@use 'a11y-contrast';
```