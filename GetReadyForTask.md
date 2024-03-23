# Подготовка к собеседованию
## Tasks:

Road Map для изучения задачи: https://neetcode.io/roadmap

1. Реализовать методы, которые при вводе (2).plus(3).minus(1) дали бы на выходе 4.  
	*Для решения задачи необходимо расширить стандартный прототип Number и добавить в него собственные новые методы **plus** и **minus***
	```
	Number.prototype.plus  =  function (value) {
		return  this  +  value
	}

	Number.prototype.minus  =  function (value) {
		return  this  -  value
	}
	console.log((2).plus(3).minus(1))
	```
2. Последовательность вывода цифр
	```
	console.log(0);

	new Promise(() => {
		setTimeout(() =>  console.log(1), 500);
	})

	new Promise (() => {
		console.log(2)
	})

	new  Promise(() => {
		setTimeout(() =>  
			console.log(3), 0);
	})
	 
	console.log(4);
	```
	*Ответ: 0 2 4 3 1*