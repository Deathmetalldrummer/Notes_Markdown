В Angular есть три типа директив:

* **Компоненты**: компонент по сути также является директивой, а декоратор **@Component** расширяет возможности декоратора **@Directive** с помощью добавления функционала по работе с шаблонами.
* **Атрибутивные**: они изменяют поведение уже существующего элемента, к которому они применяются. Например, **ngModel**, **ngStyle**, **ngClass**
* **Структурные**: они изменяют структуру DOM с помощью добавления, изменения или удаления элементов hmtl. Например, это директивы **ngFor** и **ngIf**


### ngClass
Директива **ngClass** позволяет определить набор классов, которые будут применяться к элементу
```html
<div [ngClass]="{firstClass:true}">
	<p [ngClass]="{firstClass:false, secondClass:true}"></p>
</div>
```
**[ngClass] принимает js-объект**, в котором ключи - это названия классов. Этим названиям присваиваются булевые значения **true** (если класс применяется) и **false** (если класс не применяется).

В блоке **div** есть параграф, по умолчанию он унаследует стили от родительского блока div.Допустим, к этому параграфу нужно применить другой класс, поэтому для **firstClass** устанавливается значение **false**, а для **secondClass** значение **true**.

Альтернативная запись:
```html
<div [class.firstClass]="true">
	<p [class.firstClass]="false" [class.secondClass]="true"></p>
</div>
```


### ngStyle
Директива **ngStyle** позволяет задать набор стилей, которые применяются к элементу.
```html
<div [ngStyle]="{'property':'value', 'property':'value'}">
	<p [ngStyle]="{'property':'value', 'property':'value'}"></p>
</div>
```
**[ngStyle] принимает js-объект**, в котором ключи - названия свойств CSS.

Альтернативная запись:
```html
<div [style.property]="value" [style.property]="value">
	<p [style.property]="value" [style.property]="value"></p>
</div>
```


### Динамическое изменение стилей

Директивы **ngClass** и **ngStyle** позволяют устанавливать привязку к выражениям, благодаря чему мы можем динамически менять стили или классы. Например:
```html
<style>
	.invisible { display: none; }
</style>

<div [ngClass]="{invisible: visibility}">Visible</div>
<button (click)="toggle()">Toggle</button>
```
```typescript
visibility: boolean = true;
toggle(){
    this.visibility=!this.visibility;
}
```

Альтернативная запись:
```html
<div [class.invisible]="visibility"></div>

<div [style.display]="visibility==true?'block':'none'"></div>
```




Сама по себе директива не заработает. нужно ее подключить в модуле приложения,
импортируем и добавляем в **declarations**
```typescript
import { BoldDirective} from './bold.directive';

declarations: [ AppComponent, BoldDirective]
```


---



### атрибутивные директивы
ngModel, ngStyle, ngClass

### структурные директивы
 ngFor и ngIf ngSwitch


---

## Создание атрибутивных директив
Директива - это обычный класс на TS, к которому применяется директива **Directive**

Создание директивы аналогично созданию компонента.
* Импорт **Directive** декоратор (вместо **Component** декоратор).
* Импорт **Input**, **TemplateRef** и **ViewContainerRef** символы; Вы будете нуждаться в них для любой структурной директивы.
* Примените декоратор к классу директивы.
* Установите CSS селектор атрибута , который идентифицирует директиву , когда применяется к элементу в шаблоне.

Имя атрибута должно быть прописано в **lowerCamelCase** и начинается с префиксом. Не используйте ng. Этот префикс принадлежит Угловое. Выберите что - то короткое , который подходит вам или вашей компании. В этом примере префикс **my**.


```typescript
import {Directive, ElementRef} from '@angular/core';

@Directive({
    selector: '[myBold]'
})
export class BoldDirective{
    constructor(private elementRef: ElementRef){
        this.elementRef.nativeElement.style.fontWeight = "bold";
    }
}
```
**ElementRef**  - представляет ссылку на элемент, к которому будет применяться директива.

Селектор CSS для атрибута должен определяться в квадратных скобках.

Применение:
```html
<div myBold></div>
```

импортировать и добавить в секцию **declarations**
```typescript
import { BoldDirective} from './bold.directive';

declarations: [ AppComponent, BoldDirective],
```

Для управления стилизацией элемента удобнее для управления стилем использовать рендерер.
```typescript
import {Directive, ElementRef, Renderer} from '@angular/core';
@Directive({
    selector: '[myBold]'
})
export class BoldDirective{
    constructor(private elementRef: ElementRef, private renderer: Renderer){
        this.renderer.setElementStyle(this.elementRef.nativeElement, "font-weight", "bold");
    }
}
```
**Renderer** представляет сервис, который также при вызове директивы автоматически передается в ее конструктор, и мы можем использовать данный сервис для стилизации элемента.




---



## Создание структурных директив

С помощью входного свойства-сеттера, к которому применяется декоратор **Input**, мы будем получать из вне некоторые значения, которые могут использоваться при создании разметки html. В данном случае мы получаем извне некоторое булевое значение
```typescript
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({ selector: '[while]' })
export class WhileDirective {
    constructor(private templateRef: TemplateRef<any>, private viewContainer: ViewContainerRef) { }

    @Input() set while(condition: boolean) {
        if (condition) {
          this.viewContainer.createEmbeddedView(this.templateRef);
        } else {
          this.viewContainer.clear();
        }
    }
}
```

Для получения доступа к шаблону директивы применяется объект **TemplateRef**. Этот объект автоматически передается в конструктор через механизм внедрения зависимостей. Кроме этого объекта в конструктор также передается объект рендерера - **ViewContainerRef**. Ну и с помощью применения модификатора private для обоих этих параметров автоматически будут создаваться локальные переменные, к которым мы затем сможем обратиться.

```typescript
import { WhileDirective } from './while.directive';

declarations: [ AppComponent, WhileDirective ]
```




---



### HostListener
```typescript
@HostListener("event") handler() {
}
```
Декоратор **@HostListener** позволяет связать события DOM и методы директивы.
в декоратор передается название события, по которому будет вызываться метод



## HostBinding
Еще один декоратор - **HostBinding** позволяет связать обычное свойство класса со свойством элемента, к которому применяется директива
```typescript
@HostBinding("style.fontWeight") get getFontWeight(){
	return this.fontWeight;
}
```
Инструкция `@HostBinding("style.fontWeight") get getFontWeight()` связывает со свойством `"style.fontWeight"` значение, которое возвращается этим геттером **getFontWeight**. А он возвращает значение свойства **fontWeight**, которое также меняется при наведении указателя мыши.

## Свойство host
мы можем определить обработчики событий в декораторе Directive с помощью его свойства **host** Вместо применения декораторов **HostListener** и **HostBinding**
```typescript
@Directive({
    selector: '[bold]',
    host: {
        '(event)': 'handler()',
    }
})
```


---


### Получение параметров в директивах !!!


### ngIf
Директива **ngIf** позволяет удалить или, наоборот, отобразить элемент при определенном условии
```html
<div *ngIf="true"></div>
<div *ngIf="!true"></div>
```
Начиная с версии **Angular 4.0** директива **ngIf** обогатилась новыми возможностями. В частности, мы можем задавать альтернативные выражения с помощью директивы **ng-template**
```html
<div *ngIf="false;else elseBlock"></div>
<ng-template #elseBlock>Else template</ng-template>
```
```html
<div *ngIf="false; then thenBlock else elseBlock"></div>   
<ng-template #thenBlock>Then template</ng-template>  
<ng-template #elseBlock>Else template</ng-template>   
```

### ngFor
Директива **ngFor** позволяет перебрать в шаблоне элементы массива

Если нужно,можно использовать переменную **index**
```html
<ul>
	<li *ngFor="let item of array;let i = index">{{i}}: {{item}}</li>
</ul>
```
```typescript
export class AppComponent {
	array =["1", "2", "3", "4"];
}
```





#### Символ звездочки и синтаксический сахар

Можно заметить, что при использовании директив **ngFor** и **ngIf** перед ними ставится символ звездочка. По факту это не более чем синтаксический сахар, который упрощает применение директивы.
```html
<p *ngIf="true">Привет мир</p>

<template [ngIf]="true">
	<p>Привет мир</p>
</template>
```
```html
<ul>
	<li *ngFor="let item of array">{{item}}</li>
</ul>

<ul>
	<template ngFor let-item [ngForOf]="array">
		<li>{{item}}</li>
	</template>
</ul>
```
В итоге мы можем выбирать либо первый способ со звездочкой, который более компактный, либо второй способ с элементами **template**.


### ngSwitch
С помощью директивы **ngSwitch** можно встроить в шаблон конструкцию **switch..case** и в зависимости от ее результата выполнения выводить тот или иной блок

```html
<div [ngSwitch]="num">
	<template [ngSwitchCase]="1">{{num * 10}}</template>
	<template [ngSwitchCase]="2">{{num * 100}}</template>
	<template ngSwitchDefault>{{num * 1000}}</template>
</div>
```
