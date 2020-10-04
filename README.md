# VBestPracticeGuide
  ---
  ##### *10 лучших практик JavaScript*
  ---
  ##### [1. Объекты и Массивы](#1)
  ##### [2. Функции](#2)
  ##### [3. Классы и конструкторы](#3)
  ##### [4. Свойства](#4)
  ##### [5. Использование унарных инкрементов и декрементов](#5)
  ##### [6. Использование === и !==](#6)
  ##### [7. Блоки](#7)
  ##### [8. Управляющие операторы](#8)
  ##### [9. Комментарии](#9)
  ##### [10. Соглашение об именовании](#10)

 
   ### <a name="1">Объекты и массивы</a>
  ---
  Для создания объекта или массива используйте литеральную нотацию.

 ``` js
 // Bad
 const item = new Object();
 const items = new Array();

 // Good
 const item = {};
 const items = [];
 ```
   
   ### <a name="2">Функции</a>
  ---
  Используйте функциональные выражения вместо объявлений функций.

 ``` js
 // Bad
 function foo() {
   // ...
 }

 const foo = function () {
   // ...
 };

 // Good
 const foo = function uniqueMoreDescriptiveLexicalFoo() {
   // ...
 };
 ```

   ### <a name="3">Классы и конструкторы</a>
  ---
  Всегда используйте class. Избегайте прямых манипуляций с prototype

 ``` js
 // Bad
 function Queue(contents = []) {
   this.queue = [...contents];
 }
 Queue.prototype.pop = function () {
   const value = this.queue[0];
   this.queue.splice(0, 1);
   return value;
 };

 // Good
 class Queue {
   constructor(contents = []) {
     this.queue = [...contents];
   }
   pop() {
     const value = this.queue[0];
     this.queue.splice(0, 1);
     return value;
   }
 }
 ```

  ### <a name="4">Свойства</a>
  ---
  Используйте точечную нотацию для доступа к свойствам.

 ``` js
 const Alex = {
   jedi: true,
   age: 28,
 };

 // Bad
 const isFriend = Alex['friend'];

 // Good
 const isFriend = Alex.friend;
 ```

  ### <a name="5"> Использование унарных инкрементов и декрементов</a>
  ---
  Избегайте использования унарных инкрементов и декрементов (++, --)
 Согласно документации, унарные инкремент и декремент автоматически вставляют точку с запятой, что может стать причиной трудноуловимых ошибок при инкрементировании и декрементировании значений. Также нагляднее изменять ваши значения таким образом num += 1 вместо num++ или num ++.
 
 ``` js
 // Bad
 const array = [1, 2, 3];
 let num = 1;
 num++;
 --num;

 let sum = 0;
 let truthyCount = 0;
 for (let i = 0; i < array.length; i++) {
   let value = array[i];
   sum += value;
   if (value) {
     truthyCount++;
   }
 }

 // Good
 const array = [1, 2, 3];
 let num = 1;
 num += 1;
 num -= 1;

 const sum = array.reduce((a, b) => a + b, 0);
 const truthyCount = array.filter(Boolean).length;
 ```

  ### <a name="6"> Использование === и !== </a>
  ---
  Используйте === и !== вместо == и !=. Используйте сокращения для булевских типов, а для строк и чисел применяйте явное сравнение.

 ``` js
 // Bad
 if (isValid === true) {
   // ...
 }

 if (name) {
   // ...
 }

 if (collection.length) {
   // ...
 }

 // Good
 if (isValid) {
   // ...
 }

 if (name !== '') {
   // ...
 }

 if (collection.length > 0) {
   // ...
 }
 ```
  
  ### <a name="7">Блоки</a>
  ---
  Используйте фигурные скобки, когда блок кода занимает несколько строк.

 ``` js
 // Bad
 if (test)
   return false;

 function foo() { return false; }

 // Good
 if (test) return false;

 if (test) {
   return false;
 }
 ```

  ### <a name="8"> Управляющие операторы </a>
  ---
   Если ваш управляющий оператор (if, while и т.д.) слишком длинный или превышает максимальную длину строки, то каждое (сгруппированное) условие можно поместить на новую строку. Логический оператор должен располагаться в начале строки.

 ``` js
 // Bad
 if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
   thing1();
 }

 if (foo === 123 &&
   bar === 'abc') {
   thing1();
 }

 if (foo === 123
   && bar === 'abc') {
   thing1();
 }

 if (
   foo === 123 &&
   bar === 'abc'
 ) {
   thing1();
 }

 // Good
 if (
   foo === 123
   && bar === 'abc'
 ) {
   thing1();
 }

 if (
   (foo === 123 || bar === 'abc')
   && doesItLookGoodWhenItBecomesThatLong()
   && isThisReallyHappening()
 ) {
   thing1();
 }

 if (foo === 123 && bar === 'abc') {
   thing1();
 }
 ```
   
  ### <a name="9">Комментарии</a>
  ---
 Используйте конструкцию /** ... */ для многострочных комментариев.

 ``` js
 // Bad

 // make() возвращает новый элемент
 // соответствующий переданному названию тега
 //
 // @param {String} tag
 // @return {Element} element
 function make(tag) {

   // ...

   return element;
 }

 // Good

 /**
  * make() возвращает новый элемент
  * соответствующий переданному названию тега
  */
 function make(tag) {

   // ...

   return element;
 }
 ```
   
  Используйте двойной слеш // для однострочных комментариев. Располагайте такие комментарии отдельной строкой над кодом, который хотите пояснить. Если комментарий не является первой строкой блока, добавьте сверху пустую строку.

 ``` js
 // Bad

 const active = true;  // это текущая вкладка

 function getType() {
   console.log('fetching type...');
   // установить по умолчанию тип 'no type'
   const type = this.type || 'no type';

   return type;
 }

 // Good

 // это текущая вкладка
 const active = true;

 / хорошо
 function getType() {
   console.log('fetching type...');

   // установить по умолчанию тип 'no type'
   const type = this.type || 'no type';

   return type;
 }
 ```

  Начинайте все комментарии с пробела, так их проще читать.

 ``` js
 // Bad

 //это текущая вкладка
 const active = true;

 // Good

 // это текущая вкладка
 const active = true;
 ```

  ### <a name="10">Соглашение об именовании</a>
  ---
  Избегайте названий из одной буквы. Имя должно быть наглядным.

 ``` js
 // Bad
 function q() {
   // ...
 }

 // Good
 function query() {
   // ...
 }
 ```

  Используйте camelCase для именования объектов, функций и экземпляров. 

 ``` js
 // Bad
 const OBJEcttsssss = {};
 const this_is_my_object = {};
 function c() {}

 // Good
 const thisIsMyObject = {};
 function thisIsMyFunction() {}
 ```
  Используйте PascalCase только для именования конструкторов и классов.
 
 ``` js
 // Bad
 function user(options) {
   this.name = options.name;
 }

 const bad = new user({
   name: 'nope',
 });

 // Good
 class User {
   constructor(options) {
     this.name = options.name;
   }
 }

 const good = new User({
   name: 'yup',
 });
 ```
  
  ## May the JS be with you

 ![Stormtroopocat](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")
