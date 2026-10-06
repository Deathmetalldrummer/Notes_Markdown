Слой **`2-tools`** содержит инструментарий SCSS — **функции и миксины**. Как и слой `1-settings`, он не генерирует чистый CSS при компиляции сам по себе, а используется в последующих слоях ITCSS и внутри стилей компонентов.

```
src/styles/2-tools/
├── _responsive.scss      # Миксины медиазапросов respond-to()
├── _z-index.scss         # Функция безопасного получения z()
├── _typography.scss      # Миксины обрезки текста (truncate)
├── _flex.scss            # Хелперы для выравнивания Flexbox
├── _converters.scss      # Функции rem() и fluid-size()
├── _accessibility.scss   # Миксины доступности sr-only и focus-ring()
├── _angular-helpers.scss # Миксины для селекторов :host в Angular
├── _grid.scss            # Хелперы адаптивных сеток CSS Grid
└── _index.scss           # Экспорт всех инструментов слоя
```

### 1. src/styles/2-tools/\_responsive.scss

Предоставляет миксины для создания адаптивных медиазапросов на основе шкалы точек останова из слоя `1-settings`.

```scss
/* ==========================================================================
   2-TOOLS: RESPONSIVE
   ========================================================================== */

@use '1-settings/breakpoints' as settings;

/// Миксин для мобильного подхода (Mobile-first min-width)
/// @param {String} $breakpoint - Имя точки останова из карты $breakpoints
@mixin respond-to($breakpoint) {
  $raw-value: map-get(settings.$breakpoints, $breakpoint);

  @if $raw-value {
    @media (min-width: $raw-value) {
      @content;
    }
  } @else {
    @warn "Неизвестный breakpoint: '#{$breakpoint}'. Доступные значения: #{map-keys(settings.$breakpoints)}";
  }
}

/// Миксин для интервалов между двумя точками останова
/// @param {String} $min-bp - Нижняя граница диапазона
/// @param {String} $max-bp - Верхняя граница диапазона (вычитается 1px для исключения наложения)
@mixin respond-between($min-bp, $max-bp) {
  $min-value: map-get(settings.$breakpoints, $min-bp);
  $max-value: map-get(settings.$breakpoints, $max-bp);

  @if $min-value and $max-value {
    @media (min-width: $min-value) and (max-width: ($max-value - 1px)) {
      @content;
    }
  }
}
```

### 2. src/styles/2-tools/\_z-index.scss

Реализует функцию безопасного извлечения значений Z-index из карты настроек для защиты от случайных произвольных слоев.

```scss
/* ==========================================================================
   2-TOOLS: Z-INDEX
   ========================================================================== */

@use '1-settings/shadows' as settings;

/// Извлекает числовое значение z-index из карты $z-index
/// @param {String} $layer - Название слоя ('dropdown', 'modal', 'sticky' и т.д.)
/// @return {Number} Значение z-index
@function z($layer) {
  $z-value: map-get(settings.$z-index, $layer);

  @if $z-value {
    @return $z-value;
  } @else {
    @error "Слой z-index '#{$layer}' не найден в карте $z-index!";
  }
}
```

### 3. src/styles/2-tools/\_typography.scss

Содержит вспомогательные миксины для обрезки текста с многоточием в одну или несколько строк и быстрой стилизации шрифтов.

```scss
/* ==========================================================================
   2-TOOLS: TYPOGRAPHY
   ========================================================================== */

/// Обрезка однострочного текста с многоточием
@mixin truncate-single-line {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/// Многострочная обрезка текста (Line Clamp через WebKit-бокс)
/// @param {Number} $lines - Максимальное количество отображаемых строк
@mixin truncate-multi-line($lines: 2) {
  display: -webkit-box;
  -webkit-line-clamp: $lines;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/// Быстрая установка базовых свойств шрифта при наличии значений
@mixin font-style($size: null, $weight: null, $line-height: null) {
  @if $size { font-size: $size; }
  @if $weight { font-weight: $weight; }
  @if $line-height { line-height: $line-height; }
}
```

### 4. src/styles/2-tools/\_flex.scss

Определяет миксины-хелперы для быстрого центрирования и распределения элементов внутри Flexbox-контейнеров.

```scss
/* ==========================================================================
   2-TOOLS: FLEX
   ========================================================================== */

/// Быстрое выравнивание элементов по центру Flexbox
@mixin flex-center($direction: row) {
  display: flex;
  flex-direction: $direction;
  align-items: center;
  justify-content: center;
}

/// Распределение элементов по краям контейнера (space-between)
@mixin flex-between($align: center) {
  display: flex;
  align-items: $align;
  justify-content: space-between;
}
```

### 5. src/styles/2-tools/\_converters.scss

Предоставляет математические функции перевода пикселей в относительные единицы `rem` и генерации плавных адаптивных размеров через `clamp()`.

```scss
/* ==========================================================================
   2-TOOLS: CONVERTERS
   ========================================================================== */

@use 'sass:math';

/// Математический перевод px в rem (на основе базы 16px)
/// @param {Number} $px-value - Значение в пикселях с единицей измерения или без
/// @return {Number} Рассчитанное значение в rem
@function rem($px-value) {
  @if math.is-unitless($px-value) {
    @return math.div($px-value, 16) * 1rem;
  }
  @return math.div($px-value, 16px) * 1rem;
}

/// Генератор отзывчивого размера через CSS-функцию clamp()
/// @param {Number} $min - Минимальный размер (px)
/// @param {Number} $max - Максимальный размер (px)
/// @param {Number} $min-viewport - Нижняя ширина экрана (px) [320px]
/// @param {Number} $max-viewport - Верхняя ширина экрана (px) [1280px]
@function fluid-size($min, $max, $min-viewport: 320, $max-viewport: 1280) {
  $slope: math.div($max - $min, $max-viewport - $min-viewport);
  $y-axis-intersection: -$min-viewport * $slope + $min;

  @return clamp(
    #{rem($min)},
    #{rem($y-axis-intersection)} + #{$slope * 100vw},
    #{rem($max)}
  );
}
```

### 6. src/styles/2-tools/\_accessibility.scss

Содержит миксины доступности для скрытия вспомогательного контента от зрячих пользователей и унификации фокусных рамок.

```scss
/* ==========================================================================
   2-TOOLS: ACCESSIBILITY
   ========================================================================== */

/// Визуально скрывает элемент, сохраняя его доступным для Screen Readers
@mixin sr-only {
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

/// Стилизация индикатора фокуса при навигации с клавиатуры (:focus-visible)
@mixin focus-ring($color: var(--color-primary), $offset: 2px) {
  &:focus-visible {
    outline: 2px solid $color;
    outline-offset: $offset;
  }
}
```

### 7. src/styles/2-tools/\_angular-helpers.scss

Содержит миксины для работы с селекторами `:host` в контексте изолированных стилей компонентов Angular.

```scss
/* ==========================================================================
   2-TOOLS: ANGULAR HELPERS
   ========================================================================== */

/// Стилизация состояния корневого элемента Angular-компонента через :host
/// @param {String} $state - CSS-класс или селектор состояния
@mixin host-state($state) {
  :host(#{$state}),
  :host.#{$state} {
    @content;
  }
}

/// Установка блочной модели отображения по умолчанию для хост-элемента
@mixin host-block {
  :host {
    display: block;
  }
}
```

### 8. src/styles/2-tools/\_grid.scss

Определяет миксин для быстрого создания адаптивных сеток CSS Grid с автозаполнением колонок.

```scss
/* ==========================================================================
   2-TOOLS: GRID
   ========================================================================== */

/// Создает адаптивную сетку с автозаполнением (auto-fit) без медиазапросов
/// @param {Number} $min-col-width - Минимальная допустимая ширина колонки
/// @param {Number} $gap - Интервал между колонками и рядами сетки
@mixin grid-auto-fit($min-col-width: 250px, $gap: var(--spacing-md, 16px)) {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax($min-col-width, 1fr));
  gap: $gap;
}
```

### 9. src/styles/2-tools/\_index.scss

Объединяет все инструменты, миксины и функции слоя `2-tools` для централизованного экспорта через `@forward`.

```scss
/* ==========================================================================
   2-TOOLS: INDEX
   ========================================================================== */

@forward 'converters';
@forward 'responsive';
@forward 'z-index';
@forward 'accessibility';
@forward 'typography';
@forward 'flex';
@forward 'grid';
@forward 'angular-helpers';
```