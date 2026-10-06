Шестой слой ITCSS — **`6-components`** — содержит законченные, переиспользуемые UI-компоненты интерфейса. Каждый компонент оформляется по методологии БЭМ с префиксом `c-` и не должен содержать внешних отступов (`margin`).

```
src/styles/6-components/
├── _button.scss        # Кнопки (.c-btn)
├── _card.scss          # Карточки (.c-card)
├── _badge.scss         # Бейджи и плашки (.c-badge)
├── _modal.scss         # Модальные окна (.c-modal)
├── _nav.scss           # Навигация и меню (.c-nav)
├── _dropdown.scss      # Выпадающие списки (.c-dropdown)
├── _form-field.scss    # Поля ввода и группы элементов форм (.c-field)
├── _avatar.scss        # Аватары пользователей (.c-avatar)
└── _index.scss         # Индексный экспорт всех компонентов
```

### 1. src/styles/6-components/\_button.scss

Определяет стили кнопок интерфейса с поддержкой различных цветовых тем, размеров и внутренних иконок.

```scss
/* ==========================================================================
   6-COMPONENTS: BUTTON
   ========================================================================== */

.c-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-xs, 8px);
  padding: var(--spacing-sm, 10px) var(--spacing-md, 16px);
  font-family: inherit;
  font-size: var(--font-size-base, 1rem);
  font-weight: var(--font-weight-medium, 500);
  line-height: 1.2;
  text-decoration: none;
  white-space: nowrap;
  border-radius: var(--radius-md, 6px);
  border: 1px solid transparent;
  cursor: pointer;
  transition: background-color var(--duration-fast, 150ms) ease,
              border-color var(--duration-fast, 150ms) ease,
              box-shadow var(--duration-fast, 150ms) ease;

  /* Элементы внутри кнопки */
  &__icon {
    width: 1.25em;
    height: 1.25em;
    flex-shrink: 0;
  }

  /* Модификаторы внешнего вида */
  &--primary {
    background-color: var(--color-primary);
    color: #ffffff;

    &:hover {
      background-color: var(--color-primary-hover);
    }
  }

  &--secondary {
    background-color: var(--color-surface-variant);
    color: var(--color-text-main);
    border-color: var(--color-border);

    &:hover {
      background-color: var(--color-border);
    }
  }

  /* Модификаторы размеров */
  &--sm {
    padding: var(--spacing-xs, 6px) var(--spacing-sm, 12px);
    font-size: var(--font-size-sm, 0.875rem);
  }

  &--lg {
    padding: var(--spacing-md, 14px) var(--spacing-lg, 24px);
    font-size: var(--font-size-lg, 1.125rem);
  }
}
```

### 2. src/styles/6-components/\_card.scss

Реализует компонент карточки контента с модульной структурой шапки, тела, подвала и поддержкой интерактивного наведения.

```scss
/* ==========================================================================
   6-COMPONENTS: CARD
   ========================================================================== */

.c-card {
  display: flex;
  flex-direction: column;
  background-color: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg, 12px);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  transition: box-shadow var(--duration-fast, 150ms) ease,
              border-color var(--duration-fast, 150ms) ease;

  &__header {
    padding: var(--spacing-md, 16px) var(--spacing-lg, 24px);
    border-bottom: 1px solid var(--color-border);
  }

  &__body {
    padding: var(--spacing-lg, 24px);
    flex-grow: 1;
  }

  &__footer {
    padding: var(--spacing-md, 16px) var(--spacing-lg, 24px);
    background-color: var(--color-surface-variant);
    border-top: 1px solid var(--color-border);
  }

  &__title {
    margin: 0;
    font-size: var(--font-size-xl, 1.25rem);
    color: var(--color-text-heading);
  }

  /* Модификатор: интерактивная карточка с эффектом при наведении */
  &--interactive {
    &:hover {
      box-shadow: var(--shadow-md);
      border-color: var(--color-primary);
    }
  }
}
```

### 3. src/styles/6-components/\_index.scss

Экспортирует все файлы компонентов слоя `6-components` для подключения в глобальную сборку стилей.

```scss
/* ==========================================================================
   6-COMPONENTS: INDEX
   ========================================================================== */

@use 'button';
@use 'card';
@use 'badge';
@use 'modal';
@use 'nav';
@use 'dropdown';
@use 'form-field';
@use 'avatar';
```

### Использование в HTML

В разметке объекты слоя `5-objects` (каркас) и компоненты слоя `6-components` (дизайн) комбинируются без конфликтов:

```html
<!-- o-container и o-grid создают каркас, а c-card и c-btn задают дизайн -->
<div class="o-container">
  <div class="o-grid o-grid--3-cols">
    
    <article class="c-card c-card--interactive">
      <div class="c-card__header">
        <h3 class="c-card__title">Базовый тариф</h3>
      </div>
      
      <div class="c-card__body">
        <p>Полный доступ к основным функциям системы.</p>
      </div>
      
      <div class="c-card__footer">
        <button class="c-btn c-btn--primary c-btn--lg">
          <span class="c-btn__text">Выбрать</span>
        </button>
      </div>
    </article>

  </div>
</div>
```