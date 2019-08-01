# typescript-theory

## Введение в TypeScript

### Что такое TypeScript

TypeScript представляет язык программирования на основе JavaScript.

Следует отметить, что TypeScript - это строго типизированный и компилируемый язык. Хотя на выходе компилятор создает все
тот же JavaScript, который затем исполняется браузером. Однако строгая типизация уменьшает количество потенциальных
ошибок, которые могли бы возникнуть при разработке на JavaScript.

Так же TypeScript реализует многие концепции, которые свойственны объектно-ориентированным языкам, как, например, наследование,
полиморфизм, инкапсуляция и модификаторы доступа и так далее.

Потенциал TypeScripta позволяет быстрее и проще писать большие и сложные комплексные программы, соответственно их легче
поддерживать, развивать, масштабировать и тестировать, чем на стандартном JavaScript.

TypeScript является надмножеством JavaScript, а это значит, что любая прогррама на JS является программой на TypeScript.
В TS можно использовать все те конструкции, которые применяются в JS - те же операторы, условные, циклические конструкции.
Более того код на TS компилируется в JS. В конечно счете, TS - это всего лишь инструмент, который призван облегчить
разработку приложений.


## Основы TypeScript

### Переменные и константы

Для хранения данных в программе в TypeScript, как и во многих языках программирования использются переменные.

Для определения переменных, как в JS, можно использовать ключевое слово var:

```typescript
var z; // переменная z
```

Другой способ определения переменной применяет ключевое слово let, которое было добавлено в JS в стандарте ES 2015:

```typescript
let z;
``` 

Применение let является более предпочтительным, поскольку позволяет избежать ряд проблем, связанных с объявлением переменных.
В частности, с помощью var мы можем определить два и более раз переменную с одним и тем же именем:

```typescript
var x = 'Hello';
console.log(x);
var x = 'work';
console.log(x);
```

Если программа большая, то мы можем не уследить за тем, что такая переменная уже объявлена, что является источником потенциальных
ошибок. Подобную проблему позвляет решить let:

```typescript
let x = "Hello";
console.log(x);
let x = "work"; // здесь будет ошибка, так как переменная x уже объявлена
console.log(x);
``` 

Хотя var по прежнему можно использовать.

Определив переменную, мы можем установить ее значение и в процессе работы программы поменять его на другое:

```typescript
let z = 6;
z = 8;
```

Кроме переменных в TS имеются константы - для них можно установить значение только один раз. И даллее в процессе работы
программы мы уже не сможем изменить это значение. Для определение констант используется ключевое слово const:

```typescript
const z = 6;
z = 8; // Здесь ошибка - нельзя изменить значение константы z
```

<table>
    <thead>
          <tr>
              <td>var</td>
              <td>let/const</td>
          </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p>
                    Доступна в любой части функции, в которой она определена
                </p>
                <pre>
function print(){
    if(1) {
        var x = 94;
    }
    console.log(x); // норм
}
                </pre>
            </td>
            <td>
                <p>
                    Доступна в рамках блока, в котором она определена
                </p>
                <pre>
function print(){
 if(1) {
     let x = 94;
 }
 console.log(x); // ! Ошибка
}
                </pre>
            </td>
         </tr>
         <tr>
            <td>
                <p>
                    Можно использовать в функции перед определением.
                </p>
                <pre>
function print(){
    console.log(x); // undefined, но норм
    var x = 76;
}
                </pre>
            </td>
            <td>
                <p>
                Можно использовать только после определения.
                </p>
                <pre>
function print(){
    console.log(x); // ! Ошибка
    let x = 76;
}
                </pre>
            </td>
         </tr>
         <tr>
            <td>
                <p>
                В одной и той же функции можно несколько раз определить переменную с одним и тем же именем.
                </p>
                <pre>
function print(){
    var x = 72;
    console.log(x); // 72
    var x = 24;     // норм
    console.log(x); // 24
}
                </pre>
            </td>
            <td>
                <p>
                В одной и той же функции можно только один раз определить переменную с одним и тем же именем.
                </p>
                <pre>
function print(){
    let x = 72;
    console.log(x); // 72
    let x = 24;     // ! Ошибка
    console.log(x);
}
                </pre>
            </td>
         </tr>
    </tbody>
    
</table>

###  Типы данных

TS является строго типизированным языком, и каждая переменная и константа в нем имеет определенный тип. При этом в отличии
от js мы не можем динамически изменить ранее указанный тип переменной.

В TS имеются следующие базовые типы:

* **Boolean**: логическое значение true или false
* **Number**: числовое значение
* **String**: строки
* **Array**: массивы
* **Tuple**: кортежи
* **Enum**: перечисления
* **Any**: произвольный тип
* **Null и undefined**: соответствуют значениям null и undefined в JS
* **Void**: отсутствие конкретного значения, используется в основном в качестве возвращаемого типа функций
* **Never**: также представляет отсутствие значения и используется в качестве возвращаемого типа функций, которые
генерируют или возвращают ошибку

Большинство из этих типов соотносятся с примитивными типа из JS.

Для установки типа применяется знак двоеточия. Примеры создания переменных:

```typescript
let x: number = 10;
let hello: string = "hello world";
let isValid: boolean = true;
```

То есть в данном случае выражение let hello: string = "hello world" указывает, что переменная hello будет иметь тип
string и значение hello world.

При этом если в коде мы потом захотим изменить тип, например:

```typescript
let hello: string = "hello world";
hello = 23;
```

То в процессе компиляции комплиятор TS выдаст ошибку, и мы попросту не сможем запустить программу.

Но можно в принципе и не указывать тип переменной. Например:

```typescript
let hello = "hello world";
hello = 23;
```

В этом случае TS автоматически выведет тип из присваемого данной переменной значения. Так, на первой строке компилятор
TS увидит, что переменной присваивается строка, поэтому для нее будет использоваться тип string. Однако на второй строке
опять же компилятор выдаст ошибку, поскольку у переменной уже опеределен тип string. А новое значение предполагает тип
number.

Если же переменная определяется без значения, и только впоследствии при работе программы ей присваивается значение, тогда считается,
что она имеет тип any:

```typescript
let x; // тип any
x = 10;
```

#### Boolean

Тип **Boolean** представляет логическое значение true или false:

```typescript
let isEnabled = true;
let isAlive: boolean = false;

console.log(isEnabled)
console.log(isAlive);
```

#### Number

Тип Number представляет числа, причем все числа в TS, как и в JS, являются числами с плавающей точкой. TS поддерживает 
двоичную, восьмеричную, десятичную и шестнадцатиричную записи чисел:

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

#### String

String предствляет строки. Как и в JS, в TS строки можно заключать в двойные, либо в одинарные кавычки:

```typescript
let firstName: string = "Tom";
let lastName = 'Johns';
```

Кроме того, TS поддерживает такую функциональность, как шаблоны строк, то есть мы можем задать шаблон в косых кавычках
(`), как елси бы мы писали строку, и затем в саму строку можно встраивать разные выражения с помощью синтаксиса ${ expr },
где expr - это выражение. Например:

```typescript
let firstName: string = "Tom";
let age: number = 28;
let info: string = `Имя ${firstName}    Возраст: ${age}`;
console.log(info);  // Имя Tom    Возраст: 28
```

Косые кавычки также можно применять для установки многострочного текста:

```typescript
let sentence: string = `Hello World!
Goob bye World!`;
```

#### Null и undefined

Как и в JS, в TS есть специальные типы undefined и null, которые принимают соответствующие значения undefined и null:

```typescript
let a: undefined = undefined;
let b: null = null;
```

Но фактически мы можем присваивать значения undefined и null переменным других типов, например, number:

```typescript
let x: number = undefined;
console.log(x);
x = null;
console.log(x);
x = 5;
console.log(x);
```

В этом плане null и undefined выступают как подтипы других типов и полезны преимущественно в каких-то операциях, где
неизвестен результат - то ли это будет число или строка, то ли это будет null. В этом случае, чтобы избежать возможной
ошибки, мы можем проверить значение на undefined или null, собственно как и в js.

#### Массивы

Массивы определяются с помощью выражения [] и также являются строго типизированными. То есть если изначально массив
содержит строки, то в будущем он сможет работать только со строками.

```typescript
let list: number[] = [10, 20, 30];
let colors: string[] = ["red", "green", "blue"];
console.log(list[0]);
console.log(colors[1]);
```

Как и в JS, с помощью индексов можно обращаться к элементам массива.

Альтернативный способ определения массивов представляет применение типа Array<>;

```typescript
let names: Array<string> = ["Tom", "Bob", "Alice"];
console.log(names[1]);  // Bob
```

#### Кортежи

Кортежи (Tuples) также, как и массивы, представляют набор элементов, для которых уже заранее известен тип. Например:

```typescript
// определение кортежа - кортеж состоит из двух элементов - строки и числа
let userInfo: [string, number];
// инициализация кортежа
userInfo = ["Tom", 28];
// Неправильная инициализация - переданные значения не соответствуют типам по позиции
//userInfo = [28, "Tom"]; // Ошибка
 
// использование кортежа
console.log(userInfo[1]); // 28
userInfo[1] = 37;
```

#### Тип enum

Тип enum предназначен для описания набора числовых данных с помощью строковых констант. Так, объявим следующее перечисление:

```typescript
enum Season { Winter, Spring, Summer, Autumn };
```

Перечисление называется Season и имеет четыре элемента. Теперь используем перечисление:

```typescript
enum Season { Winter, Spring, Summer, Autumn };
let current: Season = Season.Summer;
console.log(current);
current = Season.Autumn; // изменение значения
```

Здесь создается переменная current, которая имеет тип Season. При этом консоль выведет нам число 2. Так как все элементы
перечисления представляют числовые значения. По умолчанию следующие:

```typescript
enum Season { Winter=0, Spring=1, Summer=2, Autumn=3 };
```

Хотя мы можем переопределить эти значения:

```typescript
enum Season { Winter=5, Spring, Summer, Autumn }; // 5, 6, 7, 8
enum Season { Winter=4, Spring=8, Summer=16, Autumn=32 }; // 4, 8, 16, 32
```

Также мы можем получить непосредственно текстовое значение:

```typescript
enum Season { Winter=0, Spring=1, Summer=2, Autumn=3 };
var current: string = Season[2]; // 2 - числовое значение Summer
console.log(current);  // Summer
```

#### Тип any

Any описывает данные, тип которых может быть неизвестен на момент написания приложения.

```typescript
let someVar: any = "Hello";
console.log(someVar); // сейчас someVar - это string
someVar = 20;
console.log(someVar); // сейчас someVar - это number
``` 
Так как здесь применяется тип any, то данный код скомпилируется без ошибок, несмотря на смену строкового значения на числовое.
И также мы можем объявлять массивы данного типа:

```typescript
var someArray: any[] = [ 24, "Tom", false ];
```

#### Комплексные объекты

Кроме простых переменных, как и в JS, можно создавать сложные объекты. Например:

```typescript
let person = { name: "Tom", age: 23 };
console.log(person.name);
// альтернативный вариант получения свойства
console.log(person["name"]);
```

Но несмотря на то, что это фактически тот же самый объект, что мы могли бы использовать в JS, в силу строготипизированности
TS мы имеем в данном случае ограничения. В частности, если у нас будет следующий код:

```typescript
let person = { name: "Tom", age: 23 };
person = { name: "Alice" };
```

То на второй строке мы получим ошибку, поскольку компилятор после первой строки предполагает, что объект person будет
иметь два свойства name и age. Должно быть соответствие по названиям, количеству и типу свойств. 

### Работа с типами данных

#### Объединения

Объединения или union не являются типом данных, но они позволяют определить переменную, которая может хранить значение двух
или более типов:

```typescript
let id: number | string;
id = "12345dgg5";
console.log(id); // 1345dgg5
id = 234;
console.log(id); // 234
```

Чтобы определить все типы, которые должно представлять перечисление, все эти типы разделяются прямой чертой: number | string.
В данном случае переменная id может представлять как тип string, то есть строку, так и число.

#### Проверка типа

С помощью оператора typeof мы можем проверить тип переменной. Это может быть необходимо, когда мы хотим выполнить некоторый
операции с переменной, но нам неизвестен ее точный тип (например, переменная представляет тип any). Данная функциональность
еще называется type guards или защита типа:

```typescript
let sum: any;
sum = 1200;
sum = "тысяча двести";
let result: number = sum / 12;
console.log(result); // Nan - строку нельзя разделить на число
```

Переменная sum может хранить любое значение, однако деление может работать только с числами. ПОэтому перед делением
выполним проверку на тип:

```typescript
let sum: any;
sum = 1200;

if (typeof sum === "number") {
    
    let result: number = sum / 12;
    console.log(result);
} else {
    console.log("invalid operation");
}
```

После оператора typeof указывается имя переменной, затем равно и название типа, на который идет проверка. Если переменная
соответствует типу, то оператор typeof возвращает значение true.

#### Псевдонимы типов

TypeScript позволяет определять псевдонимы типов с помощью ключевого слова type:

```typescript
type stringOrNumberType = number | string;
let sum: stringOrNumberType = 36.6;
if (typeof sum === "number") {
    console.log(sum / 6)
}
```

Далее мы сможем применять псеводним аналогично типу данных.

#### Type assertion

Type assertion представляет модель преобразования значения переменной к определенному типу. Обычно в некоторых ситуациях
одна переменная может представлять какой-то широкий тип, например, any, который по факту допускает значения различных
типов. Однако при этом нам надо использовать переменную как значение строго определенного типа. И в этом случае мы можем
привести к этому типу.

Есть две формы приведения. Первая форма заключается в использовании угловых скобок:

```typescript
let someAnyValue: any = "hello world!";
let strLength: number = (<string>someAnyValue).length;
console.log(strLength); // 12

let someUnionValue: string | number = "hello work";
strLength = (<string>someUnionValue).length;
console.log(strLength); // 10
```

Вторая форма заключается в применении оператора as:

```typescript
let someAnyValue: any = "hello world!";
let strLength: number = (someAnyValue as string).length;
console.log(strLength); // 12

let someUnionValue: string | number = "hello work";
strLength = (someUnionValue as string).length;
console.log(strLength); // 10
```

### Функции

#### Определение функции

В javascript функции определяются с помощью ключевого слова function, например:

```typescript
function add(a, b) {
    return a + b;
}
// использование функции
var result1 = add(1, 2); // результат 3
var result2 = add("1", "2"); // результат 12
```

TypeScript также определяет функцию с помощью ключевого слова function, но при этом добавляет дополнительные возможности
по работе с функциями. В частности, теперь мы можем определить тип передаваемых параметров и тип возвращаемого значения.
Типичное определение функции в TypeScript:

```typescript
function add(a: number, b: number):number {
    return a + b;
}
// вызов функции
let result1 = add(1, 2);
console.log(result1)
```

Либо мы можем определить функцию как переменную и затем через переменную вызвать данную функцию:

```typescript
let add = function(a: number, b: number):number {
    return a + b;
}
let result1 = add(1, 2);
console.log(result1)
```

#### Параметры функции

Функция может иметь параметры, которые указываются после названия функции в скобках через запятую. Через двоеточие после
имени параметра указывается его тип:

```typescript
// определение функции
function add(a: number, b: number) {
    let result = a + b;
    console.log(result);
}
// вызов функции
add(20, 30); // 50
add(10, 15); // 25
```

Однако поскольку параметры имеют тип number, то при вызове функции

```typescript
add("1", "2");
```

Компилятор TS выдаст ошибку, так как параметры должны иметь тип number, а не тип string.

При этом функция может не только использовать передаваемые параметры, но и глобальные переменные, определенные во вне:

```typescript
let koef: number = 1.5;

function add(a: number) {
    let result = a *koef;
    console.log(result);
}

add(20); // 30
add(10); // 15
```

#### Результат функции

Функция может возвращать значение определенного типа, который еще называется типом функции.
Возвращаемый тип функции ставится после списка параметров через двоеточие:

```typescript
let add = function(a: number, b: number):number {
    return a + b;
}
let result1 = add(1, 2);
```

В данном случае функция будет возвращать значения типа number.

Если функция ничего не возвращает, то указывается тип void:

```typescript
let add = function(a: number, b: number): void {
    console.log(a + b)
}
add(10, 20);
```

В принципе мы можем и не указывать тип, тогда он будет выводиться неявно на основе возвращаемого значения:

```typescript
function add(a: number, b: number) {
    return a + b;
}
let result = add(10, 20);
```

#### Необязательные параметры

В typescript при вызове в функцию должно передавать ровно столько значений, сколько в ней определено параметров:

```typescript
function getName(firstName: string, lastName: string) {
    return firstName + " " + lastName;
}

let name1 = getName("Иван", "Кузнецов");
let name2 = getName("Иван", "Михайлович", "Кузнецов"); // ошибка, много параметров
let name3 = getName("Иван"); // ошибка, мало параметров
```

Чтобы иметь возможность передавать различное число значений в функцию, в TS некоторые параметры можно объявить как необязательные.
Необязательные параметры должны быть помечены вопросительным знаком ?. Причем необязательные параметры должны идти после
обязательных:

```typescript
function getName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName
}

let name1 = getName("Иван", "Кузнецов");
console.log(name1) // Иван Кузнецов
let name2 = getName("Вася");
console.log(name2) // Вася
```

Во втором случае, когда в функцию передается только имя, второй используемый параметр будет иметь неопределенное значение
или "undefined". Поэтмоу с помощью условной конструкции проверяется наличие значения для этого параметра.

#### Параметры по умолчанию

Параметры по умолчанию позволяют задать начальное значение. И если для такого параметра не передается значение, то он
использует значение по умолчанию:

```typescript
function getName(firstName: string, lastName: string="Иванов") {
    return firstName + " " + lastName;
}
let name1 = getName("Иван", "Кузнецов");
console.log(name1); // Иван Кузнецов
let name2 = getName("Вася");
console.log(name2); // Вася Иванов
```

#### Неопределенный набор параметров

Если же необходимо, чтобы функция принимала набор однотипных параметров, то используется знак многоточия, после которого
идет массив:

```typescript
function addNumbers(firstNumber: number, ...numberArray: number[]): number {
    
    let result = firstNumber;
    for (let i = 0; i < numberArray.length; i++) {
        result+= numberArray[i];
    }
    return result;
}

let num1 = addNumbers(3, 7, 8);
console.log(num1); // 18

let num2 = addNumbers(3, 7, 8, 9, 4);
console.log(num2); // 31
```

#### Перегрузка функций

TypeScript поддерживает возможность перезгрузки функций, то есть мы можем определить несколько версий функции, которые
будут иметь одно и то же имя, но разные типы параметров или разное количество параметров. Для перегрузки вначале
определяем все версии функции, которые не будут иметь инкакой логики. А потом определяем версию функции с общей сигнатурой,
которая подходит под все ранее определенные варианты. И в этой общей версии уже определяем конкретную логику функции.

Например, нам надо объединить два значения, но если они представляют строки, то просто их конкатенировать, а если числа - 
то сложить. ТОгда мы могли бы использовать следующую функцию:

```typescript
function add(x: string, y: string): string;
function add(x: number, y: number): number;
function add(x: any, y: any): any {
    return x + y;
}

let result1 = add(5, 4);
console.log(result1); // 9
let result2 = add("5", "4");
console.log(result2); // 54
```

Первая версия функции add приинмает две строки и возвращает стркоу, воторая версия принимает два числа и возвращает
число. Общей для них будет функция, которая принимает параметры типа any и возвращает рультат также типа any.

Но если бы мы ту же функцию применили бы к логическим значениям:

```typescript
let result3 = add(true, false);
console.log(result3);
```
то мы получили бы ошибку, так как две версии функции позволяют принмать в качестве параметров либо две строки, либо
два числа. И в этом случае нам надо было бы добавить еще одну версию функции два логических значений:

```typescript
function add(x: boolend, y: boolean): boolean;
```

### Тип функции и стрелочные функции

#### Тип функции

Каждая функция имеет тип, как и обычные переменные. Тип функции фактически представляет комбинацию типов параметров и
типа возвращаемого значения. Например, возьмем следующую функцию:

```typescript
function sum(x: number, y: number): number {
  return x + y;
}
```

Она имеет тип (x:number, y:number) => number;, то есть принимает два параметра number и возвращает значения типа number.
Названия параметров в типе функции необязательно должны соответствовать названиям конкретной функции. А перед типом
возвращаемого значения ставится знак равно со стрелкой. 

И подобно тому, как определяются переменные определенного типа, можно определять переменные, которые имеют тип функции:

```typescript
let op: (x: number, y: number) => number;
```

То есть переменная op представляет любую функцию, которая принимает два числа и которая возвращает число. Например:

```typescript
function sum(x: number, y: number): number {
    return x + y;
}
function subtract(a: number, b: number): number {
    return a - b;
}

let op: (x: number, y: number) => number;

op = sum;
console.log(op(2, 4)); // 6

op = subtract;
console.log(op(6, 4)) // 2
```

Здесь вначале переменная op указывает на функцию sum. И соответственно вызов op(2, 4) фактически будет представлять
вызов sum(2, 4). А затем op указывает на функцию subtract.

#### Функция обратного вызова

Тип функции можно использовать как тип переменной, но он также может применяться для определения типа параметра другой
функции:

```typescript
function mathOp(x: number, y: number, operation: (a: number, b: number) => number): number {
    let result = operation(x, y);
    return result;
}

let operationFunc: (x: number, y: number) => number;
operationFunc = function(a: number, b: number): number {
    return a + b;
}
console.log(mathOp(10, 20, operationFunc)); // 30

operationFunc = function(a: number, b: number): number {
    return a * b;
}
console.log(mathOp(10, 20, operationFunc)); // 200
```

Здесь в функции mathOp третий параметр как раз представляет функцию, которая принимает два параметра типа number и 
возвращает число. Фактически тем самым мы можем передавать функции обратного вызова, например, при генерации событий,
когда в ответ на некоторое действие срабатывает другая функция.

#### Стрелочные функции

Для определения функций в TypeScript можно использовать стрелочные функции или arrow functions. Стрелочные функции
представляют выражения типа (параметры) => тело функции. Например:

```typescript
let sum = (x: number, y: number) => x + y;

let result = sum(15, 35);
console.log(result); // 50
```

Тип параметров можно опускать:

```typescript
let sum = (x, y) => x + y;

let result = sum(15, 35);
console.log(result); // 50
```

Если стрелочная функция не требует параметров, то используются пустые круглые скобки. Если передается только один параметр,
то скобки можно опустить:

```typescript
let square = x => x * x;
let hello = () => "hello world"
  
console.log(square(5)); // 25
console.log(hello());   // hello world
```

Если тело функции представляет множество выражений, а не просто одно выражение, как в примере выше, тогда можно опять же
заключить все выражения в фигурные скобки:

```typescript
let sum = (x: number, y: number) => {
    x *= 2;
    return x + y;
};
 
let result = sum(15, 35); // 65
console.log(result);
```

Стрелочные функции можно передавать в функцию вместо параметра, который представляет собой функцию:

```typescript
function mathOp(x: number, y: number, operation: (a: number, b: number) => number): number {
    
    let result = operation(x, y);
    return result;
}
console.log(mathOp(10, 20, (x,y)=>x+y)); // 30
console.log(mathOp(10, 20, (x,y)=>x*y)); // 200
```

## Объектно-ориентированное программирование

### Классы

TypeScript реализует объектно-ориентированный подход, в нем есть полноценная поддержка классов. Класс представляет
шаблон для создания объектов и инкапсулирует функциональность, которую должен иметь объект. Класс определяет состояние и 
поведение, которыми обладает объект.

Для определения нового класса применяется ключевое слово class:

```typescript
class User {
    
    id: number;
    name: string;
    getInfo(): string {
        return "id:" + this.id + " name" + this.name;
    }
}
```

Класс называется User, он представляет пользователя и имеет два свойства id и name, которые хранят состояние объекта. И также класс 
определяет одну функцию getInfo(), которая представляет поведение объекта.

После определения класса мы можем создавать его объекты:

```typescript
let tom: User = new User();
tom.id = 1;
tom.name = "Tom";
console.log(tom.getInfo());

let alice: User = new User();
alice.id = 2;
alice.name = "Alice";
console.log(alice.getInfo());
```

Кроме обычных функций классы имеют специальные функции - конструкторы, которые определяются с помощью ключевого слова
constructor. Конструкторы выполняют начальную инициализацию объекта. Например, добавим в класс User конструктор:

```typescript
class User {
    id: number;
    name: string;
    constructor(userId: number, userName: string) {
        this.id = userId;
        this.name = userName;
    }
    getInfo(): string {
        return "id:" + this.id + " name:" + this.name;
    }
}

let tom: User = new User(1, "Tom");
console.log(tom.getInfo());
tom.id = 4;

let alice: User = new User(2, "Alice");
console.log(alice.getInfo());
```

### Статические свойства и функции

Кроме обычных свойств и функций класс может иметь статические. Для использования статических функций и свойства не надо
создавать объект класса.

Статические фунеции и свойства определяются с помощью ключевого слова static:

```typescript
class Operation {
    
    static PI: number = 3.14;
    
    static getSquare(radius: number): number {
        
        return Operation.PI * radius * radius;
    }
}

let result = Operation.getSquare(30);
console.log("Площадь круга с радиусом 30 равно " + result);
let result2 = Operation.PI * 30 * 30;
console.log(result2); // 2826
```

### Модификаторы доступа

Одной из ключевых концепций объектно-ориентированного программирования является инкапсуляция, подразумевающая сокрытие 
от внешнего доступа к состоянию объекта и управление доступом к этому состоянию. Обычно для этого во многих ООП-языках 
(как Java, C#) используются модификтора доступа. В TS три модификтора: public, protected и private.

Если к свойствам и функциям классов не применяется модификтор, то такие свойства и функции расцениваются как будто они определены
с модификтором public. То есть следующее определение класса:

```typescript
class User {
    name: string;
    year: number;
}
```

Будет эквивалентно:

```typescript
class User {
    public name: string;
    public year: number;
}
```

#### Private

Если же к свойствам и методам применяется модификтор private, то к ним нельзя будет обратиться извне при создании объекта
данного класса.

Например, создадим класс с приватными свойствами и методами:

```typescript
class User {
    private _name: string;
    private _year: number;
    
    constructor(name: string, age: number) {
        this._name = name;
        this._year = this.setYear(age)
    }
    public displayYear(): void {
        console.log("Год рождения: " + this._year);
    }
    
    public displayName(): void {
        console.log("name: " + this._name)
    }
    
    private setYear(age: number): number {
        return new Date().getFullYear() - age;
    }
}

let tom = new User("Tom", 24);
tom.displayName();
tom.displayYear();
console.log(tom._name); // нельзя обратиться, так как _name - private
console.log(tom.setYear(45)); // нельзя обратиться, так как функция - private
```

Два свойства _name и _year используются с модфикатором private, поэтмоу мы не можем их использовать вне класса, например,
console.log(tom._name). То же самое относится к функции setYear(). Остальные функции доступны.

Нередко приватные свойства в своем названии в качестве первого символа имеют символ подчеркивания. Но не обязательно так делать, это скорее
сложившаяся практика.

### protected

Модификтора protected во многом аналогичен private - свойства и методы с данным модфикатором не видны из вне, но к ним
можно обратиться из классов-наследников:

```typescript
class User {
    private name: string;
    protected age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    public displayInfo(): void {
        
        console.log("name: " + this.name + "; age: " + this.age);
       
    }
}
class Emplyee extends User {
  
    private company: string;
    constructor(name: string, age: number, company: string) {
        super(name, age);
        this.company = company;
    }
    public showData(): void {
        console.log("Age: " + this.age);
        console.log("Name: " + this.name); // не работает, так как name - private
    }
}
```

В классе Employee будет доступно свойство age, так как оно имеет модификтор protected. А вот приватное свойство name
будет недоступно.

#### Определение свойств через конструктор

Использование модификторов в параметрах конструктора позволяет сократить написание кода. Например, пусть у нас есть
следующий класс:

```typescript
class User {
    private _name: string;
    private _age: number;
    
    constructor(name: string, age: number) {
        
        this._name = name;
        this._age = age;
    }
    public displayInfo(): void {
        console.log("name: " + this._name + "; age: " + this._age);
    }
}
```

Этот класс будет аналогичен следующему:

```typescript
class User {
    constructor(private name: string, private age: number) {
    }
    public displayInfo(): void {
        console.log("name: " + this.name + "; age: " + this.age)
    }
}
```

Используя модификторы в параметрах конструктора, нам больше не надо явно создавать свойства для этих параметров.
Свойства создаются автоматически, называются они по имени параметров и имеют теже модификаторы, что и параметры.

Подобным образом, если мы хотим сделать свойства публичными, то следует создавать модификтора public: 

```typescript
class User {
    constructor(public name: string, public age: number) {
    }
}
```

### Методы доступа и readonly-свойства

#### Методы доступа

В стандарте JavaScript ECMAScript 5 была предложена концепция методов доступа: для доступа к свойству пара методов -
get-метод для получения значения свойства и set-метод для установки значения. Это довольно распространненая концепция,
которая нашла свое применение, например, в Java, где для управления доступом к приватным переменным создается пара
методов - get/set, или в С#, где для доступа к приватным переменным создается свойство с двумя методами get/set.

К примеру, у нас есть следующий класс:

```typescript
class User {
    name: string;
}

let tom = new User();
tom.name = "Tom";
console.log(tom.name);
```

Использование аксессоров или методов доступа позволяет управлять тем, как значение устанавливается и как оно возвращается.
В частности, мы можем переписать предыдущий класс с использование акссессоров следующим образом:

```typescript
class User {
    private _name: string;
    
    public get name(): string {
        return this._name;
    }
    
    public set name(n: string) {
        this._name = n;
    }
}

let tom = new User();
tom.name = "Tom";  // Срабатывает set-метод
console.log(tom.name); // Срабатывает get-метод
```

Методы доступа определяются как обычные методы, только перед ними ставятся ключевые слова get/set. Set-метод контроллирует
установку значения, а get-метод возвращает значение.

#### Свойства только для чтения

Ключевое слово readonly позволяет определить свойства, которые доступны только для чтения:

```typescript
class User {
  readonly id: number;
  name: string;
  constructor(userId: number, userName: string) {
      this.id = userId;
      this.name = userName
  }
}

let tom: User = new User(2, "Tom");
console.log(tom.id, tom.name);
// tom.id=34;   // Ошибка - так как id - Только для чтения
```

В данном случае свойство id доступно только для чтения. Мы можем установить его значения только в конструкторе класса.

Подобное определение свойств для чтения можно сократить следующим образом:

```typescript
class User {
    name: string;
    constructor(readonly id: number, userName: string) {
        this.name = userName
    }
}
```

Также мы можем вместе с модификтором readonly задать модификтор доступа.

#### Наследование. Абстрактные классы

Одним из ключевых моментов объектно-ориентированной парадигмы является наследование. В TypeScript наследование
реализуется с помощью ключевого слова extends (как в Java):

```typescript
class User {
    
    name: string;
    constructor(userName: string) {
        this.name = userName
    }
    getInfo(): void {
        console.log("Имя: " + this.name);
    }
    
}

class Employee extends User {
    company: string;
    work(): void {
        console.log(this.name + " работает в компании " + this.company)
    }
}
```

Класс Employee, который представляет работника, является подклассом или наследуется от класса User. А класс User называется
родительским или базовым классом. При наследовании класс Employee перенимает весь функционал класса User - все его свойства и функции
и может их использовать. И также можно определить в подклассе новые свойства и методы, которых нет в классе User.

```typescript
let bill: Employee = new Employee("Bill");
bill.getInfo();
bill.company = "Microsoft"
bill.work();
``` 

Также мы можем расширить функциональность класса следующим образом:

```typescript
class User {
    name: string;
    constructor(userName: string) {
     this.name = userName;
    }
    getInfo(): void {
        console.log("Имя " + this.name);
    }
    
}

let Employee = class extends User {
    company: string;
    work(): void {
        console.log(this.name, " работает в компании ", this.company)
    }
}

let sam = new Employee("Sam");
sam.company = "Google";
sam.work();
```

#### Предопределение конструктора

Если подкласс определяет свой конструктор, то в нем должен быть вызван конструктор базового класса с помощью ключевого
слова super:

```typescript
class User {
    name: string;
    constructor(userNmae: string) {
        this.name = userNmae
    }
    getInfo(): void {
        console.log("Имя: " + this.name);
    }
}

class Employee extends User {
    company: string;
    constructor(userName: string, empCompany: string) {
        super(userName);
        this.company = empCompany
    }
    work(): void {
        console.log(this.name + " работает в компании " + this.company);
    }
}
let bill: Employee = new Employee("Bill", "Apple");
bill.work();
```

С помощью ключевого слова super подкласс может обратиться к функционалу базового класса. В данном случае идет обращение к
конструктору класса User, который устанавливает значение свойства name: super(superName).

Причем даже если базовый класс не определяет явным образом никакого конструктора, в производном классе при определении
конструктора все равно надо вызвать конструктор базового класса - в этом случае это будет вызов конструктора по
умолчанию с помощью super().

```typescript
class User {
    name: string;
}

class Employee extends User {
    company: string;
    constructor(empCompany: string) {
        super();
        this.company = empCompany;
    }
   
}
```

#### Переопределение методов

Также производные классы могут переопределять методы базовых классов:

```typescript
class User {
    name: string;
    constructor(userName: string) {
        this.name = userName;
    }
    getInfo(): void {
        console.log("Имя: " + this.name);
    }
}

class Employee extends User {
    company: string;
    constructor(userName: string, empCompany: string) {
     super(userName);
     this.company = empCompany;
    }
    getInfo(): void {
        console.log("Имя: " + this.name);
        console.log("Работает в компании: " + this.company);
    }
}
let bill: Employee = new Employee("Bill", "Apple");
bill.getInfo();
```

В данном случае переопределяется метод getInfo(), который кроме имени выводит также компанию сотрудника. Однако в данном
случае реализация метода getInfo из базового класса повторяется в производном классе. И вместо того, чтобы дублирова код, 
мы можем с помощью ключевого слова super вызвать реализацию этого метода из базового класса:

```typescript
class User {
    name: string;
    constructor(userName: string) {
     this.name = userName;
    }
    getInfo(): void {
        console.log("Имя: " + this.name);
    }
}

class Employee extends User {
    company: string;
    constructor(userName: string, empCompany: string) {
        super(userName);
        this.company = empCompany;
    }
    getInfo(): void {
        super.getInfo();
        console.log("Работает в компании: " + this.company);
    }
}
```

#### Абстрактные классы

Абстрактные классы представляют классы, определенные с ключевым словом abstract. Они во много похожи на обычные классы
за тем исключением, что мы не можем создать напрямую объект абстрактного класса, исопльзуя его конструктор.

```typescript
abstract class Figure {
}

let someFigure = new Figure()  // Ошибка!
```

Как правило абстрактные классы описывают сущности, которые в реальности не имеют конкретного воплощения. Например, геометрическая
фигура может представлять круг, квадрат, треугольник, но как таковой геометрической фигуры самой по себе существует. 
Есть конкретные фигуры, с которыми мы и работаем. В то же время все фигуры могут иметь какой-то общий функционал. В этом
случае мы можем определить абстрактный класс фигуры, поместить в него общий функционал, и от него унаследовать классы конкретных геометрических
фигур:

```typescript
abstract class Figure {
  getArea(): void {
      console.log("Not Implemented");
  }
}
class Rectangle extends Figure {
  constructor(public  width: number, public height: number) {
      super();
  }
  
  getArea(): void {
      let square = this.width * this.height;
      console.log("area =", square);
  }
}

let someFigure: Figure = new Rectangle(20, 30);
someFigure.getArea(); // area = 600
```

В данном случае абстрактный класс определяет метод getArea(), который вычисляет площадь фигуры. Класс прямоугольника
определяет свою реализацию для этого метода.

Однако в данном случае метод getArea в базовом классе не выполняет никакой полезной работы, так как у абстрактной
фигуры не может быть площади. И в этом случае подобный метод лучше определить как абстрактный:

```typescript
abstract class Figure {
    abstract getArea(): void;
}
class Rectangle extends Figure {
    constructor(public width: number, public height: number) {
        super();
    }
    
    getArea(): void {
        let square = this.width * this.height;
        console.log("area =", square)
    }
}
let someFigure: Figure = new Rectangle(20, 30);
someFigure.getArea();
```

Абстрактный метод не определяет никакой реализации. Если класс содержит абстрактные мтеоды, то такой класс должен быть абстрактным.
Кроме того, при наследовании производные классы обязаны реализовать все абстрактные методы.

### Интерфейсы

#### Интерфейсы объектов

Интерфейс определяет свойства и методы, которые объект должен реализовать. Другими словами, интерфейс - это определение
кастомного типа данных, но без реализации. В данном случае интерфейсы в TS похожи на интерфейсы в языках Java и C#.
Интерфейсы определяются с помощью ключевого слова interface. Для начала определим простенький интерфейс:

```typescript
interface IUser {
  id: number;
  name: string;
}
```

Интерфейс в фигурных скобках определяет два свойства: id, которое имеет тип number, и name, которая представляет строку.
Теперь используем его в программе:

```typescript
let employee: IUser = {
    
    id: 1,
    name: "Tom"
}
console.log("id: " + employee.id);
console.log("name: " + employee.name);
```

По сути employee - обычный объект за тем исключением, что он имеет тип IUser. Если правильнее говорить, то employee
реализует интерфейс IUser. Причем эта реализация накладывает на employee некоторые ограничения. Так, employee должен
реализовать все свойства и методы интерфейса IUser, поэтому при определении employee данный объект обязательно должен включать в себя свойства
id и name. 

Параметры методов и функций также могут представлять интерфейсы:

```typescript
interface IUser {
    id: number;
    name: string;
}

let employee: IUser = {
    id: 1,
    name: "Alice"
}

function getEmployeeInfo(user: IUser): void {
    console.log("id: " + user.id);
    console.log("name: " + user.name);
}

getEmployeeInfo(employee)
```

В этом случае аргумент, который передается в функцию, должен представлять объек или класс, который реализует соответствующий
интерфейс.

И также можно возвращать объекты интерфейса:

```typescript
interface IUser {
    id: number;
    name: string;
}
function buildUser(userId: number, userName: string): IUser {
    return { id: userId, name: userName };
}

let newUser = buildUser(2, "Bill");
console.log("id: " + newUser.id);
console.log("name: " + newUser.name);
```

#### Необязательные свойства и свойства только для чтения

При определении интерфейса мы можем задать некоторые свойства как необязательные с помощью знака вопроса. Подобные свойства
реализовать необязательно:

```typescript
interface IUser {
    id: number;
    name: string;
    age?: number;
}
let employee: IUser = {
    id: 1,
    name: "Alice",
    age: 23
}
let manager: IUser = {
    id: 2,
    name: "Tom"
}
```

Свойство age помечено как необязательное, поэтому его можно не определять в объектах.

Также интерфейс может содержать свойства только для чтения, значение которых нельзя изменять. Такие свойства определяются с
помощью ключевого слвоа readonly:

```typescript
interface Point {
    readonly x: number;
    readonly y: number;
}
let p: Point = { x: 10, y: 20 };
console.log(p);
p.x = 5; // Ошибка - свойство доступно только для чтения
```

#### Определение методов

Кроме свойств интерфейсы могут определять функции:

```typescript
interface IUser {
    id: number;
    name: string;
    getFullName(surname: string): string;
}
let employee: IUser = {
    id: 1,
    name: "Alice",
    getFullName(surname:string):string {
        return this.name + " " + surname
    }
};

let fullName = employee.getFullName("Tompson");
console.log(fullName); // Alice Tompson
```

Опять же объект, который реализует интерфейс, также обязан реализовать определенную в интерфейсе функцию с тем же набором
параметров и тем типом выходного результата. В данном случае функция getFullName() в качестве параметра принимает строку
и возвращает строку, осуществляя конкатенацию имени и фамилии.

#### Интерфейсы классов

Интерфейсы могут быть реализованы не только объектами, но и классами. Для этого используется ключевое слово implements:

```typescript
interface IUser {
    id: number;
    name: string;
    getFullName(surname: string): string;    
}

class User implements IUser {
    id: number;
    name: string;
    age: number;
    constructor(userId: number, userName: string, userAge: number) {
        this.id = userId;
        this.name = userName;
        this.age = userAge
    }
    getFullName(surname:string):string {
        return this.name + " " + surname
    }
}

let tom = new User(1, "Tom", 23);
console.log(tom.getFullName("Simpson"));
```
Класс User реализует интерфейс IUser. В этом случае класс User обязан определить все те же свойства и функции, которые
есть в IUser.

При этом объект tom является как объектом User, так и объектом IUser:

```typescript
let tom :IUser = new User(1, "Tom", 23);
// или
let tom :User = new User(1, "Tom", 23);
```

#### Наследование интерфейсов

Интерфейсы, как и классы, могут наследоваться:

```typescript
interface IMovable {
    speed: number;
    move(): void;
}
interface ICar extends IMovable {
    fill(): void;
}
class Car implements ICar {
    speed: number;
    move():void {
        console.log("Машина едет со скоростью " + this.speed + " км/ч");
    }
    fill():void {
        console.log("Заправляем машину топливом");
    }
}

let auto = new Car();
auto.speed = 60;
auto.fill();
auto.move();
```

После наследования интерфейс ICar будет также иметь все те свойства и функции, которые определены в IMovable. И тогда,
класс Car, реализующий интерфейс ICar, должен будет реализовать также и свойства и методы интерфейс IMovable.

#### Интерфейсы функций

Интерфейсы функций содержат определние типа функции. Затем они должны быть реализованы объектом, который представляет
функцию данного типа:

```typescript
interface FullNameBuilder {
    (name: string, surname: string): string;
}

let simpleBuilder: FullNameBuilder = function(name: string, surname: string): string {
    return "Mr. " + name + " " + surname;
}

let fullName = simpleBuilder("Bob", "Simpson");
console.log(fullName); // Mr. Bob Simpson
```

Здесь определен интерфейс FullNameBuilder, который лишь содержит сигнатуру функции. Далее определяется переменная
simpleBuilder, которая имеет тип FullNameBuilder и поэтому должна представлять функцию с данной сигнатурой.

#### Интерфейсы массивов 

Интерфейсы массивов опиывают объекты, к которым можно обращаться по индексу, как, например, к массивам

```typescript
interface StringArray {
    [index: number]: string;
}

let phones: StringArray;
phones = ["iPhone 7", "HTC 10", "HP Elite x3"];

let myPhone: string = phones[0];
console.log(myPhone);
```

Здесь определен интерфейс StringArray, который содержит сигнатуру массива. Эта сигнатура указывает, что объект, который
реализует StringArray, может индексироваться с помощью чисел (объекта типа number). И, кроме того, объект должен хранить
объекты типа string, то есть строки.

Выше индекс представлял тип number. Но мы можем использовать для индексации и тип string:

```typescript
interface Dictionary {
    [index: string]: string;
}

var colors: Dictionary = {};
colors["red"] = "#ff0000";
colors["green"] = "#00ff00";
colors["blue"] = "#0000ff";

console.log(colors["red"]);
```

#### Гибридные интерфейсы

Интерфейсы могут сочетать различные стили, могут применяться сразу как к определению объекта, так и к определению функции:

```typescript
interface PersonInfo {
    (name: string, surname: string): void;
    fullName: string;
    password: string;
    authenticate(): void;
}

function personBuilder(): PersonInfo {
    
    let person = <PersonInfo>function(name: string, surname: string): void {
      person.fullName = name + " " + surname;
    };
    person.authenticate = function() {
      console.log(person.fullName + " входит в систему с паролем " + person.password);
    };
    return person;
}

let tom = personBuilder();
tom("Tom", "Simpson");
tom.password = "qwerty";
tom.authenticate();
```

Тип функции, определяемый в таком гибридном интерфейсе, как правило, выступает в роли конструктора объекта. В данном
случае такой конструктор имеет тип (name: string, surname: string): void;

А функция, которая пердставляет данный интерфейс (в данном случае - функция personBuilder), реализует эту функцию
конструктора, и также может использовать другие свойства и методы, которые были определены в интерфейсе.