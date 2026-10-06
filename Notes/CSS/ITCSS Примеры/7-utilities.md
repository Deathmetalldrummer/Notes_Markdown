Седьмой слой ITCSS — **`7-utilities`** (Trumps / Helpers) — это финальный слой архитектуры, обладающий **наивысшим приоритетом в каскаде**.

Его задача — точечно переопределять стили любых предыдущих слоев с помощью служебных классов с префиксом `u-` и директивы `!important`.

```
src/styles/7-utilities/
├── _display.scss       # Показ и скрытие (u-hidden, u-block)
├── _spacing.scss       # Внешние и внутренние отступы (u-mb-lg, u-p-0)
├── _text.scss          # Выравнивание и свойства шрифта (u-text-center, u-truncate)
├── _visibility.scss    # Скрытие контента для доступности (u-sr-only)
├── _position.scss      # Типы позиционирования и z-index (u-pos-relative, u-inset-0)
├── _sizing.scss        # Размеры и object-fit (u-w-100, u-fit-cover)
├── _interactivity.scss # Поведение мыши и выделения (u-pointer-events-none)
├── _overflow.scss      # Управление скроллом и переполнением (u-overflow-hidden)
├── _effects.scss       # Прозрачность и сброс теней (u-opacity-0, u-shadow-none)
└── _index.scss         # Главный файл экспорта слоя
```

### 1. src/styles/7-utilities/\_display.scss

Предоставляет атомарные классы для принудительного переключения модели отображения элементов.

```scss
/* ==========================================================================
   7-UTILITIES: DISPLAY
   ========================================================================== */

.u-hidden {
  display: none !important;
}

.u-block {
  display: block !important;
}

.u-inline-block {
  display: inline-block !important;
}

.u-flex {
  display: flex !important;
}
```

### 2. src/styles/7-utilities/\_spacing.scss

Содержит утилиты для быстрого сброса отступов или задания интервалов на основе дизайн-токенов проекта.

```scss
/* ==========================================================================
   7-UTILITIES: SPACING
   ========================================================================== */

/* Обнуление отступов */
.u-m-0  { margin: 0 !important; }
.u-mt-0 { margin-top: 0 !important; }
.u-mb-0 { margin-bottom: 0 !important; }
.u-p-0  { padding: 0 !important; }

/* Отступы на основе Design Tokens */
.u-mb-sm { margin-bottom: var(--spacing-sm, 8px) !important; }
.u-mb-md { margin-bottom: var(--spacing-md, 16px) !important; }
.u-mb-lg { margin-bottom: var(--spacing-lg, 24px) !important; }

.u-mt-sm { margin-top: var(--spacing-sm, 8px) !important; }
.u-mt-md { margin-top: var(--spacing-md, 16px) !important; }
.u-mt-lg { margin-top: var(--spacing-lg, 24px) !important; }
```

### 3. src/styles/7-utilities/\_text.scss

Управляет горизонтальным выравниванием текста, насыщенностью шрифта и однострочной обрезкой длинных строк.

```scss
/* ==========================================================================
   7-UTILITIES: TEXT
   ========================================================================== */

.u-text-left   { text-align: left !important; }
.u-text-center { text-align: center !important; }
.u-text-right  { text-align: right !important; }

.u-text-bold   { font-weight: var(--font-weight-bold, 700) !important; }
.u-text-muted  { color: var(--color-text-muted) !important; }

/* Принудительная обрезка текста в одну строку с многоточием */
.u-truncate {
  overflow: hidden !important;
  text-overflow: ellipsis !important;
  white-space: nowrap !important;
}
```

### 4. src/styles/7-utilities/\_visibility.scss

Содержит служебный класс для скрытия контента от зрячих пользователей с сохранением чтения скринридерами.

```scss
/* ==========================================================================
   7-UTILITIES: VISIBILITY
   ========================================================================== */

/* Визуально скрывает элемент, сохраняя доступность для Screen Readers */
.u-sr-only {
  position: absolute !important;
  width: 1px !important;
  height: 1px !important;
  padding: 0 !important;
  margin: -1px !important;
  overflow: hidden !important;
  clip: rect(0, 0, 0, 0) !important;
  white-space: nowrap !important;
  border: 0 !important;
}
```

### 5. src/styles/7-utilities/\_position.scss

Определяет классы для управления позиционированием в потоке документа, быстрым растягиванием слоев и Z-index.

```scss
/* ==========================================================================
   7-UTILITIES: POSITION
   ========================================================================== */

.u-pos-static    { position: static !important; }
.u-pos-relative  { position: relative !important; }
.u-pos-absolute  { position: absolute !important; }
.u-pos-fixed     { position: fixed !important; }
.u-pos-sticky    { position: sticky !important; }

/* Растягивание абсолютно позиционированного элемента на всю площадь родителя */
.u-inset-0 {
  top: 0 !important;
  right: 0 !important;
  bottom: 0 !important;
  left: 0 !important;
}

/* Управление Z-индексом */
.u-z-0    { z-index: 0 !important; }
.u-z-10   { z-index: 10 !important; }
.u-z-top  { z-index: 9999 !important; }
```

### 6. src/styles/7-utilities/\_sizing.scss

Задает утилиты для фиксации габаритов элементов и пропорционального масштабирования содержимого.

```scss
/* ==========================================================================
   7-UTILITIES: SIZING
   ========================================================================== */

.u-w-100 { width: 100% !important; }
.u-h-100 { height: 100% !important; }

.u-mw-100 { max-width: 100% !important; }
.u-mh-100 { max-height: 100% !important; }

/* Пропорциональное заполнение области медиаконтентом */
.u-fit-cover   { object-fit: cover !important; }
.u-fit-contain { object-fit: contain !important; }
```

### 7. src/styles/7-utilities/\_interactivity.scss

Управляет перехватом событий курсора мыши, возможностью выделения текста и формой указателя.

```scss
/* ==========================================================================
   7-UTILITIES: INTERACTIVITY
   ========================================================================== */

/* Игнорирование событий мыши (клики проходят сквозь элемент) */
.u-pointer-events-none { pointer-events: none !important; }
.u-pointer-events-auto { pointer-events: auto !important; }

/* Запрет/разрешение выделения текста */
.u-user-select-none { user-select: none !important; }
.u-user-select-text { user-select: text !important; }

/* Управление видом курсора */
.u-cursor-pointer     { cursor: pointer !important; }
.u-cursor-not-allowed { cursor: not-allowed !important; }
```

### 8. src/styles/7-utilities/\_overflow.scss

Предоставляет классы для быстрой изоляции контента при переполнении и активации полос прокрутки.

```scss
/* ==========================================================================
   7-UTILITIES: OVERFLOW
   ========================================================================== */

.u-overflow-hidden { overflow: hidden !important; }
.u-overflow-auto   { overflow: auto !important; }
.u-overflow-scroll { overflow: scroll !important; }

/* Раздельная прокрутка по осям X и Y */
.u-overflow-x-auto { overflow-x: auto !important; }
.u-overflow-y-auto { overflow-y: auto !important; }
```

### 9. src/styles/7-utilities/\_effects.scss

Управляет прозрачностью элементов и принудительным сбросом теней и рамок.

```scss
/* ==========================================================================
   7-UTILITIES: EFFECTS
   ========================================================================== */

.u-opacity-0   { opacity: 0 !important; }
.u-opacity-50  { opacity: 0.5 !important; }
.u-opacity-100 { opacity: 1 !important; }

.u-shadow-none { box-shadow: none !important; }
.u-border-none { border: none !important; }
```

### 10. src/styles/7-utilities/\_index.scss

Импортирует все служебные модули слоя `7-utilities` для завершения формирования итоговой сборки стилей.

```scss
/* ==========================================================================
   7-UTILITIES: INDEX
   ========================================================================== */

@use 'display';
@use 'spacing';
@use 'text';
@use 'visibility';
@use 'position';
@use 'sizing';
@use 'interactivity';
@use 'overflow';
@use 'effects';
```

### Использование в HTML

Утилиты используются для точечной коррекции разметки без создания новых компонентов или переписывания стилей:

```html
<!-- c-card — компонент, o-stack — объект, u-mb-0 и u-text-center — утилиты -->
<article class="c-card">
  <div class="c-card__body o-stack">
    <h3 class="c-card__title u-text-center">Заголовок по центру</h3>
    <p class="u-mb-0 u-text-muted">Текст без нижнего отступа и приглушенного цвета.</p>
  </div>
</article>
```

### Сводная таблица всех 7 слоев ITCSS

| Слой | Название | Что содержит | Генерирует CSS? | Префикс |
| --- | --- | --- | --- | --- |
| **1** | **Settings** | Переменные, токены, палитры | ❌ Нет | `--` |
| **2** | **Tools** | Миксины и функции SCSS | ❌ Нет | — |
| **3** | **Generic** | Reset, Normalize, Box-sizing | ✅ Да | — |
| **4** | **Elements** | Базовые стили для чистых HTML-тегов (`h1`, `p`, `a`) | ✅ Да | — |
| **5** | **Objects** | Каркас, геометрия и сетки (Layout) | ✅ Да | `o-` |
| **6** | **Components** | UI-компоненты с внешним видом (`.c-card`, `.c-btn`) | ✅ Да | `c-` |
| **7** | **Utilities** | Точечные хелперы и переопределения с `!important` | ✅ Да | `u-` |
