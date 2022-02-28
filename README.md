# Функциональный свет в JS
### Что проще КАК
### Имеративный vs Декларативный
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
### Декларативные языка это
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
### Задача ФП сделать код понятнеее
Понимание = доверие
ЧТО проще КАК

### Функции vs Процедуры
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
### Параметры vs Аргументы
#### Параметры
Переменные в обьявлении функции
#### Аргументы
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
Функции первого класса
ведут себя как полноценные обьекты
// можно создавать
const empty = () => {}









```javascript

```

```javascript

```
```javascript

```
```javascript

```






















