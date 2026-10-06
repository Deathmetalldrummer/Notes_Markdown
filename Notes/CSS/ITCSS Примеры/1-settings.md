Первый слой ITCSS — **`1-settings`** — отвечает за **конфигурацию** всей системы стилей. В нём содержатся только переменные, SCSS-карты и токены дизайна, не генерирующие чистый CSS-код при компиляции.

```
src/styles/1-settings/
├── _colors.scss          # Цветовая палитра и темы
├── _typography.scss      # Шрифты, размеры, веса
├── _spacing.scss         # Шкала отступов
├── _breakpoints.scss     # Точки останова медиазапросов
├── _radii.scss           # Радиусы скругления
├── _shadows.scss         # Тени
├── _z-index.scss         # Z-index
├── _transitions.scss     # Длительности и тайминги анимаций
├── _containers.scss      # Ширина макетов и сетка
├── _opacity.scss         # Шкала прозрачности и состояний
├── _vendor-tokens.scss   # Токены сторонних UI-библиотек
└── _index.scss           # Общий импорт всех файлов
```

### 1. src/styles/1-settings/\_colors.scss

Определяет базовую цветовую палитру проекта и семантические CSS-переменные для поддержки светлой и темной тем оформления.

```scss
/* ==========================================================================
   1-SETTINGS: COLORS
   ========================================================================== */

/* Палитра бренда (raw values) для внутреннего использования в SCSS */
$raw-colors: (
  'blue-500': #1976d2,
  'blue-700': #115293,
  'gray-100': #f8f9fa,
  'gray-900': #121212
);

/* Глобальные семантические токены дизайн-системы */
:root {
  /* Интерполяция #{} передает вычисленное значение из карты SCSS в CSS Custom Property */
  --color-primary: #{map-get($raw-colors, 'blue-500')};
  --color-primary-hover: #{map-get($raw-colors, 'blue-700')};
  --color-bg-main: #ffffff;
  --color-text-main: #212529;
}

/* Переопределение токенов для темной темы по дата-атрибуту */
[data-theme="dark"] {
  --color-bg-main: #{map-get($raw-colors, 'gray-900')};
  --color-text-main: #e0e0e0;
}
```

### 2. src/styles/1-settings/\_typography.scss

Задает системные гарнитуры шрифтов, базовые размеры текста и шкалу насыщенности шрифтов проекта.

```scss
/* ==========================================================================
   1-SETTINGS: TYPOGRAPHY
   ========================================================================== */

$font-family-sans: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
$font-family-mono: ui-monospace, 'Cascadia Code', monospace;

:root {
  --font-family-sans: #{$font-family-sans};
  --font-family-mono: #{$font-family-mono};

  /* Шкала размеров шрифта (на основе базовых 16px) */
  --font-size-xs: 0.75rem;   /* 12px */
  --font-size-sm: 0.875rem;  /* 14px */
  --font-size-base: 1rem;    /* 16px */
  --font-size-lg: 1.125rem;  /* 18px */

  --font-weight-regular: 400;
  --font-weight-bold: 700;
}
```

### 3. src/styles/1-settings/\_breakpoints.scss

Содержит карту контрольных точек адаптивности (Breakpoints) для использования в адаптивных миксинах слоя Tools.

```scss
/* ==========================================================================
   1-SETTINGS: BREAKPOINTS
   ========================================================================== */

/* Карта точек останова для адаптивной верстки (!default допускает переопределение) */
$breakpoints: (
  'mobile-sm': 320px,
  'mobile-lg': 480px,
  'tablet': 768px,
  'desktop': 1024px,
  'desktop-wide': 1440px
) !default;
```

### 4. src/styles/1-settings/\_spacing.scss

Определяет пропорциональную шкалу внутренних и внешних отступов (Spacing scale) для создания единого ритма интерфейса.

```scss
/* ==========================================================================
   1-SETTINGS: SPACING
   ========================================================================== */

/* SCSS-карта отступов с шагом 4px/8px */
$spacings: (
  'xs': 4px,
  'sm': 8px,
  'md': 16px,
  'lg': 24px,
  'xl': 32px,
  '2xl': 48px
);

:root {
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
}
```

### 5. src/styles/1-settings/\_radii.scss

Задает шкалу радиусов скругления элементов интерфейса от минимальных плашек до полностью круглых элементов.

```scss
/* ==========================================================================
   1-SETTINGS: RADII
   ========================================================================== */

$radii: (
  'none': 0,
  'sm': 2px,
  'md': 6px,
  'lg': 12px,
  'full': 9999px
);

:root {
  --radius-none: 0;
  --radius-sm: 2px;
  --radius-md: 6px;
  --radius-lg: 12px;
  --radius-full: 9999px;
}
```

### 6. src/styles/1-settings/\_shadows.scss

Управляет уровнями глубины теней (Elevation).

```scss
/* ==========================================================================
   1-SETTINGS: SHADOWS
   ========================================================================== */

:root {
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}
```

### 7. src/styles/1-settings/\_z-index.scss

Управляет фиксированной шкалой Z-index для предотвращения конфликтов наложения слоев.

```scss
/* ==========================================================================
   1-SETTINGS: Z-INDEX
   ========================================================================== */

/* Иерархическая шкала Z-index для безопасного наложения контекстов */
$z-index: (
  'deep': -999,
  'default': 1,
  'dropdown': 1000,
  'sticky': 1100,
  'modal': 1300,
  'toast': 1500
);
```

### 8. src/styles/1-settings/\_transitions.scss

Устанавливает стандартизированные длительности переходов и функции плавности анимаций интерфейса.

```scss
/* ==========================================================================
   1-SETTINGS: TRANSITIONS
   ========================================================================== */

/* Карта кубических кривых Безье для SCSS-миксинов */
$easings: (
  'standard': cubic-bezier(0.4, 0.0, 0.2, 1),
  'decelerate': cubic-bezier(0.0, 0.0, 0.2, 1),
  'accelerate': cubic-bezier(0.4, 0.0, 1, 1)
);

:root {
  /* Стандартные длительности анимаций */
  --duration-fast: 150ms;
  --duration-normal: 250ms;
  --duration-slow: 350ms;

  /* Функции сглаживания (Easings) */
  --ease-standard: cubic-bezier(0.4, 0.0, 0.2, 1);
  --ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

### 9. src/styles/1-settings/\_containers.scss

Фиксирует максимальные ширины макетов страниц и безопасные боковые отступы контентной сетки.

```scss
/* ==========================================================================
   1-SETTINGS: CONTAINERS
   ========================================================================== */

$container-widths: (
  'sm': 640px,
  'md': 768px,
  'lg': 1024px,
  'xl': 1280px,
  'full': 100%
);

:root {
  --container-max-width: 1280px;
  /* Фоллбэк 16px на случай отсутствия переменной --spacing-md */
  --container-gutter: var(--spacing-md, 16px);
}
```

### 10. src/styles/1-settings/\_opacity.scss

Определяет шкалу прозрачности для различных интерактивных состояний элементов (Hover, Focus, Disabled, Overlay).

```scss
/* ==========================================================================
   1-SETTINGS: OPACITY
   ========================================================================== */

:root {
  --opacity-disabled: 0.38;
  --opacity-hover: 0.08;
  --opacity-focus: 0.12;
  --opacity-active: 0.16;
  --opacity-overlay: 0.5;
}
```

### 11. src/styles/1-settings/\_vendor-tokens.scss

Служит для глобального переопределения дизайн-токенов сторонних библиотек компонентов через систему переменных проекта.

```scss
/* ==========================================================================
   1-SETTINGS: VENDOR TOKENS
   ========================================================================== */

:root {
  /* Переопределение переменных Angular Material */
  --mdc-outlined-text-field-container-shape: var(--radius-md, 6px);
  --mdc-theme-primary: var(--color-primary);

  /* Переопределение переменных PrimeNG */
  --p-primary-color: var(--color-primary);
  --p-content-border-radius: var(--radius-md, 6px);
}
```

### 12. src/styles/1-settings/\_index.scss

Объединяет и реэкспортирует все конфигурационные файлы слоя `1-settings` через единую директиву `@forward`.

```scss
/* ==========================================================================
   1-SETTINGS: INDEX
   ========================================================================== */

@forward 'colors';
@forward 'typography';
@forward 'spacing';
@forward 'breakpoints';
@forward 'radii';
@forward 'shadows';
@forward 'z-index';
@forward 'transitions';
@forward 'containers';
@forward 'opacity';
@forward 'vendor-tokens';
```