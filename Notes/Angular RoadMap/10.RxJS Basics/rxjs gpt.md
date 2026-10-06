
## 1️⃣ Что такое RxJS?

**RxJS (Reactive Extensions for JavaScript)** — это библиотека для работы с асинхронными и событийными потоками данных с помощью **Observable**.

---

## 2️⃣ Основные понятия

|Понятие|Описание|
|---|---|
|**Observable**|Поток данных, который может испускать значения, ошибки или завершение|
|**Observer**|Объект, который подписывается на Observable и реагирует на его события|
|**Subscription**|Связь между Observable и Observer, её можно отменить|
|**Operators**|Функции для трансформации, фильтрации и комбинирования Observable|
|**Subject**|Observable + Observer (может излучать события сам)|
|**BehaviorSubject**|Subject c начальными значениями|
|**ReplaySubject**|Subject, запоминающий несколько последних значений|
|**AsyncSubject**|Subject, который отдаёт только последнее значение при завершении|

---

## 3️⃣ Жизненный цикл Observable

- **next()** — передача значения
    
- **error()** — ошибка, поток завершается
    
- **complete()** — успешное завершение потока
    

---

## 4️⃣ Операторы RxJS (основные)

|Группа|Примеры|
|---|---|
|**Creation**|`of()`, `from()`, `interval()`, `timer()`, `ajax()`|
|**Transformation**|`map()`, `mergeMap()`, `switchMap()`, `concatMap()`, `exhaustMap()`|
|**Filtering**|`filter()`, `debounceTime()`, `distinctUntilChanged()`, `take()`, `takeUntil()`|
|**Combination**|`merge()`, `concat()`, `combineLatest()`, `forkJoin()`, `zip()`|
|**Utility**|`tap()`, `catchError()`, `finalize()`, `delay()`, `retry()`|

---

## 5️⃣ Потоковые паттерны

- **switchMap** — отменяет предыдущий поток, оставляя только последний
    
- **mergeMap** — запускает все вложенные потоки параллельно
    
- **concatMap** — выполняет вложенные потоки последовательно
    
- **exhaustMap** — игнорирует новые, пока выполняется текущий
    

---

## 6️⃣ Обработка ошибок

ts

КопироватьРедактировать

`observable$.pipe(   catchError(err => of('fallback value')) )`

---

## 7️⃣ Best Practices

- ✅ Всегда отписывайтесь от Subscription
    
- ✅ Используйте `takeUntil()` для управления жизненным циклом
    
- ✅ Используйте `pipe()` для чистого кода
    
- ✅ Разделяйте побочные эффекты с `tap()`
    
- ✅ Используйте `async` пайп в Angular
    

---

## 8️⃣ Примеры

ts

КопироватьРедактировать

`import { of, interval } from 'rxjs'; import { map, filter, take } from 'rxjs/operators';  interval(1000).pipe(   filter(x => x % 2 === 0),   map(x => x * 2),   take(5) ).subscribe(console.log);`

---

## 9️⃣ Когда применять RxJS:

- Работа с потоками событий (клики, инпуты)
    
- API-запросы
    
- Управление состоянием
    
- Реактивные формы в Angular
    
- Вебсокеты и real-time data
    

---

## 1️⃣0️⃣ Где учиться:

- 📖 [https://rxjs.dev/](https://rxjs.dev/)
    
- 📖 [https://learnrxjs.io/](https://learnrxjs.io/)
    
- 🔥 RxJS Marbles [https://rxmarbles.com/](https://rxmarbles.com/)