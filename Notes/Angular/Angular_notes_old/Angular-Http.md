# HTTP

## Get
При взаимодействии с сервером, как правило, обращения к серверу происходят не непосредственно из компонента, а из вспомогательных сервисов. Компоненты же выступают в качестве потребителей данных, которые получены от сервисов.

Для выполнения get-запроса у объекта Http вызывается метод **get()**

Сам метод **http.get()** возвращает объект **Observable<Response>**

 **Observable** представляет своего рода **поток**, и для **прослушивания событий** из этого потока применяется метод **subscribe**


Файл сервиса:
```typescript
import {Injectable} from '@angular/core';
import {Http} from '@angular/http';

@Injectable()
export class HttpService {
    constructor(private http: Http) { }
    getData() {
        return this.http.get('assets/user.json');
    }
}
```
файл модуля:
```typescript
import { Component, OnInit} from '@angular/core';
import { Response } from '@angular/http';
import { HttpService } from './http.service';

@Component({
    selector: 'app-root',
    template: ``
})
export class AppComponent implements OnInit {
    constructor(private httpService: HttpService) {} // инициализация сервиса через конструктор
    ngOnInit(){
        this.httpService.getData().subscribe(data => console.log(data.json()));
    }
}
```


### Объект Observable и библиотека RxJS
Методы объекта Http после выполнения запроса возвращают объект Observable, который определен в библиотеке RxJS ("Reactive Extensions"). Она не является непосредственно частью Angular, однако широко используется особенно при взаимодействии с сервером по http. Эта библиотека реализует паттерн "асинхронный наблюдатель" (asynchronous observable). Так, выполнение запроса к серверу с помощью класса Http выполняются в асинхронном режиме



## Post






