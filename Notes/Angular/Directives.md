Получение елемента на котором была применена директива:

[Angular Directive Host element, component, template и пример декоратора Optional](https://www.youtube.com/watch?v=iGthngTcZ8Q&list=PL4rYLeYunVf1fekZBd9Ypwl9pWxZkGT6x&index=2)





Renderer2 - Плохо - Почему?



### 2 типа директив:

**Атрибутивные директивы** - изменяют внешний вид или поведение существующего элемента. В шаблонах они выглядят как обычные атрибуты HTML, отсюда и название. Например ***ngModel***, ***ngClass*** 

**Структурные директивы** -  изменяют структуру DOM с помощью добавления или удаления html-элементов. Например ***ngIf***, ***ngFor***, ***ngSwitch***

##### Символ звездочки - синтаксический сахар:

```html
<div *ngIf="showFirstBlock">
    First Block
</div>
<template [ngIf]="showFirstBlock">
    <div>
        First Block
    </div>
</template>
```