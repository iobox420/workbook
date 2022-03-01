
# Функциональный свет в JS
[Функциональное программирование в мире JavaScript](https://www.youtube.com/watch?v=2QAUAZ5qgJM)

## Что проще КАК

Имеративный vs Декларативный

```javascript
// императивный стиль сначала как и только в конце результат
const evenNumbers = []

for (let i = 0; i < array.length; i++) {
  if (isEven(array[i])) {
    evenNumbers.push(array[i])
    }
}
```
```javascript
// декларативный стиль стиль сначала что, а уже потом как
// четные числа
const evenNumber = array.filter(isEven)
```

## Декларативные языки это

css
```css
.button {
  width:30px;
}
```
sql
```sql
SELECT title, id
FROM films
WHERE rating > 7
```

## Задача ФП сделать код понятнеее

Понимание = доверие
ЧТО проще КАК

## Функции vs Процедуры

```javascript
//функция
function sql (x) {
  return x * x 
 }
```
```javascript
//процедура - функция с побочными эффектами
function print  (text) {
  console.log(text)
}
```

## Параметры vs Аргументы

### Параметры

Переменные в обьявлении функции

### Аргументы 
Конкретные значения, переданные в вызове
### Сигнатура
Количество и тип параметров
### Арность 
Число параметров, хранится в свойстве length
#### Арность хитрости
```javascript
//аргументы по умолчнанию
function foo  (x = 0) 

//остаточные параметры
function bar  (...args) 

//декструктуризация
function baz  ({a,b})

foo.length // 0 - мы ничего не передали, параметр по  умолчанию
bar.length // 0 - мы ничего не передали, параметр по  умолчанию
baz.length // 1 - мы передали обьект
```

## Функции первого класса

ведут себя как полноценные обьекты
```javascript
// можно создавать
const empty = () => {}
// присваивать
const nothing = empty
// возвращать и передавать
cont toDo = (fn) => fn
toDo(nothing)( )
```
## Функции высших порядков

### Принимаю/возвращаю/создают другие функции
```javascript
const array = [4,8,null,16,null,42]
const normalized = array.filter(Boolean)

document.body.addEventListener('click', ()=>{})

fetch('api').then((res) => res.json())
```
## Компоненты высших порядков
```javascript
import React from 'react'

const higherOrderComponent = (WrappedComponent) => {

    class HOC extends React.component {
    render()    {   
    return <WrappedComponent />
    }
}

return HOC
}
```
## Композиция
Поток данных. Версия №1
```javascript
const text = 'Сьешь этих мягких булочек'
const wordsFound = words(text)
const wordsUsed = unique(wordsFound)
```
Поток данных. Версия №1
```javascript
const text = 'Сьешь этих мягких булочек'
function uniqueWords (text) {
    return unique(words(text))
}    
const wordsUsed = uniqueWords(text)
```
## Композиция
Фабрика для производства заводов 
Композиция = цепочка вложенных вызовов
```javascript

compose(h,g,f)(x) = h(g(f(x)))

Конвейер который едет справа налево
const double = (n) => n * 2
const increment = (n) => n + 1

//без конвейрного оператора
double(increment(double(double(5)))) // 42
// и с конвейрным оператором
5 |> double |> double |> increment |> double //42
```
## Поток данных. Версия № 3
```javascript
const text = 'Сьешь этих мягких булочек'
const uniqueWords = compose(unique, words)
const wordsUsed = uniqueWords(text)
```
## Point Free Style
Функции не упоминает данные, которые обрабатывает
```javascript
// точечный стиль, используется параметр text
function uniqueWords(text) {
    return unique(words(text))
}
```
Функции это кубики лего. А мы из них что то конструируем. Когда мы находим удачную комбинацию кубиков лего, мы хотим данную комбинацию в будуем переиспользовать.
```javascript
const text = 'Сьешь этих мягких булочек'
// полезная деталь
const uniqueWords = compose(unique, words)
// которая пригодится для новых построек
const wordsUsed = uniqueWords(text)
```
### Пора добавить еще одну деталь
```javascript
function translater (lang, words)
const translate = compose(translater, unique, words)
translate(text) // Boom
```
## Каррирование
### Каррирование - это изолента
Превращает функцию в набор функций с меньшим числом параметров
Алгоритм:
1. Распаковать изоленту
2. Приматывать аргументы по одному и получать новую функцию
3. Функция исполнится как только передан будет последний аргумент
### Каррирование в действии
```javascript
function translater(lang,words)
//распаковываем изоленту
const curriedTranslater = curry(translater)
const translateToRu = curriedTranslater('ru')
const translate(translateToRU, unique, words)
translate(text) // Теперь все работает
```
### Каррирование в деталях
```javascript
function sum(x,y,z) {
    return x + y + z
}
```
## Каррирование в деталях
```javascript
function sum(x, y, z,) {
    return x + y + z 
}
//Распаковываем изоленту
const curriedSum = curry(sum)
curriedSum(3) //sum(3)
curriedSum(3)(14) //sum(3, 14)
curriedSum(3)(14)(15)

const addTo42 = curriedSum(42)
curriedSum(20,38) //100
```
## Частичное применение - кусок скотча
Превращает функцию в единственную функцию в меньшим числом параметров
### Алгоритм
1. Приклеить один или несколько параметров к функции
2. Получить новую функцию и вызвать ее
Частичное применение в деталях
```javascript
// приклеиваем параметр к функции
const partialSum = partial(sum, 42)

partialSum(20, 38) // 100
partialSum(17) // NaN
```
## Частичное применение в действии
```javascript
function translater (lang, text)

const translateToRu = partial(translater, 'ru')

translateToRu(text) // все работает
```
## Частичное применение из коробки
```javascript
function translater (lang, text)

const translateToRu = translater.bind(null, 'ru')

translateToRu(text) // все снова работает
```   

## Порядок аргументов имеет значение
```javascript
// Iteratee-first Data-last
function translater (lang, text)
// Iteratee-last Data-first
function translater (text, lang)
```
## Привязка аргументов с конца
```javascript
function translater (text, lang)

//flip меняет порядок аргументов
const curryRight - compose(curry, flip)
const curriedTranslate = curryRight(translater)
const translateToRu = curriedTranslate('ru')
translateToRu(text) // все работает
```
# Специализация

## Специализация в действии
```javascript
function ajax(url, data, callback) {
    // ... асинхронный запрос
}

// распоковываем изоленту
const curriedAjax = curry(ajax)
// специализация
const userFetcher = curriedAjax('api/users')
// еще больше специализации
const currentUserFetcher = curriedAjax('api/users', { user: USER_ID})
```
### Реализация curry и partial?

## Побочные эффекты: Глобальные переменные
```javascript
let status = 404

function isSuccess () {
    return status === 200 ? true : false
}
// делаем функцию чистой
function isSuccess (status) {
    return status === 200 ? true : false
}
```
## Побочные эффекты: Мутация данных
### Неправильно
```javascript
const fruits = ['orange', 'apple', 'banana']
function sortFruits (fruits) {
    return fruits.sort()
}

const sortedFruits = sortFuits(fruits)
sortedFruits // ['orange', 'apple', 'banana']
fruits // ['orange', 'apple', 'banana']
```
### Правильно
```javascript
const fruits = ['orange', 'apple', 'banana']
function sortFruits (fruits) {
const copy = [...fruits]
    return copy.sort()
}

const sortedFruits = sortFuits(fruits)
sortedFruits // ['orange', 'apple', 'banana']
fruits // ['orange', 'apple', 'banana']
```
Не мутировать данные вне функции, дабы не создать сайд эффекта, для той части программы которая пользуется этими же данными.

## Побочные эффекты: I/O
```javascript
function arrange () {
    const data = fetch('/api')
    // ... работа с data
}

const data = fetch('/api')

function arrange(data) {
    // ... работа с data
}
```
## Борьба с побочными эффектами

**1. Чистые функции**
**2. Иммутабельные (неизменяемые) данные**

## Чистые функции
- Без побочных эффектов
 - Работает детерминированно
- Вызывают только чистые функции

## Чистые функции: Детерминорованность
```javascript
function sqr (x) {
    return x * x
}

function random() {
    return Math.random()
}
```
   Недетерминированность функции — возможность возвращения функцией разных значений несмотря на то, что ей передаются на вход одинаковые значения входных аргументов.

## Чистые функции: Только чистота
```javascript
let state = 'ok'

function notPure () {
    state = null
}

function pure () {
    notPure() // вызов нечистой функции
}
```
Так делать неправильно. Внутри чистых функций необходимо вызывать только чистые функции

## Чистота относительна
Бывают ситуации когда нельзя написать чистую функцию без side effect

## Чистые функции: Мемоизация
Функции с памятью 
```javascript
const sql  = memoize(x => x * x)

const sqr = ( function () {
    const cache = {}; // мемоизация
    // вернуть, если результат квадрата был закеширован ранее
    return (x) => {
        if (cache[x]) {
            return cache[x]
        }
        // вычислить квадрат
)()
```
## Чистые функции : преимущества
 - Кешируемость
 - Простота
 - Ссылочная прозрачность - выражение называется **ссылочно прозрачным**, если его можно заменить соответствующим значением без изменения поведения программы.
 - Легко тестировать
- Легко распараллеливать
Чистые функции 
Неизменяемые данные

## JS очень динамичен
```javascript
//Создаем обьект
const immutable = {
	value: 42,
	sadness: { level: 3}
}

immutable = {} // Ошибка
immutable.value = 23

const frozen = Object.freeze(immutable)

immutable.value = 23 // ошибка

frozen.sadness.level = 100500 // однако если попробуем изменить обьект на более глубоком уровне вложенности у нас это получится
```
## Копия данных: Обьекты
```javascript
const state = { value: 42 }
const copy = Object.assign({}, state)
const copy = { ...state }
```
## Копия данных: Массивы
```javascript
const fruits = ['orange','apple','banana']
const copy = [].concat(fruits)
```
### Настоящая иммутабельность immutable JS и immer
Redux является отличным примером чистых функций и неиммутабельности в JS
**Не стоит стремится к абсолютной чистоте. Наша задача как можно больше кода сделать чистым.**
Чистые функции и неизменяемые данные 

## Ключ в мир Функционального Программирования
[MostlyAdequate/mostly-adequate-guide](https://github.com/fxzhukov/Functional-Light-JS-RU)
[Functional-Light-JS-RU](https://github.com/fxzhukov/Functional-Light-JS-RU)
[Functional Programming Jargon](https://github.com/hemanth/functional-programming-jargon)

