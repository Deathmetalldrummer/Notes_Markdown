# TypeScript

## Использование

#### Установка 

```bash
npm i -g typescript
```

С помощью параметра `–target` или его сокращенной версии `–t` можно задать версию стандарта JavaScript,   "ES3", "ES5" или "ES6".(Из консоли)



#### Запуск

```bash
tsc
```

*Запуск с определенными настройками*

```bash
 tsc --project configs/my_tsconfig.json
```



#### Настройка

**tsconfig.json** - файл настроек TypeScript

свойство compilerOptions" настраивает параметры компиляции

```JSON
{
   "compileOnSave": true,
   "compilerOptions": {
       "target": "ES5",
       "removeComments": true,
       "outFile": "./index.js"
   },
   "files": ["index.ts"]
}
```

Если секция "files" не указана в файле tsconfig.json, то компилятор по умолчанию включает все файлы TypeScript (файлы с расширением .ts и .tsx), которые находятся в каталоге и подкаталогах проекта. Если же указана секция "files", то используются только файлы из этой секции.

```JSON
"exclude":[
    "wwwroot",
    "node_modules"
]
```

При этом следует учитывать, что если в файле одновременно будут заданы обе секции files и exclude, то секция exclude будет игнорироваться.



## Типы примитивов

Примитивные типы являются строительными блоками всех остальных типов.

В TypeScript есть 6 примитивных типов:

1. **boolean**: логическое значение true или false
2. **number**: числовое значение и числа с плавающей запятой
3. **string**: текст/строки
4. **undefined**: неопределённое значение
5. **null**: нулевое значение
6. **void**: отсутствие конкретного типа

```ts
let flag: boolean = true;
let num: number = 123;
let str: string = 'Hello, TypeScript!';
let undefValue: undefined = undefined;
let nullValue: null = null;

// Void
function logMessage(message: string): void {
  console.log(message);
}
let unusable: void = undefined; // Может иметь только значение undefined или null
```



## Типы объектов

1. **Interface**: Описывает свойства и типы объекта.
2. **Class**: Описывает свойства, типы и поведение объекта.
3. **Array**: список значений
4. **Tuple**: массив фиксированной длины (**Кортеж**)
5. **Enum**: перечисление именованных значений



*Объект с произвольным количеством свойств (например, хештаблица или словарь)*

```ts
{ [key: string]: Type }
{ [key: number]: Type }
{ [key: symbol]: Type }
{ [key: `data-${string}`]: Type }
```



#### Интерфейс

Определяет структуру объекта/класса

```ts
interface User {
  name: string;
  age: number;
}
```

**Подробнее ниже*

#### Класс

Реализует интерфейс **User**

```ts
class Person implements User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
```

**Подробнее ниже*

#### Массивы

Как и в других языках, массив - это список значений.

```ts
let numbers: number[] = [1, 2, 3, 4, 5];
let numbers: Array<string> = [1, 2, 3, 4, 5];

// Массив функций, возвращающих строки
// (() => string)
// { (): string }
// Array<() => string>
let arrayFunctionString: (() => string)[] = [() => 'string', () => 'string'];
let arrayFunctionString: { (): string }[] = [() => 'string', () => 'string'];
let arrayFunctionString: Array<() => string> = [() => 'string', () => 'string'];
```

#### Кортеж

Кортеж/Tuple - массив фиксированной длины. Он полезен, когда вы знаете точное количество элементов в массиве.

```ts
let tuple: [string, number, string] = ['Hello', 42, 'string'];

type Numbers = [number, number]
type Strings = [string, string]

type NumAndStr = [...Numbers, ...Strings]
// [number, number, string, string]

type NumberAndRest = [number, ...string[]]
// [number, любое количество строк]

type RestAndBool = [...any[], boolean]
// [любое количество любых типов, boolean]
```



#### Перечисления

Перечисления - это способ дать более дружественные имена наборам числовых значений.
По умолчанию перечисления начинают нумеровать своих членов, начиная с 0.

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

// Доступ к значениям перечисления с помощью имени перечисления
console.log(Direction.Up); // Вывод: 0
// Доступ к значениям перечисления с помощью индекса перечисления
console.log(Direction[1]); // Вывод: "Down"
```



##### Перечисление с пользовательскими значениями:

```ts
enum StatusCode {
  Success = 200,
  BadRequest = 400,
  NotFound = 404,
  InternalServerError = 500,
}

function logResult(status: StatusCode) {
  if (status === StatusCode.Success) {
console.log('The request was successful');
  } else {
console.log('The request failed with status code: ', status);
  }
}

logResult(StatusCode.Success); // Вывод: " The request was successful"
logResult(StatusCode.NotFound); // Вывод: " The request failed with status code: 404"
```



##### Перечисление со строковыми значениями:

```ts
enum UserRole {
  Admin = 'ADMIN',
  User = 'USER',
  Guest = 'GUEST',
}

// Используйте значение перечисления для сравнения или других операций
function checkRole(role: UserRole) {
  if (role === UserRole.Admin) {
console.log('This is an admin user');
  } else {
console.log('This is not an admin user');
  }
}

checkRole('ADMIN'); // Вывод: " This is an admin user"
```



## Другие типы

1. **any**: любой тип
2. **unknown**: неизвестный тип
3. **never**: never тип
4. **object**: объектный тип



#### Any

Позволяет присваивать переменной значения любого типа.

```ts
let data: any = 'Hello';
data = 42;
data = true;

function untypedFunction(inputs: any[]): any {
  // ...
}
```
Если же переменная определяется без значения, и только впоследствии при работе программы ей присваивается значение, тогда считается, что она имеет тип any:

```typescript
let x;  // тип any
x = 10;
```



#### Object

**object** - это тип, который представляет не примитивный тип, т.е. все, что **не является**
**number**, **string**, **boolean**, **symbol**, **null** или **undefined**.

```ts
function logObject(obj: object): void {
  console.log(obj);
}

logObject({ greeting: 'Hello, TypeScript!' });
```


#### Unknown

unknown является типобезопасным аналогом any - это означает, что мы можем присвоить
ему любое значение, но мы не можем получить доступ к его свойствам, если только не
сузим его до более конкретного типа.
```ts
let unknownValue: unknown = 42;
console.log(unknownValue * 2); // Error: Оператор '*' не может быть применён к типам 'unknown' и '2'.

// Вы должны принудительно определить тип, прежде чем использовать его
if (typeof unknownValue === 'number') {
    console.log(unknownValue * 2); // Вывод: 84
}

```


#### Never

never - это тип, который представляет собой тип значений, которые никогда не встречаются.
Например, never - это тип возврата для выражения функции или выражение стрелочной функции,
которое всегда выбрасывает исключение или которое ничего не возвращает.
```ts
function throwError(message: string): never {
  throw new Error(message);
}
```



## Утверждение типа `as` (assertion)

Type assertion представляет модель преобразования значения переменной к определенному типу. Обычно в некоторых ситуациях одна переменная может представлять какой-то широкий тип, например, any, который по факту допускает значения различных типов. Однако при этом нам надо использовать переменную как значение строго определенного типа. И в этом случае мы можем привести к этому типу.

Утверждение типа - это способ сообщить компилятору, что вы лучше него знаете тип переменной

Есть две формы приведения. Первая форма заключается в использовании угловых скобок:

```ts
let someValue: any = 'This is a string';
let strLength: number = (<string>someValue).length;
console.log(strLength); // Вывод: 16

let someValue: string | number = 'This is a string';
let strLength: number = (<string>someValue).length;
console.log(strLength); // Вывод: 16
```

Вторая форма заключается в применении оператора as:

```ts
let someValue: any = 'This is a string';
let strLength: number = (someValue as string).length;
console.log(strLength); // Вывод: 16

let someValue: string | number = 'This is a string';
let strLength: number = (someValue as string).length;
console.log(strLength); // Вывод: 16
```



#### Как const

Утверждение `as const` используется, чтобы сообщить компилятору, что значение является константой.

```ts
let colors = ['red', 'green', 'blue'] as const;
// colors теперь имеет тип readonly ['red', 'green', 'blue'].
colors[0] = 'yellow'; // Error: Cannot assign to '0' because it is a read-only property
```



#### Обход проверки типов TypeScript с помощью `as` и `any`

```ts
let obj: unknown = { key: 'value' };
let bypassTypeCheck = (obj as any).key;
```



## Оператор утверждения Non-Null

Оператор утверждения **Non-null** (!) используется, чтобы сообщить компилятору, что значение не является нулевым или неопределённым.

```ts
// Объявление переменной с возможным нулевым значением
let possibleNullValue: string | null = 'TypeScript';

console.log(possibleNullValue.length); // Error: Object is possibly 'null'
console.log(possibleNullValue!.length); // Вывод: 10
```



## Ключевое слово `satisfies`

Ключевое слово satisfies используется для проверки того, удовлетворяет ли тип заданному ограничению.
Без ключевого слова satisfies нам пришлось бы использовать утверждения типов, чтобы проверить, удовлетворяет ли тип заданному ограничению.

```ts
type Colors = 'red' | 'green' | 'blue';
type RGB = [red: number, green: number, blue: number];

const palette = {
  red: [255, 0, 0],
  green: '#00ff00',
  bleu: [0, 0, 255],
  //~~~~ Опечатка поймана!
} satisfies Record<Colors, string | RGB>;

// Оба этих метода все ещё доступны!
const redComponent = palette.red.at(0);
const greenNormalized = palette.green.toUpperCase();
```



## Вывод типов

Компилятор TypeScript может определить тип переменной по её значению.

Объявление переменной с предполагаемым типом
Компилятор TypeScript примет тип переменной за строку

```ts
let inferredValue = 'TypeScript';
console.log(inferredValue); // Вывод: "TypeScript"
```



## Совместимость типов

TypeScript использует структурную типизацию для определения совместимости типов.
Это означает, что два типа считаются совместимыми, если они имеют одинаковую структуру, независимо от их имён.

Даже если p2 имеет другое имя, он все равно совместим с p1

```ts
interface Point {
  x: number;
  y: number;
}

let p1: Point = { x: 10, y: 20 }
let p2: { x: number; y: number } = p1;

console.log(p2.x); // Вывод: 10
```



## Объединение типов (union)

Объединения или union не являются собственно типом данных, но они позволяют определить переменную, которая может хранить значение двух или более типов.

Объединение типов используется для представления значения, которое может быть одним из нескольких типов.

```ts
// Объявление объединения типов
let unionValue: string | number;

unionValue = 'TypeScript';
unionValue = 42;

// Это также работает с объектными типами
type User = { name: string; age: number };
type Admin = { name: string; age: number; role: string };

let user: User | Admin;
```



## Пересечение типов

Пересечение типов используется для объединения нескольких типов в один.

```ts
type Human = {
  name: string;
  age: number;
};

type Animal = {
  species: string;
  age: number;
};

// Объявление типа пересечения
let human: Human & Animal = {
  name: 'John',
  species: 'Human',
  age: 30,
};
```



## Псевдонимы типа

Псевдонимы типов используются для создания нового имени для типа.

```ts
// Объявление псевдонима типа
type Name = string;
type Age = число;
type User = { name: Name; age: Age };

const user: User = { name: 'John', age: 30 };
```



## Оператор `keyof`

Оператор `keyof` используется для получения ключей объекта.

```ts
interface User {
  name: string;
  age: число;
  location: string;
}

type UserKeys = keyof User; // " name" | "age" | "location"
const key: UserKeys = 'name';
```



## Защита типов: 

#### Защита типов с помощью `typeof`

Защита типа typeof используется для сужения типа переменной на основе её значения.

```ts
let value: string | number = 'hello';

// Защита типа с использованием typeof
if (typeof value === 'string') {
  console.log('value is a string');
} else {
  console.log('value is a number');
}
```



#### Защита типа с помощью instanceof

```ts
class Bird {
  fly() {
    console.log('flying...');
  }
  layEggs() {
    console.log('laying eggs...');
  }
}

const pet = new Bird();

if (pet instanceof Bird) {
  pet.fly();
} else {
  console.log('pet is not a bird');
}
```



#### Защита типа с помощью равенства

```ts
function example(x: string | number, y: string | boolean) {
  if (x === y) {
    // Теперь мы можем вызвать любой метод 'string' для 'x' или 'y'.
    x.toUpperCase();
    y.toLowerCase();
  } else {
    console.log(x);
    console.log(y);
  }
}
```



#### Защита типа с использованием истинности

```ts
function getUsersOnlineMessage(numUsersOnline: number) {
  if (numUsersOnline) {
    return `There are ${numUsersOnline} online now!`;
  }

  return "Nobody's here. :(";
}
```



## Предохранители

*Предикаты типа*

```ts
function isType(val: unknown): val is T {
  // возвращает `true`, если `val` имеет тип `T`
}

if (isType(val)) {
  // `val` имеет тип `T`
}
```



*`typeof`*

```ts
declare value: string | number | boolean
const isBoolean = typeof value === 'boolean'

if (typeof value === 'number') {
  // значением `value` является число
} else if (isBoolean) {
  // `value` имеет логическое значение
} else {
  // значением `value` является строка
}
```



*`instanceof`*

```ts
declare value: Date | Error | MyClass
const isMyClass = value instanceof MyClass

if (value instanceof Date) {
  // значением `value` является экземпляр `Date`
} else if (isMyClass) {
  // значением `value` является экземпляр `MyClass`
} else {
  // значением `value` является экземпляр `Error`
}
```



*`in`*

```ts
interface Dog { woof(): void }
interface Cat { meow(): void }

function speak(pet: Dog | Cat) {
  if ('woof' in pet) {
    pet.woof()
  } else {
    pet.meow()
  }
}
```



## Функции

Типы функций используются для описания структуры функции.

```ts
(arg1: Type, argsN: Type) => Type
// or
{ (arg1: Type, argN: Type): Type }

// Обычная функция
function add(a: number, b: number): number {
	return a + b;
}

// Стрелочная функция
const multiply = (a: number, b: number): number => {
    return a * b;
};

// Тип функции
let divide: (a: number, b: number) => number;

divide = (a, b) => {
	return a / b;
};

// Лямбда
let sum = (x: number, y: number): number => x + y;
```



*Конструктор*

```ts
new () => ConstructedType
// or
{ new (): ConstructedType }
```



#### Необязательные параметры

*Функциональный тип с опциональным параметром*

```ts
// (arg1: Type, optional?: Type) => ReturnType

function getName(firstName: string, lastName?: string): string {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

var result = getName("Иван", "Кузнецов");
console.log(result); // Иван Кузнецов
var result2 = getName("Вася");
console.log(result2); // Вася
```



#### Неограниченное количество параметров

Функциональный тип с оставшимися параметрами

```ts
(arg1: Type, ...args: Type[]) => ReturnType

function addNumbers(firstNumber: number, ...numberArray: number[]): number {

    var result = firstNumber;
    for (var i = 0; i < numberArray.length; i++) {
        result+= numberArray[i];
    }
    return result;
}

var result1 = addNumbers(3, 7, 8);
console.log(result1); // 18

var result2 = addNumbers(3, 7, 8, 9, 4);
console.log(result2); // 31
```



#### Функциональный тип со статическим свойством

```ts
{ (): Type; staticProp: Type }
```



#### Параметры по умолчанию

*Дефолтное значение параметра*

```ts
function fn(arg = 'default'): ReturnType {}

function getName(firstName: string, lastName: string="Иванов"): string {

    return firstName + " " + lastName;
}

var result = getName("Иван", "Кузнецов");
console.log(result); // Иван Кузнецов
var result2 = getName("Вася");
console.log(result2); // Вася Иванов
```



#### *Типизация `this`*

```ts
function fn(this: Type, arg: string) {}
```



## Перегрузка функций

Перегрузки функций используются для описания нескольких сигнатур функции.

```ts
function add(a: number, b: number): number;
function add(a: string, b: string): string;

// Помните, что существует только одна реализация функции.
// Перегрузки используются только для описания сигнатуры функции.
function add(a: any, b: any): any {
  return a + b;
}

console.log(add(1, 2)); // 3
console.log(add('Hello', ' World')); // "Hello World"

//----------------
function add(x: string, y: string): string;
function add(x: number, y: number): number;
function add(x: any, y: any): any {
    return x + y;
}

var result1 = add(5, 4);
console.log(result1);   // 9
var result2 = add("5", "4");
console.log(result2);   // 54
var result3 = add(true, false);
console.log(result3); // ошибка
```



## Интерфейсы

Интерфейсы используются для описания структуры объекта.

```ts
interface User {
  name: string;
  age: number;
}
const user: User = { name: 'John Doe', age: 30 };
```



#### Типы по сравнению с интерфейсами

Типы используются для создания нового именованного типа на основе существующего типа или для объединения существующих типов в новый тип. Они могут быть созданы с помощью ключевого слова type. Например:

```ts
type Person = { name: string; age: number };
const person: Person = { name: 'John Doe', age: 30 };
```

Интерфейсы, с другой стороны, используются для описания структуры объектов и классов.
Они могут быть созданы с помощью ключевого слова interface. Например:

```ts
interface Person {
  name: string;
  age: number;
}
const person: Person = { name: 'John Doe', age: 30 }
```

Основное различие между типами и интерфейсами заключается в том, что типы можно использовать для создания новых типов на основе существующих, в то время как интерфейсы могут использоваться только для описания структуры объектов и классов. Также интерфейсы можно расширять с помощью ключевого слова extends, а типы - с помощью оператора &.



#### Расширение интерфейсов

```ts
// Интерфейс Square наследуется от Shape с помощью ключевого слова extends
interface Shape {
  width: number;
  height: number;
}
interface Square extends Shape {
  sideLength: number;
}

let square: Square = { width: 10, height: 10, sideLength: 10 };
```



#### Гибридные типы

Гибридные типы - это типы, которые сочетают в себе особенности двух или более типов. Например, гибридный тип может быть объектом, который имеет и свойства, и методы, или массивом, который имеет и числа, и строки.

```ts
type Education = { degree: string; school: string; year: number };
type User = { name: string; age: number; email: string; education: Education };
```



## Классы 

Классы используются для создания объектов, которые имеют как данные, так и функциональность.

```ts
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }

  makeSound(): void {
    console.log(`${this.name} is making a sound`);
  }
}

const dog = new Animal('Dog');
dog.makeSound(); // Выходные данные: Dog is making a sound
```



#### Параметры конструктора

Параметры конструктора могут быть объявлены как **public**, **private** или **protected**.

- **Public** (по умолчанию) свойства доступны из любого места.
- **Private** свойства доступны только изнутри класса
- **Protected** свойства доступны только в пределах класса и его подклассов

Примечание: TypeScript автоматически создаёт свойства для параметров конструктора, которые объявлены как public или protected.

```ts
class Example {
  constructor(private name: string, public age: number) {}
}
```



#### Перегрузки конструктора

Перегрузки конструкторов используются для создания нескольких конструкторов для класса

```ts
class Point {
  // Перегрузки:
  constructor(x: number, y: string);
  constructor(s: string);
  constructor(xs: any, y: any) {
    // Примечание: у нас есть только одна реализация конструктора.
    // Перегрузки используются только для определения типов параметров
  }
}
```



#### Абстрактные классы

Абстрактные классы используются для создания базовых классов, от которых могут быть получены другие классы. Абстрактные классы нельзя создавать напрямую. Вы можете создавать только экземпляры производных классов.

```ts
abstract class Animal {
  abstract makeSound(): void;

  move(): void {
    console.log('moving...');
  }
}

// Собака наследует от животного (наследование).
// Также известен как подкласс или производный класс.
class Dog extends Animal {
  makeSound(): void {
    console.log('bark');
  }
}
```



## Дженерики

Дженерики используются для создания многократно используемых компонентов, которые могут работать с различными типами, а не с одним.

```ts
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>('Hello'); // Тип вывода будет 'string'
```



#### Общие типы

Общие типы также могут быть использованы с классами, интерфейсами, объектными типами и псевдонимами типов.

```ts
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();

myGenericNumber.zeroValue = 0;
myGenericNumber.add = function (x, y) {
  return x + y;
};
```



#### Ограничения дженерика

Ограничения дженерика используются для обеспечения того, чтобы параметр типа был ограничен определённым типом или набором типов. Например, мы можем использовать ключевое слово `extends`, чтобы ограничить параметр типа типом, который является производным от определённого типа.

```ts
interface Measurable {
  length: number;
}

// Здесь мы ограничиваем параметр типа T типом Measurable.
function loggingIdentity<T extends Measurable>(arg: T): T {
  // Теперь мы знаем, что у него есть свойство .length, поэтому ошибки больше не будет
  console.log(arg.length);

  return arg;
}

// Ошибка, у числа нет свойства .length
loggingIdentity(3);
loggingIdentity({ length: 10, value: 3 }); // OK
```



*Функция с типом параметров*

```ts
<T>(items: T[], callback: (item: T) => T): T[]
```



*Интерфейс с несколькими типами*

```ts
interface Pair<T1, T2> {
  first: T1
  second: T2
}
```



*Ограниченный тип параметра*

```ts
<T extends ConstrainedType>(): T
```



*Дефолтный тип параметра*

```ts
<T = DefaultType>(): T
```



*Ограниченный и дефолтный тип параметра*

```ts
<T extends ConstrainedType = DefaultType>(): T
```



*Общий кортеж*

```ts
type Arr = readonly any[]

function concat(<U extends Arr, V extends Arr>(x: U, y: V): [...U, ...V] {
  return [...x, ...y]
})

const strictResult = concat([1, 2] as const, ['3', '4'] as const)
// type -> [1, 2, '3', '4']

const relaxedResult = concat([1, 2], ['3', '4'])
// type -> Array<string | number>
```



## Декораторы

Декораторы используются для изменения поведения класса, метода, свойства или параметра.

Это способ добавить дополнительную функциональность в существующий код, и они могут использоваться для широкого круга задач, включая ведение журнала, оптимизацию производительности и валидацию.

```ts
function log(target: Object, propertyKey: string | symbol, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
  console.log(`Calling ${propertyKey} with arguments: ${args}`);
    return originalMethod.apply(this, args);
  };

  return descriptor;
}

class Calculator {
  // декоратор @log изменяет поведение метода add
  // в классе Calculator. Декоратор log записывает в журнал аргументы.
  // переданные методу перед вызовом исходного метода
  @log
  add(a: number, b: number): number {
    return a + b;
  }
}

const calculator = new Calculator();
calculator.add(1, 2);
// Вывод: Calling add with arguments: 1,2
// Вывод: 3
```



## Утилитарные типы

Утилитарные типы - это типы, которые обеспечивают полезные сокращения при работе с другими типами.



#### Partial

Тип Partial используется для создания нового типа из существующего типа, в котором все свойства являются необязательными.

```ts
interface Person {
  name: string;
  age: number;
}

// toUpdate имеет тип Partial<Person>, то есть будет обладать некоторыми свойствами Person
function updatePerson(person: Person, toUpdate: Partial<Person>): Person {
  return { ...person, ...toUpdate }
}
```



#### Pick

Тип Pick используется для создания нового типа из существующего типа путём выбора набора свойств.

```ts
interface Product {
  name: string;
  description: string;
  amount: number;
  shippingCountry: string;
  shippingMethod: string;
  imageUrl: string;
  creatorId: string;
  createdAt: string;
  updatedAt: string;
}

// ProductPreview выбирает только те свойства, которые нам нужны
type ProductPreview = Pick<Product, 'name' | 'description' | 'amount' | 'imageUrl'>;
```



#### Omit

Тип Omit используется для создания нового типа из существующего путём исключения набора свойств.

```ts
type User = {
  id: string;
  name: string;
  email: string;
  password: string;
  createdAt: string;
  updatedAt: string;
};

// Удаляем свойство password из User
type PublicUser = Omit<User, 'password'>;
```



#### Readonly

Тип Readonly используется для создания нового типа из существующего, где все свойства становятся доступными для чтения.

```ts
interface Todo {
  title: string;
}

const todo: Readonly<Todo> = {
  title: 'Delete inactive users',
};

// Невозможно присвоить 'title', потому что это свойство только для чтения.
todo.title = 'Hello';
```



#### Record

Вы можете использовать его для создания типа, в котором ключ имеет определённый тип, а значение - другой тип.

```ts
type Cats = Record<
  string,
  {
    name: string;
    age: number;
  }
>;

// Хэш-карта имён кошек и информации о них
const catInfo: Cats = {
  mimi: { name: 'Mimi', age: 3 }
  momo: { name: 'Momo', age: 2 },
};
```



#### Exclude

Тип Exclude используется для создания нового типа путём исключения набора свойств из существующего типа.

```ts
type T0 = Exclude<'a' | 'b' | 'c', 'a'>; // "b" | "c"
type T1 = Exclude<'a' | 'b' | 'c', 'a' | 'b'>; // "c"
type T2 = Exclude<string | number | (() => void), Function>; // string | number
```



#### Extract

Тип Extract используется для создания нового типа путём извлечения набора свойств из существующего типа.

```ts
type T0 = Extract<'a' | 'b' | 'c', 'a' | 'f'>; // "a"
type T1 = Extract<string | number | (() => void), Function>; // () => void
type T2 = Extract<string | number | (() => void), Function | string>; // string | (() => void)
```



#### NonNullable

Тип NonNullable используется для создания нового типа путём исключения null и undefined из существующего типа.

```ts
type T0 = NonNullable<string | number | undefined>; // string | number
type T1 = NonNullable<string[] | null | undefined>; // string[]
```



#### Parameters

Тип Parameters используется для создания нового типа из типа функции путём извлечения типов её параметров.

```ts
type T0 = Parameters<() => string>; // []
type T1 = Parameters<(s: string) => void>; // [string]
type T2 = Parameters<<T>(arg: T) => T>; // [unknown]
type T3 = Parameters<<T extends U, U extends number[]>() => T>; // []
type T4 = Parameters<typeof Object.create>; // [object | null]
```



#### ReturnType

Тип ReturnType используется для создания нового типа из типа функции путём извлечения её возвращаемого типа.

```ts
type T0 = ReturnType<() => string>; // string
type T1 = ReturnType<(s: string) => void>; // void
type T2 = ReturnType<<T>() => T>; // {}
type T3 = ReturnType<<T extends U, U extends number[]>() => T>; // number[]
type T4 = ReturnType<<T>() => T>; // {}
type T5 = ReturnType<typeof Object.create>; // object
type T6 = ReturnType<any>; // any
type T7 = ReturnType<never>; // any
type T8 = ReturnType<string>; // Error
type T9 = ReturnType<Function>; // Error
```



#### InstanceType

Этот тип конструирует тип, состоящий из типа экземпляра функции-конструктора в Type.

```ts
class C {
  x = 0;
  y = 0;
}

type T0 = InstanceType<typeof C>; // C
type T1 = InstanceType<any>; // any
type T2 = InstanceType<never>; // any
type T3 = InstanceType<string>; // Error
type T4 = InstanceType<Function>; // Error
```



#### Awaited

Создаёт тип, который является ожидаемым аналогом заданного типа.

```ts
type T0 = Awaited<Promise<string>>; // string
type T1 = Awaited<Promise<string> | Promise<number>>; // string | number
type T2 = Awaited<Promise<string | number>>; // string | number
type T3 = Awaited<Promise<Promise<string>>; // string
type T4 = Awaited<Promise<Promise<string> | Promise<number>>; // string | number
```



## Директивы `///`

*Ссылка на встроенные типы*

```ts
/// <reference types="react-scripts" />
```

*Ссылка на другие типы*

```ts
/// <reference path="../my-types" />
/// <reference types="node" />
```



## Пространства имён

Пространства имён используются для организации кода в логические группы и для обеспечения способа обработки коллизий имён.

```ts
// myMath.ts - Объявление пространства имён
namespace MyMath {
  const PI = 3.14;

  export function calculateCircumference(diameter: number): number {
    return diameter * PI;
  }
}

// main.ts - Использование пространства имён
/// <reference path="myMath.ts" />
const circumference = MyMath.calculateCircumference(10);
```



#### Пространства имён Ambient

Модули Ambient в TypeScript используются для объявления внешних модулей или сторонних библиотек в программе на TypeScript.
Модули Ambient предоставляют информацию о типе для модулей, которые не имеют объявлений в TypeScript, но доступны в глобальной области видимости.

```ts
// myMath.d.ts - объявление пространства имён Ambient
declare namespace "my-math" {
  function calculateCircumference(diameter: number): number;
}

// main.ts - Использование пространства имён Ambient
import * as MyMath from './my-math';
const circumference = MyMath.calculateCircumference(10);
```



#### Внешние модули

Внешние модули позволяют организовать и совместно использовать код в нескольких файлах.
Внешние модули в TypeScript соответствуют стандартам модулей CommonJS или ES.

```ts
// myModule.ts
export function doSomething() {
  console.log(" Doing something...");
}

// main.ts
import { doSomething } from "./myModule";
doSomething(); // Вывод: "Doing something..."
```



#### Расширение пространства имён

Расширение пространства имён - это способ расширения или модификации существующих пространств имён. Это полезно, когда вы хотите добавить новую функциональность в существующие пространства имён или исправить недостающие или неправильные объявления в сторонних библиотеках

```ts
// myModule.d.ts
declare namespace MyModule {
  export interface MyModule {
    newFunction(): void;
  }
}

// main.ts
/// <reference path="myModule.d.ts" />
namespace MyModule {
  export class MyModule {
    public newFunction() {
      console.log(" I am a new function in MyModule!");
    }
  }
}

const obj = new MyModule.MyModule();
obj.newFunction(); // Вывод: " I am a new function in MyModule!".
```



#### Глобальное расширение

Глобальная аугментация - это способ добавления объявлений в глобальную область видимости.
Это полезно, когда вы хотите добавить новую функциональность в существующие библиотеки или дополнить встроенные типы в TypeScript.

```ts
// myModule.d.ts
declare namespace NodeJS {
  interface Global {
    myGlobalFunction(): void;
  }
}

// main.ts
global.myGlobalFunction = function () {
  console.log(" I am a global function!");
};

myGlobalFunction(); // Вывод: " I am a global function!"
```



## Комментарии для компилятора

Отключение проверки файла:

```ts
// @ts-nocheck
```

Включение проверки файла:

```ts
// @ts-check
```

Игнорирование следующей строки:

```ts
// @ts-ignore
```

Ожидание ошибки на следующей строке:

```ts
// @ts-expect-error
```
