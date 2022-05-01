# Маршрутизация
### Определение маршрутов

Ключевым для работы маршрутизации является модуль **RouterModule**, который располагается в пакете **@angular/router**.

Файл *app.routes.ts*:
```typescript
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home.component';
import { AboutComponent } from './about.component';
import { ContactsComponent } from './contacts.component';
import { ErrorComponent } from './error.component';

appRoutes: Routes = [
 {path: '', component: HomeComponent},
 {path: 'about', component: AboutComponent},
 {path: 'contacts', component: ContactsComponent},
 {path: '**', component: ErrorComponent}
];
export const ROUTES = RouterModule.forRoot(appRoutes);
```
Импортируем все модули которые будут использоваться + **Routes** , **RouterModule**.


На место элемента `<router-outlet>` будет рендериться компонент, выбранный для обработки запроса.
```html
<router-outlet></router-outlet>
```



<!-- создаем массив объектов с типом Routes   -->



### Определение адресов
Для определения адресов ссылок применяется директива **routeLink**.
```html
<a routerLink="/about">О сайте</a>
```



### Стилизация активных ссылок
Для стилизации активных ссылок применяется специальная директива **routerLinkActive**
```html
<a routerLink="/about"  routerLinkActive="active">О сайте</a>
```



### Переадресация
Вполне возможно, что по какому-то маршруту мы захотим сделать переадресацию по другому пути. Например, в случае, если нужного маршрута для запроса не найдено, мы можем переадресовать на главную страницу.

Для переадресации указываем параметр **redirectTo**. Его значение представляет путь переадресации.
```typescript
{ path: '**', redirectTo: '/'}
```

### Полное соответствие маршруту
Значение pathMatch:'full' указывает, что запрошенный адрес должен полностью соответствовать маршруту
```typescript
{ path: 'contact', redirectTo: '/about', pathMatch:'full'}
```
```html
<a routerLink="" routerLinkActive="active" [routerLinkActiveOptions]="{exact:true}">Главная</a>
```
Значение {exact:true} указывает на то, что для установки активной ссылки будет применяться полное соответствие
