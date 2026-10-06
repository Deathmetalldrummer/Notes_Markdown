

## 1️⃣ **Module (модуль)**

- Основной строительный блок приложения.
    
- Инкапсулирует **сервисы, контроллеры, провайдеры и экспорты**.
    
- Может быть обычным или глобальным (`@Global()`).
    
- Пример: `UserModule`, `EventModule`.
    

**Структура:**

`@Module({   imports: [],      // другие модули   controllers: [],  // контроллеры   providers: [],    // сервисы, репозитории, провайдеры   exports: [],      // что можно использовать в других модулях }) export class UserModule {}`

---

## 2️⃣ **Controller (контроллер)**

- Отвечает за **HTTP/REST API, WebSocket, GraphQL**.
    
- Получает запросы, валидирует входные данные (через DTO) и вызывает сервисы.
    
- Не содержит бизнес-логики.
    

`@Controller('users') export class UserController {   constructor(private readonly userService: UserService) {}    @Get(':id')   getUser(@Param('id') id: string) {     return this.userService.findById(id);   } }`

---

## 3️⃣ **Service (сервис)**

- Основная бизнес-логика модуля.
    
- Вызывает репозитории, валидирует данные, применяет правила.
    
- Может использовать другие сервисы через DI.
    

`@Injectable() export class UserService {   constructor(private readonly userRepository: UserRepository) {}    findById(id: string) {     return this.userRepository.findById(id);   } }`

---

## 4️⃣ **Repository (репозиторий / data-access)**

- Работа с **источником данных** (MongoDB, Postgres, API и т.д.).
    
- CRUD операции, фильтры, агрегации.
    
- Не содержит бизнес-логики.
    

`@Injectable() export class UserRepository {   constructor(@Inject('DB') private readonly db: Db) {}    findById(id: string) {     return this.db.collection('users').findOne({ _id: new ObjectId(id) });   } }`

---

## 5️⃣ **Entity / Document / Model**

- Представляет **структуру данных в БД**.
    
- Может быть классом или интерфейсом.
    
- Используется в репозиториях и для валидации данных.
    
- Для MongoDB часто `EventDocument`, для Postgres — `UserEntity`.
    

`export interface UserEntity {   _id: ObjectId;   email: string;   name: string; }`

---

## 6️⃣ **DTO (Data Transfer Object)**

- Определяет **структуру входных/выходных данных**.
    
- Используется в контроллерах.
    
- Часто валидируется через `class-validator`.
    

`export class CreateUserDto {   @IsEmail()   email: string;    @IsString()   name: string; }`

---

## 7️⃣ **Domain Entity / Domain Model (опционально)**

- Слой **чистого домена / бизнес-логики**.
    
- Содержит методы, инварианты и бизнес-правила.
    
- Репозиторий только читает/пишет данные, сервис оперирует доменом.
    

`export class Event {   constructor(     public readonly id: string,     public readonly userId: string,     public readonly currentPoint: number,     public readonly skip: number,   ) {}    advancePoint() {     return new Event(this.id, this.userId, this.currentPoint + 1, 0);   } }`

---

## 8️⃣ **Optional / Infrastructure / Shared**

- **Guards** — авторизация/аутентификация.
    
- **Interceptors** — логирование, трансформация данных.
    
- **Pipes** — валидация/трансформация.
    
- **Filters** — обработка исключений.
    
- **Providers / Utils / Shared Services** — глобальные сервисы (например MongoModule).
    

---

## 🔑 Итог

|Сущность|Роль|
|---|---|
|Module|Организация кода, инкапсуляция|
|Controller|API слой, входящие запросы|
|Service|Бизнес-логика|
|Repository|Работа с БД / data source|
|Entity / Document|Структура данных в БД|
|DTO|Вход/выход данных, валидация|
|Domain Entity|Чистая бизнес-логика, инварианты|
|Guards / Interceptors / Pipes / Filters|Инфраструктурные вещи|

---

💡 **Правило:**

- **Сервис = бизнес**
    
- **Репозиторий = данные**
    
- **Контроллер = API**
    
- **DTO = валидированные входные данные**
    
- **Domain Entity = логика объекта**