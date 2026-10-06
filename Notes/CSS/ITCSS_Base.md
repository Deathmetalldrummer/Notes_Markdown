

### 7 слоев классического ITCSS

По мере движения сверху вниз по слоям увеличивается специфичность селекторов и уменьшается область их применения:

1. **Settings:** Глобальные переменные, конфигурация (цветовая палитра, размеры шрифтов, брекпоинты). Не генерирует чистый CSS-код при компиляции.
2. **Tools:** Глобальные SCSS-миксины и функции. Не генерирует чистый CSS-код.
3. **Generic:** Сбросы стилей, сброс браузерных дефолтов (`normalize.css`, `box-sizing: border-box`). Первая секция, генерирующая реальный CSS.
4. **Elements:** Стили для базвых HTML-тегов без использования классов (`h1`, `a`, `table`, `input`).
5. **Objects:** Классы макетов и каркасов, не имеющие оформления (сетка, `.container`, `.media-object`).
6. **Components:** Конкретные UI-элементы с полноценным оформлением (`.btn`, `.card`, `.nav-bar`).
7. **Trumps / Utilities:** Классы с принудительной высокой специфичностью (часто с `!important`) для точечных правок (`.u-text-center`, `.u-hidden`).

#### Базовая структура папок в Angular-проекте

```
src/
├── styles/
│   ├── 1-settings/                  # Настройки и токены
│   │   ├── _colors.scss
│   │   └── _breakpoints.scss
│   ├── 2-tools/                     # SCSS-миксины и функции
│   │   ├── _mixins.scss
│   │   └── _functions.scss
│   ├── 3-generic/                   # Сброс дефолтов
│   │   └── _reset.scss
│   ├── 4-elements/                  # Базовые теги
│   │   ├── _typography.scss
│   │   └── _page.scss
│   ├── 5-objects/                   # Глобальные каркасы
│   │   ├── _layout.scss
│   │   └── _grid.scss
│   ├── 6-components/               # Глобальные / Сторонние компоненты / переопределения
│   │   └── _ng-material-override.scss
│   ├── 7-utilities/                # Утилиты
│   │   └── _helpers.scss
│   └── styles.scss                  # Главная точка входа
└── app/
    └── features/
        └── user-card/
            ├── user-card.component.ts
            └── user-card.component.scss  # Локальный слой Components!
```



#### Импорт стилей в Angular

Для импорта настроек (`Settings`) и инструментов (`Tools`) в изолированные компоненты настройте `stylePreprocessorOptions` в `angular.json`:

```JSON
"stylePreprocessorOptions": {
  "includePaths": [
    "src/styles"
  ]
}
```

Теперь в SCSS любого компонента можно легко импортировать нужные файлы:

```SCSS
// app/features/user-card/user-card.component.scss
@use '1-settings/colors' as *;
@use '2-tools/mixins' as *;

:host {
  display: block;
  background-color: var(--color-surface);
  border-radius: 8px;
  padding: 16px;

  @include respond-to('desktop') {
    padding: 24px;
  }
}
```


## Сброс стилей
3-generic/_reset.scss

1. **Компоненты форм:** HTML-теги `<button>` и `<input>` по умолчанию не наследуют шрифт от `<body>`. Без сброса ваш компонент ввода текста будет выглядеть чужеродно на фоне остального интерфейса.
2. **Изоляция стилей (ViewEncapsulation):** Локальные стили компонентов не должны отвлекаться на «борьбу» с дефолтными браузерными `margin`. Сбросив их на уровне слоя `Generic`, вы гарантируете, что компонент `<app-card>` будет вести себя одинаково в любом окружении.

```CSS
/* ==========================================================================
   MODERN CSS RESET
   ========================================================================== */

/* 1. Включаем box-sizing: border-box для всех элементов и их псевдоэлементов.
      Это упрощает расчет размеров и исключает вылезание padding за границы. */
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* 2. Обнуляем дефолтные внешние отступы (margin) у всех основных элементов. */
* {
  margin: 0;
}

/* 3. Гарантируем корректное поведение корневых элементов и отклик на скролл. */
html,
body {
  height: 100%;
}

/* 4. Настраиваем бановую работу body:
      - line-height: 1.5 улучшает читаемость текста;
      - -webkit-font-smoothing включит качественное сглаживание шрифтов на macOS/iOS;
      - text-rendering сглаживает лигатуры для сложной типографики. */
body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeSpeed;
}

/* 5. Элементы медиа (картинки, видео, canvas, svg) делают адаптивными по умолчанию:
      - max-width: 100% не дает вылезать за границы родителя;
      - display: block убирает ненужный нижний зазор от подстрочных символов (inline gaps). */
img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

/* 6. Элементы форм (button, input, select, textarea) по умолчанию НЕ наследуют 
      стили шрифта от body в большинстве браузеров. Это явное исправление: */
input,
button,
textarea,
select {
  font: inherit;
  color: inherit;
}

/* 7. Убираем дефолтные границы у текстовых полей и кнопок */
button,
input,
textarea {
  border: none;
  background: none;
}

/* 8. Делаем кликабельные элементы явно выраженными */
button,
select,
a {
  cursor: pointer;
}

/* 9. Отключаем изменение размера текстового поля textarea по горизонтали, 
      чтобы пользователь не ломал сетку верстки. */
textarea {
  resize: vertical;
}

/* 10. Убираем оформление маркеров для списков, имеющих атрибут class 
       (сохраняет маркеры для стандартного семантического текста). */
ul[class],
ol[class] {
  list-style: none;
  padding: 0;
}

/* 11. Предотвращаем переполнение текста внутри флекс- и грид-контейнеров */
p, h1, h2, h3, h4, h5, h6 {
  overflow-wrap: break-word;
}

/* 12. Создаем контейнер для Angular изолированного приложения (root-компонента),
       чтобы он растягивался на всю высоту экрана при необходимости. */
#root,
app-root {
  isolation: isolate;
  min-height: 100%;
  display: flex;
  flex-direction: column;
}

/* 13. Отключаем анимации для пользователей с включенным режимом "Reduced Motion" 
       в операционной системе (улучшение доступности / Accessibility). */
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