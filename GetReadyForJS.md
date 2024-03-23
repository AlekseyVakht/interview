# Подготовка к собеседованию
## Java Script:

 1. Основные типы данных в JS:
	Всего 8 типов:
	 - String ('Hello, world!')  
	 - Number (4)  Boolean (true/ false)  
	 - null 
	 - undefined  
	 - Object {car: 'Mercedes', year: 2015}  
	 - Symbol ('id') 
	 - BigInt (123456789n)

2. Отличия между null и undefined

	**Null** - присваивается, применяется для обнуления, имеет явное значение (let arr = null):
	```
   let arr = null;
   console.log(arr) // arr = null
   ```
	**Undefined** - не присваивается, в случае если значения нет - оно будет undefined (let arr = undefined => arr не определяется):
	```
   let arr = undefined;
   console.log(arr) // undefined
   ```
3. В чем отличия между операторами == и ===
	Оператор "==" - нестрогое равенство с приведением типов
	```
	0 == false // true
	1 == true // true
	1 == '1' // true
	```
	Оператор "===" - строгое равенство с приведением типов и сравнением значения
	```
	0 === false // false
	1 === true // false
	1 === '1' // false
	```
4. Способы объявления переменных
	Устаревшие способы (на сегодняшний день не применяются в виду того, что объявленные таким образом переменные имеют глобальную или функциональную области видимости)
	```
	a = 5
	var b = 'hello'
	```
	Новые способы - в новом стандарте ES6 применяются два способа объявления переменных **let** и **const**, имеющие блочную область видимости (т.е. использование переменной возможно только внутри блока, где она была объявлена)
	```
	let a = 5
	const obj = {}
	```
	Объявление перменной **a** в блоке if
	```
	let b = 1
	if (a + b > 0) {
		let a = 0
		return console.log('true') // ReferenceError: a is not defined
	}
	```
	
5. Отличия map, filter, reduce и forEach
	map, filter - возвращают новый массив
	
	**map** применяется для перебора и модификации элементов массив через функцию callback:
	```
	Array.map(callbackFn, thisArg)
	```
	```
	let arr = [1,2,3]
	let squaring = arr.map((item) => Math.pow(item, 2))
	console.log(squaring) // [1,4,9]
	```
	**filter** применяется для фильтрации массива и возвращении нового массива при условии, что callback = true:
	```
	Array.filter(callbackFn, thisArg)
	```
	```
	const words = ['spray', 'elite', 'exuberant', 'destruction', 'present']
	const result = words.filter((word) => word.length > 6)
	console.log(result) // ["exuberant", "destruction", "present"]
	```
	**reduce** возвращает результат выполнения:
	```
	Array.reduce(accumulator, currentlValue)
	```
	```
	let arr = [1,2,3]
	let result = arr.reduce((accumulator, currentValue) => return accumulator + currentValue)
	console.log(result) // 6
	```
	**forEach** проходит по исходному массиву без возвращения нового, а так же 
	не поддерживает операторы return, break или continue для прерывания или управления итерацией:
	```
	const locations = [
	  {country: "Россия", population: 10},
	  {country: "Китай", population: 100},
	  {country: "США", population: 20}
	]
	
	locations.forEach(location => {
	  console.log(location.country)
	  // Россия
	  // Китай
	  // США
	})
	```
6. Отличия стрелочных функций от функций, объявленных через function
	Стрелочные функции не имеют ключевого слова arguments
	
	Нет своего this. Он берется из внешней области видимости в момент создания функции 
	*В случае с обычной функцией при создании класса и обращении к this, будет ошибка, ввиду того, что в 	обычных функциях this определяется в момент вызова этой функции:*
	```
	<..>
   eat(food){food.forEach(function(item){
	   console.log(`${this.name} is eating ${item}`)});   
   } 
   const bim = new Dog('Bim')
   bim.eat([bone, cookie])  // Uncaught TypeError: Cannot read properties of undefiend('name')
	```
	*Таким образом появляется необходимость явной привязки контекста this через bind:* 
	```
	<..>
	eat(food){food.forEach(function(item){
	   console.log(`${this.name} is eating ${item}`)}.bind(this));   
   }
   const bim = new Dog('Bim')
   bim.eat([bone, cookie])  // ['Bim is eating bone', 'Bim is eating cookie']
   ```
	```
   eat(food) {
	   console.log('method', this) 
		   food.forEach((item) => { 
			   console.log('arrow func', this) 
			   console.log(`${this.name} is eating ${item}`)
   });   
   } // method: Dog('Bim'), arrow func Dog('Bim')
	```
   
	Не могут быть вызваны через new
7. Замыкание - способность функции запоминать свое лексическое окружение
	 ```
	function parent(num) {
		return function child () {
			console.log(num) // num
		}
	}
	```
	Примеры замыкания на задачах:
	```
	function makeCounter(count) {
		return function () {
			return count++
		}	
	}
	let counter = makeCounter(0)
	console.log(counter()) // 0
	console.log(counter()) // 1
	```
	```
	function createIncrement() {
		let count = 0;
		function increment() {
			return count++
		}
		function getMessage() {
			let message = `Count is ${count}`
			return message
		}
		return [increment, getMessage]
	}

	const [increment, getMessage] = createIncrement();
	console.log(increment()) // 1
	console.log(increment()) // 2
	console.log(increment()) // 3
	console.log(getMessage()) // Count is 3
	```
8. Шаблонные литералы
	```
	let item = 'Hello'
	let str = `${item} world!`
	console.log(str) // Hellow world!
	```
	```
	const html = `
	<p>${text}</p>
	`
	```

9. Set и Map, для чего используются  
	**Map** - коллекция ключ-значение, как и Object, ключи могут быть любого типа
	```
	const map = new Map()
	map.set('a', 1)
	console.log(map.get('a')) // 1
	console.log(map.size) // 1
	console.log(map.delete('a')) => map.size = 0
	```
	**Set** - особая коллекция, в которой каждое значение (без ключа) уникально
	```
	const set = new Set([1,1,2,2,3])
	console.log(set) // Set(3){1,2,3}
	
	set.add(3)
	console.log(set) // Set(3){1,2,3}
	console.log(set.has(1)) // true
	```
10. Как определить наличие свойства у объекта?
	```
	const obj = {
		car: 'Volvo',
		year: 1956
	}
	console.log(obj.hasOwnProperty('car')) // true
	console.log('year' in obj) // true
	```
11. Способы создания объектов  
	**Function:**
	```
	function User (name, surname) {
		this.name = name
		this.surname = surname
	}
	const user = new User(name: "Stas", surname: "Baretskiy")
	console.log(user) // User {name: "Stas", surname: "Baretskiy"}
	```
	**Литеральная нотация:**
	```
	myObj = {
		car: "Volvo",
		year: "1956"
	}
	```
	**Class:**
	```
	class User {
		constructor (name, surname) {
			this.name = name
		this.surname = surname
		}
	}
	
	const user = new User(name: "Stas", surname: "Baretskiy")
	console.log(user) // User {name: "Stas", surname: "Baretskiy"}
	```
	**Конструктор объекта:**
	```
	const obj = new Object();
		obj.name = 'John';
		obj.age = 30;
	```
12. Falsy значения
	```
	console.log(false) // false
	console.log(!!0) // false
	console.log(!!"") // false
	console.log(!!undefined) // false
	console.log(!!null) // false
	console.log(!!NaN) // false
	console.log(!!BigInt(0)) // false
	```
13. Определение Promise  
	**Promise** - специальный объект, предназначенный для работы с асинхронными операциями, содержащий собственное состояние. Pending -> либо fulfilled (выполнено успешно), либо rejected (выполнено с ошибкой).
	Promise заменяет собой callback функцию, которые использовались раньше для работы с async.
	```
	new Promise(resolve, reject => {
		setTimeout(() => {resolve('Done')}, 1000 )
	})
		.then((res) => console.log(res)) // Done
		.catch((err) => console.log(err)) // Error 404
	```
14. Применение async, await для асинхронных запросов
	```
	async function fetchData() {
		const response = await fetch('url.com/')
		const json = await response.json()
		return json
	}
	```
	*Все это нужно для того, чтобы асинхронный код работал синхронно (последовательно)*

15. Оператор spread  
	**Spread ...** - применяется для разоврачивания массивов или объектов
	```
	const firstArr = [1,2,3,4]
	const secondArr = [5,6]
	const result = [...firstArr, ...secondArr]
	console.log(result) // [1,2,3,4,5,6]
	```
	```
	const firstObject = {a: 1, b: 2}
	const secondObject = {c:3, d:4}
	const result = {...firstObject, ...secondObject}
	console.log(result) // { a: 1, b: 2, c: 3, d: 4 }
	```
16. Как избежать ссылочной зависимости при копировании объекта
	```
	const  obj  = { 
		a: { 
			b:  2 
		} 
	};
	const copy = Object.assign({}, obj)
	console.log( obj.a === copy.a) // true - зависимости сохранены, 
	таким образом копия неполная, произошло поверхностное копирование
	```
	```
	const  obj  = { 
		a: { 
			b:  2 
		} 
	};
	const copy = JSON.parse(JSON.stringify(obj))
	console.log( obj.a === copy.a) // false - глубокое копирование, 
	при котором копия имеет свои зависимости (костыль)
	```
	```
	const  obj  = { 
		a: { 
			b:  2 
		} 
	};
	const copy = Object.assign({}, obj)
	copy.a = Object.assign({}, obj.a)
	console.log( obj.a === copy.a) // false - глубокое копирование, 
	при котором копия имеет свои зависимости (более правильный способ)
	```
	```
	const obj = { 
  		a: { 
    		b: 2 
  		} 
	};

	const copy = {...obj, a: {...obj.a}};

	console.log( obj.a === copy.a) // false - глубокое копирование, 
	//создается копия объекта obj путем распыления его свойств в новый объект. 
	//Однако, чтобы выполнить глубокое копирование, мы также 
	//создаем копию вложенного объекта a с помощью спред-оператора {...obj.a}.
	//В результате у нас есть новый объект copy, который является глубокой копией исходного объекта obj.
	```
17. Как изменить контекст функции
	```
	function fn () {
		return this
	}
	
	const obj = {name: "Aleksey"}
	const newFn = fn.bind(obj)
	const newFn = fn.call(obj, arg1, arg2) // Параметры передаются в виде перечисления
	const newFn = fn.apply(obj, [arg1, arg2]) // Параметры передаются в виде массива
	console.log(newFn()) // {name: "Aleksey"}
	```
18. Тернарный оператор
	```
	let result = condition ? result1 : result2 // где result1 - если condition === true, 
	result2 - если condition === false
	```
19. Деструктуризация  
	Это синтаксис присваивания, при котором можно разбив объект или массив на части, присвоить их разным переменным
	```
	const arr = ["Hello", "world"]
	const [greet, who] = arr
	console.log(greet, who) // Hello world
	```
	```
	const card = {car: "Volvo", year: "1956", transmission: "MT"}
	const {car, year, transmission} = card
	console.log(car, year, transmission) // Volvo 1956 MT
	```
20. Способы работы с асинхронным кодом
	- через функции callback
	- через Promise
	- с использованием async/await
21. e.preventDefault() и e.stopPropagination() применение
	```
	const handleSubmit = (e) => {
		e.preventDefault() // Отменяет стандартное поведение браузера при событии submit
		<..>
	}
	```
	```
	<div onclick=alert('Всплытие')>
		<button onclick="event.stopPropagination()" >Click me</button> // stopPropagination - 
		предотвращает всплытие события при вызове
	</div>
	```
22. Отслеживание и обработка ошибок
	 ```
	try {
		<..>
	} catch(err) {
		// Код выполняется если в try ошибка
	} finally {
		// Код выполняется в любом случае
	}
	```
23.  DOM дерево
		```
		<html>
			<body>
				<main>
				</main>
			</body>
		</html>
		```
24.  Все ли является объектом в js ?
	В какой то степени да.
	Ведь если обратиться к примитиву через точку то в этот момент 
	произойдет боксинг (boxing) и анбоксинг (unboxing), то есть примитив 
	превратиться в объект-обертку и обратно после выполнения выражения
	
	```
	const str = "qwerty"
	console.log(str.__proto__ === String.prototype) //true
	```


25. Прототипное наследование  
	Каждый объект обладает proto ссылающимся на prototype. В prototype который можно добавлять свои кастомные свойства. 
	Таким образом при создании объекта на основе прототипа со своими свойствами, получаем объект с унаследованными свойствами.

	proto - ссылается на prototype создателя
	prototype - есть либо у class либо у функции конструкторов "под капотом это одно и тоже"

	```
	const obj ={}
	console.log(obj.__proto__ === Object.prototype) //true

	class Person {
  		constructor(name, age) {
    		this.name = name;
    		this.age = age;
  		}

  		sayHello() {
    		console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  		}
	}
	const john = new Person('John', 25);

	console.log(john.__proto__ === Person.prototype) //true
	console.log(Person.__proto__ === Function.prototype) //true
	console.log(Function.__proto__ === Function.prototype) //true
	console.log(Function.__proto__.__proto__ === Object.prototype) //true

	```
	
26. Получение свойства объекта
	```
	const obj = {name: "Stas"}
	console.log(obj.name) // Stas
	console.log(obj['name']) // Stas
	```
