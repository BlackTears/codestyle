# JavaScript сode style


----------

### Компиляция и Развертывание

Для контроля стиля, тестирования и сжатия кода использовать [grunt](https://github.com/cowboy/grunt) от Ben Alman.

----------
### Содержание

- [Пробелы, табуляция и пустые строки](#whitespace)
- [Именование](#naming)
- [Комментарии](#comments)
- [Красивый синтаксис](#spacing)
- [Проверка типов (Руководство по стилю от команды jQuery Core)](#type)
- [Условия](#cond)
- [Стиль в действии](#practical)

----------
### Основы
1. <a name="whitespace">Пробелы, табуляция и пустые строки</a>
 - Никогда не мешать пробел и знак табуляции.
 - Всегда работать с включенной опцией «показать скрытое», если редактор поддерживает ее. Преимущества:
        - удаление пробела в конце строки
        - удаление пустых строк
        - читабельные коммиты и диффы

2. <a name="comments">Комментарии</a>

	Комментирование строки
	```javascript
	\\
	```

	Все файлы и классы необходимо комментировать в стиле JSDoc
	```javascript
	/**
	 * Комментарий
	 */
	```

	Комментарий для класса
	```javascript
	/**
	 * Class making something fun and easy.
	 * @param {string} arg1 An argument that makes this more interesting.
	 * @param {Array.<number>} arg2 List of numbers to be processed.
	 */
	function SomeFunClass(arg1, arg2) {
	  // ...
	}
	

3. <a name="naming">Именование</a>

	```javascript
	// 3.1. Имена переменных
	
		ClassNamesLikeThis
		methodNamesLikeThis
		variableNamesLikeThis
		parameterNamesLikeThis
		propertyNamesLikeThis
		SYMBOLIC_CONSTANTS_LIKE_THIS

	// Переменные и свойства использующие jQuery — добавлять в имя префикс $
	/**
	 * @param {string} selector The jQuery selector for elements to apply 
	 *     fanciness to.
	 */
	function doSomethingFancy(selector) {
	  var $elements = $(selector);
	  // do something fancy with $elements ...
	}
	
	// 3.2 Имена файлов
	file-names-like-this.js
	template-names-like-this.handlebars
	

4. <a name="spacing">Красивый Синтаксис</a>

    ```javascript


	// if/else/for/while/try всегда разделяются пробелом,
	// это улучшает читабельность
	
	// 4.A.1.1
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

    // 4.B.1.1
    // Переменные
    var foo = "bar",
        num = 1,
        undef;

    // Объявление литералов:
    var array = [],
        object = {};


    // 4.B.1.2
    // Использование только одного `var` на одну область видимости улучшает читабельность
    // и упорядочивает блок объявления переменных

    // Неправильно
    var foo = "";
    var bar = "";
    var qux;

    // Правильно
    var foo = "",
        bar = "",
        quux;


    // 4.B.1.3
    // Оператор var всегда должен быть в начале области видимости (функции).
    // То же самое верно для констант и оператора let из ECMAScript 6.

    function foo() {
      var bar = "",
          qux;

      // все выражения после объявления переменных.
    }
    ```

    ```javascript

    // 4.B.2.1
    // Объявление Именованных Функций
    function foo( arg1, argN ) {

    }

    // Использование
    foo( arg1, argN );


    // 4.B.2.2
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

    // 4.B.2.3
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

    // 4.B.2.4
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

    // 4.C.1.1
    // Функции с обратным вызовом
    foo(function() {
      // Заметьте, что пробела между "function" и первой скобкой нет
    });

    // Функция, которая принимает массив как параметр, тоже без пробела
    foo([ "alpha", "beta" ]);

    // 4.C.1.2
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

    D. Кавычки

    Абсолютно неважно, какие кавычки используются (одинарные или двойные), нет никакой разницы в том, как JavaScript обрабатывает их. Что **действительно важно**, это сохранять единообразие. **Никогда не путайть кавычки в проекте. Выберать один стиль и придерживаться его.**

    E. Конец строки и пустые строки

    Пробелы, знаки табуляции могут испортить диффы и сделать чэнджсеты непригодными для чтения.

5. <a name="type">Проверка типов (Руководство по стилю от jQuery Core)</a>

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

    // 5.B.1.1

    // Можно избежать ошибок, используя приведение типов с помощью унарных операторов "+" и "-":

    foo = +document.getElementById("foo-input").value;
    //    ^ унарный оператор + приведет правую часть выражения к типу `number`

    // typeof foo;
    // "number"

    if ( foo === 1 ) {

      importantTask();

    }

    // `importantTask()` будет вызвана
    ```

    Несколько примеров приведения типов:


    ```javascript

    // 5.B.2.1

    var number = 1,
      string = "1",
      bool = false;

    number;
    // 1

    number + "";****
    // "1"

    string;
    // "1"

    +string;
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
    // 5.B.2.2

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
    // 5.B.2.3

    var array = [ "a", "b", "c" ];

    !!~array.indexOf("a");
    // true

    !!~array.indexOf("b");
    // true

    !!~array.indexOf("c");
    // true

    !!~array.indexOf("d");
    // false

    // Вышеизложенное можно считать "черезчур умным"
    // Лучше делать так:

    if ( array.indexOf( "a" ) >= 0 ) {
      // ...
    }
    ```

    ```javascript
    // 5.B.2.3


    var num = 2.5;

    parseInt( num, 10 );

    // то же самое, что и ...

    ~~num;


    // Во всех случаях результат равен 2


    // Отрицательные числа будут обработаны по-другому...

    var neg = -2.5;

    parseInt( neg, 10 );

    // тоже самое что...

    ~~neg;

    // Во всех случаях результат равен -2

    ```
    
6. <a name="cond">Условия</a>

    ```javascript

    // 6.1.1
    // Проверка длинны массива,
    if ( array.length ) ...


    // 6.1.2
    // Проверка, массива на пустоту:
    // вместо:
    if ( array.length === 0 ) ...

    // вот так:
    if ( !array.length ) ...


    // 6.1.3
    // Проверка, строки на пустоту:
    // вместо:
    if ( string !== "" ) ...

    // вот так:
    if ( string ) ...

    // вместо:
    if ( string === "" ) ...

    // проверять ложно ли выражение:
    if ( !string ) ...


    // 6.1.4
    // Проверка, переменной на истину,
    // вместо:
    if ( foo === true ) ...

    // вот так:
    if ( foo ) ...


    // 6.1.5
    // Проверка, переменной на ложь,
    // вместо:
    if ( foo === false ) ...

    // использовать отрицание:
    if ( !foo ) ...

    // ...Внимание: выражение справедливо и для: 0, "", null, undefined, NaN
    // Для проверки значения заведомо ложных выражений:
    if ( foo === false ) ...


    // 6.1.6
    // Проверка, если переменная null или undefined, но НЕ ложь, "" или 0,
    // вместо:
    if ( foo === null || foo === undefined ) ...

    // ...использовать оператор ==:
    if ( foo == null ) ...

    // Внимание: сравнение с помощью оператора == с `null` сработает для ОБОИХ `null` и `undefined`
    // но не для `false`, "" или 0
    null == undefined

    ```


    ```javascript

    // 6.2.1
    // Приведение типов и оценка выражений

    // Предпочтение `===`, а не `==` (только если конкретный случай не требует слабо типизированной оценки)

    // === не приводит типы принудительно, т.е.:

    "1" === 1;
    // false

    // == приводит типы принудительно, т.е.:

    "1" == 1;
    // true


    // 6.2.2
    // Логические выражения
    
    // Истинные:
    "foo", 1

    // Ложные:
    "", 0, null, undefined, NaN, void 0

    ```
    
7. <a name="practical">Стиль в действии</a>

    ```javascript

    // 7.1.1
    // Модуль

    (function( global ) {
      var Module = (function() {

        var data = "secret";

        return {
          // Логическое свойство
          bool: true,
          // Свойство типа строка
          string: "a string",
          // Свойство — массив
          array: [ 1, 2, 3, 4 ],
          // Свойство — объект
          object: {
            lang: "en-Us"
          },
          getData: function() {
            // получить текущее значение переменной `data`
            return data;
          },
          setData: function( value ) {
            // присвоить значение переменной `data` и вернуть его
            return ( data = value );
          }
        };
      })();

      // Другие объявления

      // делаем модуль глобальным
      global.Module = Module;

    })( this );

    ```

    ```javascript

    // 7.2.1
    // Конструктор

    (function( global ) {

      function Ctor( foo ) {

        this.foo = foo;

        return this;
      }

      Ctor.prototype.getFoo = function() {
        return this.foo;
      };

      Ctor.prototype.setFoo = function( val ) {
        return ( this.foo = val );
      };


      // Чтобы вызывать конструктор без использования оператора `new`, можно объявить конструктор так:
      var ctor = function( foo ) {
        return new Ctor( foo );
      };


      // делаем наш конструктор глобальным
      global.ctor = ctor;

    })( this );

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