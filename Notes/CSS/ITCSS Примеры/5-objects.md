Пятый слой ITCSS — **`5-objects`** — отвечает исключительно за **раскладку, геометрический каркас и пространственную структуру сайта** (Layout & Structure).

Все классы этого слоя начинаются с префикса `o-` и не содержат визуального оформления (цвета, тени, границы), описывая только позиционирование и сетку.

```
src/styles/5-objects/
├── _container.scss      # Центратор контента
├── _stack.scss          # Вертикальные отступы между элементами
├── _grid.scss           # CSS Grid сетки
├── _media.scss          # Медиа-объект (картинка + контент)
├── _crop.scss           # Пропорции медиа (Aspect Ratio)
├── _cluster.scss        # Горизонтальный перенос (теги, группы кнопок)
├── _bar.scss            # Панели (Left / Right разнос)
├── _table-wrapper.scss  # Адаптивный скролл таблиц
├── _scroll-box.scss     # Изолированный скролл-контейнер
├── _overlay.scss        # Фиксированные слои / Каркас модалок
└── _index.scss          # Полный экспорт слоя
```

### 1. src/styles/5-objects/\_container.scss

Ограничивает максимальную ширину страницы и центрирует контент по горизонтали.

```scss
/* ==========================================================================
   5-OBJECTS: CONTAINER
   ========================================================================== */

.o-container {
  width: 100%;
  max-width: var(--container-max-width, 1280px);
  margin-right: auto;
  margin-left: auto;
  padding-right: var(--container-padding, 16px);
  padding-left: var(--container-padding, 16px);

  /* Модификаторы ширины */
  &--fluid {
    max-width: 100%;
  }

  &--narrow {
    max-width: var(--container-narrow-width, 800px);
  }
}
```

### 2. src/styles/5-objects/\_stack.scss

Управляет вертикальным ритмом и отступами между соседними элементами без использования `margin-bottom` на компонентах.

```scss
/* ==========================================================================
   5-OBJECTS: STACK (FLOW)
   ========================================================================== */

.o-stack {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;

  /* Селектор смежного соседа (Lobotomized Owl): отступ задается строго между элементами */
  > * + * {
    margin-top: var(--stack-gap, var(--spacing-md, 16px));
  }

  /* Модификаторы шага отступа */
  &--sm { --stack-gap: var(--spacing-sm, 8px); }
  &--lg { --stack-gap: var(--spacing-lg, 24px); }
  &--xl { --stack-gap: var(--spacing-xl, 32px); }
}
```

### 3. src/styles/5-objects/\_grid.scss

Определяет универсальную сетку на основе CSS Grid с поддержкой фиксированных колонок и автозаполнения.

```scss
/* ==========================================================================
   5-OBJECTS: GRID
   ========================================================================== */

.o-grid {
  display: grid;
  gap: var(--grid-gap, var(--spacing-md, 16px));
  grid-template-columns: repeat(12, 1fr);

  /* Автоматическая адаптивная сетка без медиазапросов */
  &--auto-fit {
    grid-template-columns: repeat(
      auto-fit,
      minmax(var(--grid-min-col-width, 280px), 1fr)
    );
  }

  /* Модификаторы количества колонок */
  &--2-cols { grid-template-columns: repeat(2, 1fr); }
  &--3-cols { grid-template-columns: repeat(3, 1fr); }
  &--4-cols { grid-template-columns: repeat(4, 1fr); }
}
```

### 4. src/styles/5-objects/\_media.scss

Реализует классический паттерн «Медиа-объект» для размещения фиксированного графического элемента рядом с гибким контентом.

```scss
/* ==========================================================================
   5-OBJECTS: MEDIA
   ========================================================================== */

.o-media {
  display: flex;
  align-items: flex-start;
  gap: var(--media-gap, var(--spacing-md, 16px));

  &__img {
    flex-shrink: 0;
  }

  &__body {
    flex-grow: 1;
  }

  /* Модификатор центрирования по вертикали */
  &--center {
    align-items: center;
  }
}
```

### 5. src/styles/5-objects/\_crop.scss

Фиксирует пропорции медиаконтента (Aspect Ratio) и защищает изображения и видео от искажений пропорций.

```scss
/* ==========================================================================
   5-OBJECTS: CROP
   ========================================================================== */

.o-crop {
  position: relative;
  display: block;
  overflow: hidden;
  aspect-ratio: var(--crop-ratio, 16 / 9);

  > img,
  > video,
  > iframe {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  /* Модификаторы пропорций */
  &--1x1 { --crop-ratio: 1 / 1; }
  &--4x3 { --crop-ratio: 4 / 3; }
}
```

### 6. src/styles/5-objects/\_cluster.scss

Формирует гибкую горизонтальную строку с автоматическим переносом элементов и равными промежутками между ними.

```scss
/* ==========================================================================
   5-OBJECTS: CLUSTER
   ========================================================================== */

.o-cluster {
  display: flex;
  flex-wrap: wrap;
  align-items: var(--cluster-align, center);
  justify-content: var(--cluster-justify, flex-start);
  gap: var(--cluster-gap, var(--spacing-sm, 8px));
}
```

### 7. src/styles/5-objects/\_bar.scss

Разносит элементы по противоположным краям строки с вертикальным центрированием для панелей навигации и шапок карточек.

```scss
/* ==========================================================================
   5-OBJECTS: BAR
   ========================================================================== */

.o-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--bar-gap, var(--spacing-md, 16px));

  /* Допускает перенос элементов при нехватке ширины */
  &--wrap {
    flex-wrap: wrap;
  }
}
```

### 8. src/styles/5-objects/\_table-wrapper.scss

Обеспечивает безопасный горизонтальный скролл широких таблиц данных на мобильных экранах без ломки сетки страницы.

```scss
/* ==========================================================================
   5-OBJECTS: TABLE WRAPPER
   ========================================================================== */

.o-table-wrapper {
  width: 100%;
  overflow-x: auto;
  /* Плавная инерционная прокрутка на устройствах iOS */
  -webkit-overflow-scrolling: touch;

  > table {
    width: 100%;
    /* Предотвращает нежелательное сплющивание ячеек */
    white-space: nowrap;
  }
}
```

### 9. src/styles/5-objects/\_scroll-box.scss

Создает изолированную область прокрутки и предотвращает скроллинг родительской страницы при достижении границ контейнера.

```scss
/* ==========================================================================
   5-OBJECTS: SCROLL BOX
   ========================================================================== */

.o-scroll-box {
  max-height: var(--scroll-box-max-height, 100%);
  overflow-y: auto;
  /* Изолирует цепочку прокрутки от основного документа */
  overscroll-behavior-y: contain;

  &--horizontal {
    display: flex;
    overflow-x: auto;
    overflow-y: hidden;
    overscroll-behavior-x: contain;
  }
}
```

### 10. src/styles/5-objects/\_overlay.scss

Задает каркас позиционирования для поверхностных элементов интерфейса (бэкдропы, модальные окна, плавающие панели).

```scss
/* ==========================================================================
   5-OBJECTS: OVERLAY
   ========================================================================== */

.o-overlay {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: var(--z-index-overlay, 100);
  display: flex;
  align-items: center;
  justify-content: center;

  &--sticky {
    position: sticky;
    top: 0;
  }
}
```

### 11. src/styles/5-objects/\_index.scss

Объединяет все структурные объекты слоя `5-objects` для общего экспорта через директиву `@use`.

```scss
/* ==========================================================================
   5-OBJECTS: INDEX
   ========================================================================== */

@use 'container';
@use 'stack';
@use 'grid';
@use 'cluster';
@use 'bar';
@use 'media';
@use 'crop';
@use 'table-wrapper';
@use 'scroll-box';
@use 'overlay';
```

### Использование в HTML

Объекты создают каркас страницы, объединяясь с компонентами из последующих слоев:

```html
<!-- o-container и o-stack создают каркас, а компоненты наполняют контентом -->
<div class="o-container">
  <div class="o-stack o-stack--lg">
    
    <!-- Шапка страницы -->
    <header class="o-media o-media--center">
      <div class="o-media__img">
        <app-avatar></app-avatar>
      </div>
      <div class="o-media__body">
        <h1>Профиль пользователя</h1>
      </div>
    </header>

    <!-- Сетка с карточками -->
    <div class="o-grid o-grid--auto-fit">
      <app-card></app-card>
      <app-card></app-card>
      <app-card></app-card>
    </div>

  </div>
</div>
```

### Различие слоев 5-objects, 6-components и 7-utilities

| Слой | Назначение | Пример класса | Изменяет внешний вид? |
| --- | --- | --- | --- |
| **`5-objects`** | Структура и макет | `.o-grid`, `.o-container` | ❌ Нет (только геометрия) |
| **`6-components`** | Конкретный UI-элемент | `.c-button`, `.c-card` | ✅ Да (цвета, тени, шрифт) |
| **`7-utilities`** | Точечные переопределения | `.u-text-center`, `.u-hidden` | ⚡ Переопределяет стили (`!important`) |
