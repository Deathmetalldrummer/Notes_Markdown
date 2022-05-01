# Gulp
![gulp](./img/gulp.png)

## Установка

0. Установить Gulp глобально:
    ```
    $ npm install --global gulp
    ```

0.  Создать файл package.json:
    ```
    $ npm init
    ```

0. Установить Gulp для проекта (локально):
    ```
    $ npm install --save-dev gulp
    ```

0. Создать gulpfile.js для настройки задач:
    ```
    $ touch gulpfile.js
    ```

<br />
<br />

## Фантастическая четверка

0. Определяет задачу
    ```JavaScript
    gulp.task();
    ```

0. Указывает на файлы,которые хотим использовать
    ```JavaScript
    gulp.src();
    ```

0. Указывает папку для сохранения измененных файлов
    ```JavaScript
    gulp.dest();
    ```

0. Следит за изменениями файлов
    ```JavaScript
    gulp.watch()
    ```

<br />
<br />

## Синтаксис
0. Вызываем Gulp и записываем в переменную:
    ```JavaScript
    var gulp = require('gulp');
    ```

0. Создаем задачу:
    ```JavaScript
    gulp.task('default', function(){
    });
    ```

0. Возвращаем результат:
    ```JavaScript
    return console.log('Hello World!');
    ```


```JavaScript
var gulp = require('gulp');

gulp.task('default', function(){
    return console.log('Hello World!');
});
```

<br />

```JavaScript
// Вызываем Gulp и записываем в переменную:
var gulp = require('gulp');
//  Вызываем плагин minify-css и записываем в переменную:
var minifyCSS = require('gulp-minify-css');

// Создаем задачу 'miniCss’ :
gulp.task('miniCss', function(){
    // Получаем файлы по указанному пути:
    gulp.src('css/*.css')
    // Фильтруем данные через плагин:
    .pipe(minifyCss())
    // Записываем результат в папку:
    .pipe(gulp.dest('css'));
});
```
Вызываем задачу из терминала:
```
$ gulp miniCss
```

`.pipe()` - Поток (очередь) позволяет передать некоторые данные последовательно от одной функции к другой, каждая из которых выполняет некоторые действия с этими данными.

<br />
<br />

## Watch docs

0. Создаем задачу  watcher :
    ```JavaScript
    gulp.task('watcher', function(){});
    ```

0. Следим за файлами в папке Css и при их изменении выполняем задачу miniCss :
    ```JavaScript
    gulp.watch('css/*.*',['mimiCss']);
    ```

<br />

```JavaScript
gulp.task('watcher', function() {
    gulp.watch('css/*.*',['mimiCss']);
});
```

<br />
<br />

## Плагины

* __bower__ - пакетный менеджер
* __browser-sync__ - живая перезагрузка
* __gulp__ - менеджер задач
* __del__ - очищает путь и файлы (удаляет)
* __gulp-autoprefixer__ - расставляет css префиксы исходя из статистики caniuse
* __gulp-jade__ - поддержка jade шаблонизатора(или препроцессора)
* __gulp-sass__ - поддержка sass препроцессора
* __gulp-plumber__ - обработчик ошибок без выкидышей
* __gulp-rename__ - переименовывает файлы
* __gulp-sourcemaps__
* __gulp-uncss__ - Удаление неиспользуемого CSS
* __gulp-concat__ - объединяет js файлы
* __gulp-uglify__ - сжимает (минифицирует) js файлы
* __gulp-clean-css__ или __clean-css__ минификатор css
* __gulp-svgmin__ - минификация SVG изображений
* __gulp-imagemin__ - минификация изображений
* __gulp.spritesmith__ - спрайты
* __run-sequence__ - серия задач

[BlackList](https://github.com/gulpjs/plugins/blob/master/src/blackList.json)
