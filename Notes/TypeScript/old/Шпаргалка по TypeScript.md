## Типы примитивов

```ts
// Примитивные типы являются строительными блоками всех остальных типов.
//
// В TypeScript есть 6 примитивных типов:
// > boolean: true или false
// > number: числа с плавающей запятой
// > string: текст
// > void: отсутствие значения
// > null: нулевое значение
// > undefined: неопределённое значение
//
let flag: boolean = true;
let num: number = 123;
let str: string = 'Hello, TypeScript!';
let undefValue: undefined = undefined;
let nullValue: null = null;

// Пример типа Void
function logMessage(message: string): void {
  console.log(message);
}
```

## Типы объектов

```ts
// Вот список различных типов объектов в TypeScript:
// > Interface: Описывает свойства и типы объекта.
// > Class: Описывает свойства, типы и поведение объекта.
// > Enum: перечисление именованных значений
// > Array: список значений
// > Tuple: массив фиксированной длины

// Интерфейс
// ----------------------------
// Определяет структуру объекта
interface User {
  name: string;
  age: number;
}

// Объявляем класс, реализующий интерфейс User
class Person implements User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

// Массивы
// ----------------------------
// Как и в других языках, массив - это список значений.
let numbers: number[] = [1, 2, 3, 4, 5];

// Кортеж
// ----------------------------
// Кортеж/Tuple - массив фиксированной длины. Он полезен, когда вы знаете точное количество элементов в массиве.
let tuple: [string, number] = ['Hello', 42];
```

## Типы перечислений

```ts
// Перечисления - это способ дать более дружественные имена наборам числовых значений.
// По умолчанию перечисления начинают нумеровать своих членов, начиная с 0.
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

// Перечисление с пользовательскими значениями
// ----------------------------
// Вы также можете установить значение каждого члена перечисления.
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

// Перечисление со строковыми значениями
// ----------------------------
// Объявляем перечисление со строковыми значениями
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

```ts
// Другие типы:
// > any: любой тип
// > unknown: неизвестный тип
// > never: never тип
// > object: объектный тип

// Any
// ----------------------------
// any - это тип, который позволяет присваивать переменной значения любого типа.
let data: any = 'Hello';
data = 42;
data = true;

// Обеспечивает ввод массива, но значения массива могут быть любого типа.
// Также не ограничивает никаких типов на возврате
function untypedFunction(inputs: any[]): any {
  // Реализация функции
}

// Object
// ----------------------------
// object - это тип, который представляет не примитивный тип, т.е. все, что не является
// number, string, boolean, symbol, null или undefined.
function logObject(obj: object): void {
  console.log(obj);
}

logObject({ greeting: 'Hello, TypeScript!' });

// Unknown
// ----------------------------
// unknown является типобезопасным аналогом any - это означает, что мы можем присвоить
// ему любое значение, но мы не можем получить доступ к его свойствам, если только не
// сузим его до более конкретного типа.
let unknownValue: unknown = 42;
console.log(unknownValue * 2); // Error: Оператор '*' не может быть применён к типам 'unknown' и '2'.

// Вы должны принудительно определить тип, прежде чем использовать его
if (typeof unknownValue === 'number') {
    console.log(unknownValue * 2); // Вывод: 84
}

// Never
// ----------------------------
// never - это тип, который представляет собой тип значений, которые никогда не встречаются.
// Например, never - это тип возврата для выражения функции или выражение стрелочной функции,
// которое всегда выбрасывает исключение или которое ничего не возвращает.
function throwError(message: string): never {
  throw new Error(message);
}
```

## Утверждение типа `as`

```ts
// Утверждение типа - это способ сообщить компилятору, что вы лучше него знаете тип переменной.

// Утверждение типа с синтаксисом угловых скобок
let someValue: any = 'This is a string';
let strLength: number = (someValue as string).length;
console.log(strLength); // Вывод: 16

// как const
// ----------------------------
// Утверждение `as const` используется, чтобы сообщить компилятору, что значение является константой.
const colors = ['red', 'green', 'blue'] as const;
// colors теперь имеет тип readonly ['red', 'green', 'blue'].
colors[0] = 'yellow'; // Error: Cannot assign to '0' because it is a read-only property

// Обход проверки типов TypeScript с помощью `as` и `any`
let obj: unknown = { key: 'value' };
let bypassTypeCheck = (obj as any).key;
```

## Оператор утверждения Non-Null

```ts
// Оператор утверждения Non-null (!) используется, чтобы сообщить компилятору,
// что значение не является нулевым или неопределённым.

// Объявление переменной с возможным нулевым значением
let possibleNullValue: string | null = 'TypeScript';

console.log(possibleNullValue.length); // Error: Object is possibly 'null'
console.log(possibleNullValue!.length); // Вывод: 10
```

## Ключевое слово `satisfies`

```ts
// Ключевое слово `satisfies используется для проверки того, удовлетворяет ли
// тип заданному ограничению.
// Без ключевого слова satisfies нам пришлось бы использовать утверждения типов,
// чтобы проверить, удовлетворяет ли тип заданному ограничению.

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

```ts
// Компилятор TypeScript может определить тип переменной по её значению.

// Объявление переменной с предполагаемым типом
// Компилятор TypeScript примет тип переменной за строку
let inferredValue = 'TypeScript';
console.log(inferredValue); // Вывод: "TypeScript"
```

## Совместимость типов

```ts
// TypeScript использует структурную типизацию для определения совместимости типов.
// Это означает, что два типа считаются совместимыми, если они имеют одинаковую структуру,
// независимо от их имён.
interface Point {
  x: number;
  y: number;
}

let p1: Point = { x: 10, y: 20 }
// Даже если p2 имеет другое имя, он все равно совместим с p1
let p2: { x: number; y: number } = p1;

console.log(p2.x); // Вывод: 10
```

## Объединение типов

```ts
// Объединение типов используется для представления значения,
// которое может быть одним из нескольких типов.

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

```ts
// Пересечение типов используется для объединения нескольких типов в один.

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

```ts
// Псевдонимы типов используются для создания нового имени для типа.

// Объявление псевдонима типа
type Name = string;
type Age = число;
type User = { name: Name; age: Age };

const user: User = { name: 'John', age: 30 };
```

## Оператор `keyof`

```ts
// Оператор `keyof` используется для получения ключей объекта.

interface User {
  name: string;
  age: число;
  location: string;
}

type UserKeys = keyof User; // " name" | "age" | "location"
const key: UserKeys = 'name';
```

## Защита типов с помощью `typeof`

```ts
// Защита типа typeof используется для сужения типа переменной на основе её значения.

let value: string | number = 'hello';

// Защита типа с использованием typeof
if (typeof value === 'string') {
  console.log('value is a string');
} else {
  console.log('value is a number');
}
```

## Защита типа с помощью instanceof

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

## Защита типа с помощью равенства

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

## Защита типа с использованием истинности

```ts
function getUsersOnlineMessage(numUsersOnline: number) {
  if (numUsersOnline) {
    return `There are ${numUsersOnline} online now!`;
  }

  return "Nobody's here. :(";
}
```

## Функции

```ts
// Типы функций используются для описания структуры функции.

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
```

## Перегрузка функций

```ts
// Перегрузки функций используются для описания нескольких сигнатур функции.
function add(a: number, b: number): number;
function add(a: string, b: string): string;

// Помните, что существует только одна реализация функции.
// Перегрузки используются только для описания сигнатуры функции.
function add(a: any, b: any): any {
  return a + b;
}

console.log(add(1, 2)); // 3
console.log(add('Hello', ' World')); // "Hello World"
```

## Интерфейсы

```ts
// Интерфейсы используются для описания структуры объекта.
interface User {
  name: string;
  age: number;
}
const user: User = { name: 'John Doe', age: 30 };

// Типы по сравнению с интерфейсами
// -------------------
// Типы используются для создания нового именованного типа на основе существующего
// типа или для объединения существующих типов в новый тип. Они могут быть созданы
// с помощью ключевого слова type. Например:
type Person = { name: string; age: number };
const person: Person = { name: 'John Doe', age: 30 };

// Интерфейсы, с другой стороны, используются для описания структуры объектов и классов.
// Они могут быть созданы с помощью ключевого слова interface. Например:
interface Person {
  name: string;
  age: number;
}
const person: Person = { name: 'John Doe', age: 30 }

// Основное различие между типами и интерфейсами заключается в том, что типы можно
// использовать для создания новых типов на основе существующих, в то время как
// интерфейсы могут использоваться только для описания структуры объектов и классов.
// Также интерфейсы можно расширять с помощью ключевого слова extends, а типы -
// с помощью оператора &.

// Расширение интерфейсов
// -------------------
// Создайте новый интерфейс, который наследуется от исходного интерфейса с помощью
// ключевого слова "extends"
interface Shape {
  width: number;
  height: number;
}
interface Square extends Shape {
  sideLength: number;
}

let square: Square = { width: 10, height: 10, sideLength: 10 };

// Гибридные типы
// -------------------
// Гибридные типы - это типы, которые сочетают в себе особенности двух или более типов.
// Например, гибридный тип может быть объектом, который имеет и свойства, и методы,
// или массивом, который имеет и числа, и строки.
type Education = { degree: string; school: string; year: number };
type User = { name: string; age: number; email: string; education: Education };
```

## Классы

```ts
// Классы используются для создания объектов, которые имеют как данные, так и функциональность.
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

// Параметры конструктора
// -------------------
// Параметры конструктора могут быть объявлены как public, private или protected.
class Example {
  // Public (по умолчанию) свойства доступны из любого места.
  // Private свойства доступны только изнутри класса
  // Protected свойства доступны только в пределах класса и его подклассов
  // Примечание: TypeScript автоматически создаёт свойства для параметров конструктора,
  // которые объявлены как public или protected.
  constructor(private name: string, public age: number) {}
}

// Перегрузки конструктора
// -------------------
// Перегрузки конструкторов используются для создания нескольких конструкторов для класса.
class Point {
  // Перегрузки
  constructor(x: number, y: string);
  constructor(s: string);
  constructor(xs: any, y: any) {
    // Примечание: у нас есть только одна реализация конструктора.
    // Перегрузки используются только для определения типов параметров
  }
}

// Абстрактные классы
// -------------------
// Абстрактные классы используются для создания базовых классов, от которых могут быть
// получены другие классы.
// Абстрактные классы нельзя создавать напрямую. Вы можете создавать только экземпляры
// производных классов.
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

// Переопределение методов
// -------------------
// Механизм, с помощью которого подкласс переопределяет метод суперкласса.
class Animal {
  move(distanceInMeters: number = 0) {
    console.log(`Animal moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  move(distanceInMeters = 5) {
    console.log('Galloping...');
    super.move(distanceInMeters);
  }
}
```

## Дженерики

```ts
// Дженерики используются для создания многократно используемых компонентов,
// которые могут работать с различными типами, а не с одним.
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>('Hello'); // Тип вывода будет 'string'

// Общие типы
// -------------------
// Общие типы также могут быть использованы с классами, интерфейсами,
// объектными типами и псевдонимами типов.
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();

myGenericNumber.zeroValue = 0;
myGenericNumber.add = function (x, y) {
  return x + y;
};

// Ограничения дженерика
// -------------------
// Ограничения дженерика используются для обеспечения того, чтобы параметр
// типа был ограничен определённым типом или набором типов.
// Например, мы можем использовать ключевое слово `extends`, чтобы ограничить
// параметр типа типом, который является производным от определённого типа.
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

## Декораторы

```ts
// Декораторы используются для изменения поведения класса, метода, свойства или параметра.
// Это способ добавить дополнительную функциональность в существующий код, и они могут
// использоваться для широкого круга задач, включая ведение журнала, оптимизацию
// производительности и валидацию.
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

```ts
// Утилитарные типы - это типы, которые обеспечивают полезные сокращения при работе
// с другими типами.

// Partial
// -------------------
// Тип Partial используется для создания нового типа из существующего типа, в котором
// все свойства являются необязательными.
interface Person {
  name: string;
  age: number;
}

// toUpdate имеет тип Partial<Person>, то есть будет обладать некоторыми свойствами Person
function updatePerson(person: Person, toUpdate: Partial<Person>): Person {
  return { ...person, ...toUpdate }
}

// Pick
// -------------------
// Тип Pick используется для создания нового типа из существующего типа путём выбора
// набора свойств.
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

// Omit
// -------------------
// Тип Omit используется для создания нового типа из существующего путём исключения
// набора свойств.
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

// Readonly
// -------------------
// Тип Readonly используется для создания нового типа из существующего, где все
// свойства становятся доступными для чтения.
interface Todo {
  title: string;
}

const todo: Readonly<Todo> = {
  title: 'Delete inactive users',
};

// Невозможно присвоить 'title', потому что это свойство только для чтения.
todo.title = 'Hello';

// Record
// -------------------
// Вы можете использовать его для создания типа, в котором ключ имеет определённый
// тип, а значение - другой тип.
тип Cats = Record<
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

// Exclude
// -------------------
// Тип Exclude используется для создания нового типа путём исключения набора свойств
// из существующего типа.
type T0 = Exclude<'a' | 'b' | 'c', 'a'>; // "b" | "c"
type T1 = Exclude<'a' | 'b' | 'c', 'a' | 'b'>; // "c"
type T2 = Exclude<string | number | (() => void), Function>; // string | number

// Extract
// -------------------
// Тип Extract используется для создания нового типа путём извлечения набора свойств
// из существующего типа.
type T0 = Extract<'a' | 'b' | 'c', 'a' | 'f'>; // "a"
type T1 = Extract<string | number | (() => void), Function>; // () => void
type T2 = Extract<string | number | (() => void), Function | string>; // string | (() => void)

// NonNullable
// -------------------
// Тип NonNullable используется для создания нового типа путём исключения null и
// undefined из существующего типа.
type T0 = NonNullable<string | number | undefined>; // string | number
type T1 = NonNullable<string[] | null | undefined>; // string[]

// Parameters
// -------------------
// Тип Parameters используется для создания нового типа из типа функции путём
// извлечения типов её параметров.
type T0 = Parameters<() => string>; // []
type T1 = Parameters<(s: string) => void>; // [string]
type T2 = Parameters<<T>(arg: T) => T>; // [unknown]
type T3 = Parameters<<T extends U, U extends number[]>() => T>; // []
type T4 = Parameters<typeof Object.create>; // [object | null]

// ReturnType
// -------------------
// Тип ReturnType используется для создания нового типа из типа функции путём
// извлечения её возвращаемого типа.
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

// InstanceType
// -------------------
// Этот тип конструирует тип, состоящий из типа экземпляра функции-конструктора в Type.
class C {
  x = 0;
  y = 0;
}

type T0 = InstanceType<typeof C>; // C
type T1 = InstanceType<any>; // any
type T2 = InstanceType<never>; // any
type T3 = InstanceType<string>; // Error
type T4 = InstanceType<Function>; // Error

// Awaited
// -------------------
// Создаёт тип, который является ожидаемым аналогом заданного типа.
type T0 = Awaited<Promise<string>>; // string
type T1 = Awaited<Promise<string> | Promise<number>>; // string | number
type T2 = Awaited<Promise<string | number>>; // string | number
type T3 = Awaited<Promise<Promise<string>>; // string
type T4 = Awaited<Promise<Promise<string> | Promise<number>>; // string | number
```

## Пространства имён

```ts
// Пространства имён используются для организации кода в логические группы и для
// обеспечения способа обработки коллизий имён.
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

// Пространства имён Ambient
// -------------------
// Модули Ambient в TypeScript используются для объявления внешних модулей или
// сторонних библиотек в программе на TypeScript.
// Модули Ambient предоставляют информацию о типе для модулей, которые не имеют
// объявлений в TypeScript, но доступны в глобальной области видимости.
// myMath.d.ts - объявление пространства имён Ambient
declare namespace "my-math" {
  function calculateCircumference(diameter: number): number;
}

// main.ts - Использование пространства имён Ambient
import * as MyMath from './my-math';
const circumference = MyMath.calculateCircumference(10);

// Внешние модули
// ----------------
// Внешние модули позволяют организовать и совместно использовать код в нескольких файлах.
// Внешние модули в TypeScript соответствуют стандартам модулей CommonJS или ES.

// myModule.ts
export function doSomething() {
  console.log(" Doing something...");
}

// main.ts
import { doSomething } from "./myModule";
doSomething(); // Вывод: "Doing something..."

// Расширение пространства имён
// ----------------------
// Расширение пространства имён - это способ расширения или модификации существующих
// пространств имён.
// Это полезно, когда вы хотите добавить новую функциональность в существующие
// пространства имён или исправить недостающие или неправильные объявления в сторонних
// библиотеках.
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

// Глобальное расширение
// -------------------
// Глобальная аугментация - это способ добавления объявлений в глобальную область видимости.
// Это полезно, когда вы хотите добавить новую функциональность в существующие
// библиотеки или дополнить встроенные типы в TypeScript.

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