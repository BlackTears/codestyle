# JavaScript сode style


----------

### Компиляция и Развертывание

Для контроля стиля, тестирования и сжатия кода использовать [grunt](https://github.com/cowboy/grunt) от Ben Alman.

----------
### Содержание

- [Пробелы, табуляция и пустые строки](#whitespace)
- [Красивый синтаксис](#spacing)
- [Проверка типов (Руководство по стилю от команды jQuery Core)](#type)
- [Условное Вычисление](#cond)
- [Практичный стиль](#practical)
- [Именование](#naming)
- [Разное](#misc)
- [«Родные» и «чужие» объекты](#native)
- [Комментарии](#comments)
- [Код одного языка](#language)

----------
### Основы
1. <a name="whitespace">Пробелы, табуляция и пустые строки</a>
 - Никогда не мешать пробел и знак табуляции.
 - Всегда работать с включенной опцией «показать скрытое», если редактор поддерживает ее. Преимущества:
        - удаление пробела в конце строки
        - удаление пустых строк
        - читабельные коммиты и диффы

2. <a name="spacing">Красивый Синтаксис</a>

    ```javascript


	// if/else/for/while/try всегда разделяются пробелом,
	// это улучшает читабельность
	
	// 2.A.1.1
	// Использовать пробелы для того, чтобы улучшить читабельность
	
	while ( condition ) {
	  // выражения
	}
	
	for ( var i = 0; i < 100; i++ ) {
	  // выражения
	}
	
	// Еще лучше:
	var i,
	  length = 100;
	
	for ( i = 0; i < length; i++ ) {
	  // выражения
	}
	
	var prop;
	
	for ( prop in object ) {
	  // выражения
	}
	
	
	if ( true ) {
	  // выражения
	} else {
	  // выражения
	}
    
    ```



    B. Присваивание, Объявление, Функции (Именованные, Функции-Выражения, Функции-Конструкторы)

    ```javascript

    // 2.B.1.1
    // Переменные
    var foo = "bar",
      num = 1,
      undef;

    // Объявление литералов:
    var array = [],
      object = {};


    // 2.B.1.2
    // Использование только одного `var` на одну область видимости улучшает читабельность
    // и упорядочивает блок объявления переменных (также сохраняет вам несколько нажатий клавиш)

    // Неправильно
    var foo = "";
    var bar = "";
    var qux;

    // Правильно
    var foo = "",
      bar = "",
      quux;

    // или...
    var // комментарий для переменных
    foo = "",
    bar = "",
    quux;

    // 2.B.1.3
    // Оператор var всегда должен быть в начале области видимости (функции).
    // То же самое верно для констант и оператора let из ECMAScript 6.

    // Неправильно
    function foo() {

      // выражения

      var bar = "",
        qux;
    }

    // Правильно
    function foo() {
      var bar = "",
        qux;

      // все выражения после объявления переменных.
    }
    ```

    ```javascript

    // 2.B.2.1
    // Объявление Именованных Функций
    function foo( arg1, argN ) {

    }

    // Использование
    foo( arg1, argN );


    // 2.B.2.2
    // Объявление Именованных Функций
    function square( number ) {
      return number * number;
    }

    // Использование
    square( 10 );

    // Очень надуманный стиль передачи параметров
    function square( number, callback ) {
      callback( number * number );
    }

    square( 10, function( square ) {
      // обратный вызов
    });

    // 2.B.2.3
    // Функция-Выражение
    var square = function( number ) {
      // вернуть что-то ценное и важное
      return number * number;
    };

    // Функция-Выражение с Идентификатором
    // Такое объявление хорошо тем, что функция может вызвать сама себя
    // и ее имя будет видно в стеке вызова функций:
    var factorial = function factorial( number ) {
      if ( number < 2 ) {
        return 1;
      }

      return number * factorial( number-1 );
    };

    // 2.B.2.4
    // Объявление Конструктора
    function FooBar( options ) {

      this.options = options;
    }

    // Использование
    var fooBar = new FooBar({ a: "alpha" });

    fooBar.options;
    // { a: "alpha" }

    ```


    C. Исключения, Незначительные Отклонения от правил

    ```javascript

    // 2.C.1.1
    // Функции с обратным вызовом
    foo(function() {
      // Заметьте, что пробела между "function" и первой скобкой нет
    });

    // Функция, которая принимает массив как параметр, тоже без пробела
    foo([ "alpha", "beta" ]);

    // 2.C.1.2
    // Функция, которая принимает объект как параметр, тоже без пробела
    foo({
      a: "alpha",
      b: "beta"
    });

    // Одна строка, тоже без пробела
    foo("bar");

    // Внутренние скобки, тоже без пробела
    if ( !("foo" in obj) ) {

    }

    ```

    D. Консистентность Всегда Побеждает

    В секции 2.A-2.C, правила использования пробела и знака табуляции установлены с простой целью: консистентность.
    Очень важно отметить, что предпочтения в форматировании, такие как "внутренний пробел", должны считаться опциональными, но в вашем проекте должен использоваться только один стиль форматирования.

    ```javascript

    // 2.D.1.1

    if (condition) {
      // выражения
    }

    while (condition) {
      // выражения
    }

    for (var i = 0; i < 100; i++) {
      // выражения
    }

    if (true) {
      // выражения
    } else {
      // выражения
    }

    ```

    E. Кавычки

    Абсолютно неважно, какие кавычки вы используете (одинарные или двойные), нет никакой разницы в том, как JavaScript обрабатывает их. Что **действительно важно**, это сохранять консистентность. **Никогда не путайте кавычки в вашем проекте. Выберите один стиль и придерживайтесь его.**

    F. Конец строки и пустые строки

    Пробелы, знаки табуляции могут испортить диффы и сделать чэнджсеты непригодными для чтения. Подумайте о том, чтобы убирать пробелы в конце строк и пустые строки автоматически перед коммитом.

3. <a name="type">Проверка типов (Руководство по стилю от jQuery Core)</a>

    A. Типы

    String:

        typeof variable === "string"

    Number:

        typeof variable === "number"

    Boolean:

        typeof variable === "boolean"

    Object:

        typeof variable === "object"

    Array:

        Array.isArray( arrayLikeObject )
        (где возможно)

    Node:

        elem.nodeType === 1

    null:

        variable === null

    null or undefined:

        variable == null

    undefined:

      Глобальные переменные:

        typeof variable === "undefined"

      Локальные переменные:

        variable === undefined

      Свойства:

        object.prop === undefined
        object.hasOwnProperty( prop )
        "prop" in object

    B. Неявное приведение типов

    Представьте результат следующего...

    Пусть дан следующий HTML:

    ```html

    <input type="text" id="foo-input" value="1">

    ```


    ```js

    // 3.B.1.1

    // `foo` была объявлена, ей был присвоен `0` и ее тип `number`
    var foo = 0;

    // typeof foo;
    // "number"
    ...

    // Далее в коде вам нужно обновить значение `foo`
    // новым значением из input элемента

    foo = document.getElementById("foo-input").value;

    // Если бы вы проверили тип переменной сейчас `typeof foo`, то получили бы `string`
    // Это значит, что если бы вы тестировали `foo` вот так:

    if ( foo === 1 ) {

      importantTask();

    }

    // то `importantTask()` не была вызвана, даже если значение `foo` было бы "1"


    // 3.B.1.2

    // Вы можете избежать ошибок, используя приведение типов с помощью унарных операторов "+" и "-":

    foo = +document.getElementById("foo-input").value;
    //    ^ унарный оператор + приведет правую часть выражения к типу `number`

    // typeof foo;
    // "number"

    if ( foo === 1 ) {

      importantTask();

    }

    // `importantTask()` будет вызвана
    ```

    Вот несколько простых примеров приведения типов:


    ```javascript

    // 3.B.2.1

    var number = 1,
      string = "1",
      bool = false;

    number;
    // 1

    number + "";
    // "1"

    string;
    // "1"

    +string;
    // 1

    +string++;
    // 1

    string;
    // 2

    bool;
    // false

    +bool;
    // 0

    bool + "";
    // "false"
    ```


    ```javascript
    // 3.B.2.2

    var number = 1,
      string = "1",
      bool = true;

    string === number;
    // false

    string === number + "";
    // true

    +string === number;
    // true

    bool === number;
    // false

    +bool === number;
    // true

    bool === string;
    // false

    bool === !!string;
    // true
    ```

    ```javascript
    // 3.B.2.3

    var array = [ "a", "b", "c" ];

    !!~array.indexOf("a");
    // true

    !!~array.indexOf("b");
    // true

    !!~array.indexOf("c");
    // true

    !!~array.indexOf("d");
    // false

    // Заметьте, что вышеизложенное можно считать "черезчур умным"
    // Лучше делать так:

    if ( array.indexOf( "a" ) >= 0 ) {
      // ...
    }
    ```

    ```javascript
    // 3.B.2.3


    var num = 2.5;

    parseInt( num, 10 );

    // то же самое, что и ...

    ~~num;

    num >> 0;

    num >>> 0;

    // Во всех случаях результат равен 2


    // Помните, что отрицательные числа будут обработаны по-другому...

    var neg = -2.5;

    parseInt( neg, 10 );

    // тоже самое что...

    ~~neg;

    neg >> 0;

    // Во всех случаях результат равен -2
    // Хотя...

    neg >>> 0;

    // покажет 4294967294



    ```

----------
### Ссылки
- [idiomatic.js](https://github.com/rwldrn/idiomatic.js/blob/master/translations/ru_RU/readme.md "idiomatic.js")
- [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
- [JavaScript Style Guide (rashbrook.org)](http://neil.rashbrook.org/JS.htm)
- [ECMAScript 5.1 с комментариями](http://es5.github.com/)
- [Спецификация языка ECMAScript, издание 5.1](http://ecma-international.org/ecma-262/5.1/)
- [Baseline For Front End Developers](http://rmurphey.com/blog/2012/04/12/a-baseline-for-front-end-developers/)
- [Eloquent JavaScript](http://eloquentjavascript.net/)
- [JavaScript, JavaScript](http://javascriptweblog.wordpress.com/)
- [Adventures in JavaScript Development](http://rmurphey.com/)
- [Perfection Kills](http://perfectionkills.com/)
- [Douglas Crockford's Wrrrld Wide Web](http://www.crockford.com)
- [JS Assessment](https://github.com/rmurphey/js-assessment)