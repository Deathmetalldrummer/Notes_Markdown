
```
src/
├── styles/
│   ├── 1-settings/                  # Настройки и токены
|   |	├── _colors.scss               # Цветовая палитра и темы
|   |	├── _typography.scss           # Шрифты, размеры, веса
|   |	├── _spacing.scss              # Шкала отступов
|   |	├── _breakpoints.scss          # Точки останова медиазапросов
|   |	├── _radii.scss                # Радиусы скругления
|   |	├── _shadows.scss              # Тени
|   |	├── _z-index.scss              # Z-index
|   |	├── _transitions.scss          # Длительности и тайминги анимаций
|   |	├── _containers.scss           # Ширина макетов и сетка
|   |	├── _opacity.scss              # Шкала прозрачности и состояний
|   |	├── _vendor-tokens.scss        # Токены сторонних UI-библиотек
|   |	└── _index.scss                # Общий импорт всех файлов
|   |
│   ├── 2-tools/                     # SCSS-миксины и функции
|   |	├── _converters.scss           # Функции rem() и fluid-size() 
|   |	├── _responsive.scss           # Миксины @include respond-to('desktop') 
|   |	├── _z-index.scss              # Функция z('modal') 
|   |	├── _accessibility.scss        # Миксины @include sr-only и focus-ring() 
|   |	├── _typography.scss           # Обрезка текста (truncate) 
|   |	├── _flex.scss                 # Хелперы для Flexbox 
|   |	├── _grid.scss                 # Авто-сетки CSS Grid 
|   |	├── _angular-helpers.scss      # Миксины для :host и пробрасывания стилей 
|   |	└── _index.scss                # Экспорт всех файлов через @forward
|   |
│   ├── 3-generic/                   # Сброс дефолтов
|   |	├── _box-sizing.scss           # Алгоритм расчета border-box
|   |	├── _reset.scss                # Modern CSS Reset
|   |	├── _normalize.scss            # Коррекция браузерных багов
|   |	├── _scroll.scss               # Настройка скроллбара
|   |	├── _mobile-fixes.scss         # Фиксы iOS / Android
|   |	├── _print.scss                # Базовые правила печати
|   |	├── _a11y-contrast.scss        # Поддержка Forced Colors Mode
|   |	└── _index.scss                # Общий импорт слоя через @use
|   |
│   ├── 4-elements/                  # Базовые теги
|   |	├── _base.scss                 # html, body, a, hr, ::selection
|   |	├── _typography.scss           # h1-h6, p, blockquote, code, pre
|   |	├── _lists.scss                # ul, ol без классов
|   |	├── _tables.scss               # table, th, td, caption
|   |	├── _forms.scss                # input, button, textarea, select, label
|   |	├── _media.scss                # figure, figcaption, svg
|   |	├── _dialogs.scss              # dialog, ::backdrop
|   |	├── _interactive.scss          # details, summary
|   |	├── _feedback.scss             # progress, meter
|   |	├── _text-formatting.scss      # mark, ins, del, sub, sup, time
|   |	└── _index.scss                # Полный экспорт слоя
|   |
│   ├── 5-objects/                   # Глобальные каркасы
│   │   ├── _layout.scss               # Макеты
|   |	├── _container.scss            # Центратор контента
|   |	├── _stack.scss                # Вертикальные отступы между элементами
|   |	├── _grid.scss                 # CSS Grid сетки
|   |	├── _media.scss                # Медиа-объект (картинка + контент)
|   |	├── _crop.scss                 # Пропорции медиа (Aspect Ratio)
|   |	├── _cluster.scss              # Горизонтальный перенос (теги, группы кнопок)
|   |	├── _bar.scss                  # Панели (Left / Right разнос)
|   |	├── _table-wrapper.scss        # Адаптивный скролл таблиц
|   |	├── _scroll-box.scss           # Изолированный скролл-контейнер
|   |	├── _overlay.scss              # Фиксированные слои / Каркас модалок
|   |	└── _index.scss                # Полный экспорт слоя
|   |
│   ├── 6-components/               # Сторонние компоненты / Переопределения
|   |   ├── _prime-ng-override.scss
│   │   └── _ng-material-override.scss
|   |
│   ├── 7-utilities/                # Утилиты
│   │   ├── _helpers.scss
|   |	├── _display.scss             # Показ и скрытие (u-hidden, u-block)
|   |	├── _spacing.scss             # Внешние и внутренние отступы (u-mb-lg, u-p-0)
|   |	├── _text.scss                # Выравнивание и свойства шрифта (u-text-center, u-truncate)
|   |	├── _visibility.scss          # Скрытие контента для доступности (u-sr-only)
|   |	├── _position.scss            # Типы позиционирования и z-index (u-pos-relative, u-inset-0)
|   |	├── _sizing.scss              # Размеры и object-fit (u-w-100, u-fit-cover)
|   |	├── _interactivity.scss       # Поведение мыши и выделения (u-pointer-events-none)
|   |	├── _overflow.scss            # Управление скроллом и переполнением (u-overflow-hidden)
|   |	├── _effects.scss             # Прозрачность и сброс теней (u-opacity-0, u-shadow-none)
|   |	└── _index.scss               # Главный файл экспорта слоя
│   └── styles.scss                  # Главная точка входа
└── app/
    └── features/
        └── user-card/
            ├── user-card.component.ts
            └── user-card.component.scss  # Локальный слой Components!
```

## Bash
Сохранить в файл `create-itcss.sh`, сделать исполняемым (`chmod +x create-itcss.sh`) и запустить в нужной директории:
```bash
#!/bin/bash

TARGET_DIR="./itcss"
DIR_1="1-settings"
DIR_2="2-tools"
DIR_3="3-generic"
DIR_4="4-elements"
DIR_5="5-objects"
DIR_6="6-components"
DIR_7="7-utilities"

echo "Создание структуры ITCSS в $TARGET_DIR..."

# Создание папок
mkdir -p "$TARGET_DIR/$DIR_1"
mkdir -p "$TARGET_DIR/$DIR_2"
mkdir -p "$TARGET_DIR/$DIR_3"
mkdir -p "$TARGET_DIR/$DIR_4"
mkdir -p "$TARGET_DIR/$DIR_5"
mkdir -p "$TARGET_DIR/$DIR_6"
mkdir -p "$TARGET_DIR/$DIR_7"

# 1-settings (Настройки, переменные)
touch "$TARGET_DIR/$DIR_1/_colors.scss"
touch "$TARGET_DIR/$DIR_1/_typography.scss"
touch "$TARGET_DIR/$DIR_1/_spacing.scss"
touch "$TARGET_DIR/$DIR_1/_breakpoints.scss"
touch "$TARGET_DIR/$DIR_1/_radii.scss"
touch "$TARGET_DIR/$DIR_1/_shadows.scss"
touch "$TARGET_DIR/$DIR_1/_z-index.scss"
touch "$TARGET_DIR/$DIR_1/_transitions.scss"
touch "$TARGET_DIR/$DIR_1/_containers.scss"
touch "$TARGET_DIR/$DIR_1/_opacity.scss"
touch "$TARGET_DIR/$DIR_1/_vendor-tokens.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_1/index.scss"
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
EOF

# 2-tools (Функции и миксины)
touch "$TARGET_DIR/$DIR_2/_converters.scss"
touch "$TARGET_DIR/$DIR_2/_responsive.scss"
touch "$TARGET_DIR/$DIR_2/_z-index.scss"
touch "$TARGET_DIR/$DIR_2/_accessibility.scss"
touch "$TARGET_DIR/$DIR_2/_typography.scss"
touch "$TARGET_DIR/$DIR_2/_flex.scss"
touch "$TARGET_DIR/$DIR_2/_grid.scss"
touch "$TARGET_DIR/$DIR_2/_angular-helpers.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_2/index.scss"
@forward 'converters';
@forward 'responsive';
@forward 'z-index';
@forward 'accessibility';
@forward 'typography';
@forward 'flex';
@forward 'grid';
@forward 'angular-helpers';
EOF
# 3-generic (Сброс и базовые настройки)
touch "$TARGET_DIR/$DIR_3/_box-sizing.scss"
touch "$TARGET_DIR/$DIR_3/_reset.scss"
touch "$TARGET_DIR/$DIR_3/_normalize.scss"
touch "$TARGET_DIR/$DIR_3/_scroll.scss"
touch "$TARGET_DIR/$DIR_3/_mobile-fixes.scss"
touch "$TARGET_DIR/$DIR_3/_print.scss"
touch "$TARGET_DIR/$DIR_3/_a11y-contrast.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_3/index.scss"
@use 'box-sizing';
@use 'reset';
@use 'normalize';
@use 'scroll';
@use 'mobile-fixes';
@use 'print';
@use 'a11y-contrast';
EOF

# 4-elements (Базовые селекторы тегов)
touch "$TARGET_DIR/$DIR_4/_base.scss"
touch "$TARGET_DIR/$DIR_4/_typography.scss"
touch "$TARGET_DIR/$DIR_4/_lists.scss"
touch "$TARGET_DIR/$DIR_4/_tables.scss"
touch "$TARGET_DIR/$DIR_4/_forms.scss"
touch "$TARGET_DIR/$DIR_4/_media.scss"
touch "$TARGET_DIR/$DIR_4/_dialogs.scss"
touch "$TARGET_DIR/$DIR_4/_interactive.scss"
touch "$TARGET_DIR/$DIR_4/_feedback.scss"
touch "$TARGET_DIR/$DIR_4/_text-formatting.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_4/index.scss"
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
EOF

# 5-objects (Сетки, макеты без оформления)
touch "$TARGET_DIR/$DIR_5/_container.scss"
touch "$TARGET_DIR/$DIR_5/_stack.scss"
touch "$TARGET_DIR/$DIR_5/_grid.scss"
touch "$TARGET_DIR/$DIR_5/_cluster.scss"
touch "$TARGET_DIR/$DIR_5/_bar.scss"
touch "$TARGET_DIR/$DIR_5/_media.scss"
touch "$TARGET_DIR/$DIR_5/_crop.scss"
touch "$TARGET_DIR/$DIR_5/_table-wrapper.scss"
touch "$TARGET_DIR/$DIR_5/_scroll-box.scss"
touch "$TARGET_DIR/$DIR_5/_overlay.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_5/index.scss"
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
EOF

# 6-components (Только глобальные UI-компоненты вне Angular-модулей)
touch "$TARGET_DIR/$DIR_6/_override.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_6/index.scss"
@use '_override';
EOF

# 7-trumps (Утилиты, переопределения)
touch "$TARGET_DIR/$DIR_7/_display.scss"
touch "$TARGET_DIR/$DIR_7/_spacing.scss"
touch "$TARGET_DIR/$DIR_7/_text.scss"
touch "$TARGET_DIR/$DIR_7/_visibility.scss"
touch "$TARGET_DIR/$DIR_7/_position.scss"
touch "$TARGET_DIR/$DIR_7/_sizing.scss"
touch "$TARGET_DIR/$DIR_7/_interactivity.scss"
touch "$TARGET_DIR/$DIR_7/_overflow.scss"
touch "$TARGET_DIR/$DIR_7/_effects.scss"
cat << 'EOF' > "$TARGET_DIR/$DIR_7/index.scss"
@use 'display';
@use 'spacing';
@use 'text';
@use 'visibility';
@use 'position';
@use 'sizing';
@use 'interactivity';
@use 'overflow';
@use 'effects';
EOF

# Главный входной файл
cat << 'EOF' > "$TARGET_DIR/index.scss"
/* ==========================================================================
   MAIN ITCSS BUILDER
   ========================================================================== */

// 1. Settings (Переменные, CSS Custom Properties, дизайн-токены)
@use '1-settings';

// 2. Tools (Миксины и функции SCSS)
@use '2-tools';

// 3. Generic (Reset, Normalize, Box-Sizing)
@use '3-generic';

// 4. Elements (Базовые стили для чистых HTML-тегов: h1, p, a, table)
@use '4-elements';

// 5. Objects (Каркасы, сетки, макеты layouts: o-grid, o-container, o-layout)
@use '5-objects';

// 6. Components (Визуальные UI-компоненты: c-btn, c-card, c-modal)
@use '6-components';

// 7. Utilities (Точечные переопределения и утилиты с !important: u-hidden, u-mb-0)
@use '7-utilities';
EOF

echo "Структура ITCSS готова!"
```