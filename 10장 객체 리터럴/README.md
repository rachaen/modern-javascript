# 10.1 객체란?

> 자바스크립트는 객체 기반의 프로그래밍 언어이다.
> 
- 객체 타입은 다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조
- 객체는 변경 가능한 값
- 객체는 0개 이상의 프로퍼티로 구성된 집합
- 프로퍼티: 키와 값으로 구성으로 객체의 상태를 나타내는 값
- 메서드: 프로퍼티를 참조하고 조작할 수 있는 동작

# 10.2 객체 리터럴에 의한 객체 생성

> 자바스크립트는 프로토타입 기반 객체지향 언어로 다양한 객체 생성 방법을 지원
> 
- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

객체 리터럴은 중괄호({…}) 내에 0개 이상의 프로퍼티를 정의한다.

```jsx
var person = {
 name: 'Lee',
 sayHello: function() {
	 console.log(`hello My name is ${this.name}.`);
	}
};

var empty = {}; // 빈 객체
```

# 10.3 프로퍼티

> 객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다
> 

```jsx
const person = {
  // 프포러티 키는 name, 프로퍼티 값은 'Lee'
  name: 'Lee',
  // 프포러티 키는 age, 프로퍼티 값은 20
  age: 20,
};
```

- 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값

```jsx
const name = {
  firstName: 'Chae-eun', // 식별자 네이밍 규칙 준수하는 키
  'last-name': 'Lee', // 식별자 네이밍 규칙 준수하지 않는 키
  //last-name: 'Lee' // SyntaxError: Unexpected token -
};
```

- 키가 식별자 네이밍 규칙을 준수하면 따옴표를 생략할 수 있다.

```jsx
const obj = {};
const key = "hello";

// ES5: 프로퍼티 키 동적 생성
obj[key] = "world";
// 'world'
// ES6: 계산된 프로퍼티 이름
// const obj = {[key]: 'world'}
console.log(obj);
// {hello:'world'}
```

- 프로퍼티 키로 사용할 표현식을 대괄호로 묶음으로서 프로퍼티 키를 동적으로 생성할 수 있다.

```jsx
var foo = {
  0: 1,
  1: 2,
  2: 3,
},
console.log(foo); // {0: 1, 1: 2, 2: 3}
```

- 프로퍼티 키에 문자열이나 삼벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.

```jsx
var foo ={
   name: 'Lee',
   name: 'Kim',
};
console.log(foo); // {name: 'kim'}
```

- 이미 존재하는 프로퍼티 키를 중복 사용하면 나중에 선언한 프로퍼티가 먼저 선언된 프로퍼티를 덮어쓴다. 이 것은 에러가 발생하지 않으니 주의해야한다.

# 10.4 메서드

> 메서드는 객체에 묶여 있는 함수를 의미한다.
> 

```jsx
var circle = {
	radius: 5, // 프로퍼티
  // 원의 지름
	getDiameter: function (){ // 메서드
		return 2 * this.radius; // this는 circle를 가리킨다.
 }
};
```

# 10.5 프로퍼티 접근

> 프로퍼티에 접근하는 방법은 마침표 표기법(.)과 대괄호 표기법([…]) 두 가지다.
> 

```jsx
const person = {
  name: 'Lee',
};

// 마침표 표기법에 의한 접근
console.log(person.name); // Lee

// 대괄호 표기법에 의한 접근
console.log(person['name']); // Lee
```

- 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.

```jsx
const person = {
  name: "ChaeEun",
};

console.log(person[name]); //ReferenceError: name is not defined
```

- 따옴표로 감싸지 않아 자바스크립트 엔진은 식별자로 해석해서 `ReferenceError`가 발생했다.

```jsx
const obj = {};
console.log(obj.a); //undefined
```

- 객체에 존재하지 않는 프로퍼티에 접근하면 `undefined`를 반환한다.

# 10.6 프로퍼티 값 갱신

> 이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.
> 

```jsx
const person = {
  name: 'Lee',
};

person.name = 'Kim';
console.log(person); // {name:'Kim'}
```

# 10.7 프로퍼티 동적 생성

> 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.
> 

```jsx
const person = {
  name: "Lee",
};

person.age = 20;
console.log(person); // {name:'Lee', age:20}
```

# 10.8 프로퍼티 삭제

> delete 연산자는 객체의 프로퍼티를 삭제한다.
> 
- delete 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.
- 만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러 없이 무시된다.

```jsx
const person = {
  name: 'Lee',
  age: 20,
};

// person 객체에 age 프로퍼티가 존재하여 삭제할 수 있다.
delete person.age; // true

// person 객체에 address 프로퍼티가 존재하지 않는다.
// 삭제할 수 없지만 에러는 발생하지 않는다.
delete person.address; // true
console.log(person); // { name: 'Lee' }
```

# 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

## 10.9.1 프로퍼티 축약 표현

> ES6에서는 프로퍼티의 값을 변수를 사용하는 경우 프로퍼티의 키가 변수명과 같으면 이를 축약해서 나타낼 수 있다.
> 

```jsx
// ES5
var x = 1; y = 2;
var obj = {
  x: x,
  y: y
};

console.log(obj); // {x: 1, y: 2}

// ES6
var x = 1; y = 2;
var obj = {x,y};

console.log(obj); // {x: 1, y: 2}
```

- 프로퍼티 키는 변수 이름으로 자동 생성된다.

## 10.9.2 계산된 프로퍼티 이름

> 대괄호 [ ] 를 사용하면 객체 리터럴 상에서 표현식의 `평가값`을 `키`로 사용할 수 있다.
> 

```jsx
// ES5

var prefix = 'prop';
var i = 0;

var obj = {};

// 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}

// ES6
var prefix = 'prop';
var i = 0;

/ // 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
var obj = {};
obj[`${prefix}-${++i}`] = i;
obj[`${prefix}-${++i}`] = i;
obj[`${prefix}-${++i}`] = i;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

- 객체 리터럴 안의 프로퍼티 키가 대괄호[ ]로 둘러싸여 있다면, 이를 `계산된 프로퍼티`(computed property) 라고 부른다.

## 10.9.3 메서드 축약 표현

> `ES6`에서는 메서드를 정의할 때 `function 키워드를 생략`한 축약 표현을 사용할 수 있다.
> 

```jsx
// ES5
var obj = {
 name: 'Lee',
 sayHi: function(){ console.log('hi' + this.name); };
};

obj.sayHi(); // hi Lee

// ES6
var obj = {
 name: 'Lee',
 sayHi(){ console.log('hi' + this.name); };
};

obj.sayHi(); // hi Lee
```
