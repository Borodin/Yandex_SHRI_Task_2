#ШРИ Задание №2 — Клиентское приложение (работа с API)

Рабочий пример — [borodin.github.io/Yandex_SHRI_Task_2/](http://borodin.github.io/Yandex_SHRI_Task_2/) (вывод в консоль)

###1. Исправление ошибки
Код не работает из за того, что в функции `callback` не указанна переменная `request`, когда эта функция вызывается она берез значение `request` из внешнего LexicalEnvironment.

К моменту вызовов функции `callback`, цикл уже отработал, поэтому переменная `request` во всех коллбэках равна `'/populations'`, что и приводит к ошибке.

Есть несколько способов исправления этой ошибки, самый "Ленивый", это обернуть цикл во временную функцию:

```javascript
for (i = 0; i < 3; i++) (
	// ...
)
```
**↓**

```javascript
for (i = 0; i < 3; i++) function(i) {
	// ...
})(i);
```
Таким образом, внутри временной функции переменная ```i``` берется уже не из глобальной области видимости.

###2. Добавление новой возможности
Добавим модальное окно с вопросом:
```javascript
var query = window.prompt('Enter the name of the city or the country to find out the population');
```
Заполним массив ```c``` и ```cc``` результатом вопроса:
```javascript
var c = [query], cc = [query], p = 0;
```
В функии ```callback``` заменим ```console.log()``` на ```alert()```, для удобства:
```javascript
alert(p? 'Total population in ' + query + ': ' + p : 'In place '+ query +' population not found'); 
```

Цикл поиска африканских стран нам уже не нужен, можно его убрать:
```javascript
/*
for (i = 0; i < responses['/countries'].length; i++) {
	if (responses['/countries'][i].continent === 'Africa') {
		c.push(responses['/countries'][i].name);
	}
}
*/
```

[Посмотреть все изменения](http://github.com/Borodin/Yandex_SHRI_Task_2/blob/gh-pages/shri.js)