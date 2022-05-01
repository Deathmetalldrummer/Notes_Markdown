# Service

Файл сервиса:
```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class MyService {
}
```
Чтобы указать, что сервис сам может использовать другие сервисы, к классу сервиса применяется декоратор **Injectable**. Если класс не будет иметь подобного декоратора, то встроенный механизм внедрения зависимостей не сможет создать объект этого класса и выдаст ошибку.


<br />

Внедрение в компонент (через конструктор!):
```typescript
import {MyService} from './data.service';

constructor(private myService: MyService) { }
```
*Чтобы задействовать сервис в компоненте, его надо импортировать.*

Также необходимо добавить в коллекцию **providers** (module.ts) компонента:
```typescript
providers: [MyService]
```




<br />

В отличие от компонентов и директив **сервисы не работают с представлениями**, то есть с разметкой html, не оказывают на нее прямого влияния. Они выполняют строго определенную и достаточно узкую задачу.

Стандартные задачи сервисов:

* Предоставление данных приложению. Сервис может сам хранить данные в памяти, либо для получения данных может обращаться к какому-нибудь источнику данных, например, к серверу.

* Сервис может представлять канал взаимодействия между отдельными компонентами приложения

* Сервис может инкапсулировать бизнес-логику, различные вычислительные задачи, задачи по логгированию, которые лучше выносить из компонентов. Тем самым код компонентов будет сосредоточен непосредственно на работе с представлением. Кроме того, тем самым мы также можем решить проблему повторения кода, если нам потребуется выполнить одну и ту же задачу в разных компонентах и классах


<br />
<br />
<br />

Файл сервиса *app.service.ts*:
```typescript
import {Injectable} from '@angular/core';

@Injectable()
export class AppService {
    data = {
        user: 'user'
    }
    getData() {
        return this.data;
    }
}
```

Файл компонента *app.component.ts*:
```typescript
import { Component, OnInit} from '@angular/core';
import { AppService } from './app.service';

@Component({
  selector: 'app-root',
  template: ``
})
export class AppComponent implements OnInit {
    constructor(private appService: AppService) {}
    ngOnInit() {
        console.log(this.appService.getData())
    }
}
```

Файл модуль *app.module.ts*:
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { AppService } from './app.service';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [AppService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
