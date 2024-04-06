# 12.1 함수란?

> 함수란 일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것
> 
- 매개변수(parameter): 함수 내부로 입력을 전달받는 변수
- 인수(argument): 입력
- 출력(return value): 반환값

  
![image](https://github.com/rachaen/modern-javascript/assets/78066837/cf29b100-24b9-4cf7-b441-4c52dad9b671)


- 함수는 함수 정의를 통해 생성한다.
    
    ```jsx
    function add(x,y) {
    		return x + y;
    }
    ```
    
- 함수를 실행하기 위해서는 함수 호출을 통해 명시적으로 지시해야한다.
    
    ```jsx
    // 함수 호출
    var result = add(2, 5);
    
    // 함수 add에 인수 2, 5를 전달하면서 호출하면 반환값 7을 반환한다.
    console.log(result); // 7
    ```
    

# 12.2 함수를 사용하는 이유

1. **코드의 재사용성**: 동일한 작업을 반복적으로 수행했을 때 미리 정의된 함수를 재사용하는 것이 효율적
2. **유지보수의 편의성 및 코드의 신뢰성 증가:** 코드 수정의 중복 횟수를 줄이고 실수를 줄임
3. 코드의 가독성 향상: 함수 이름을 통해 내부 코드를 이해하지 않고도 함수의 역할을 파악할 수 있게 도움

# 12.3 함수 리터럴

> 함수는 객체타입이기 때문에 함수 리터럴로 생성할 수 있다.
> 

```jsx
// 변수에 함수 리터럴을 할당
var f = function add(x, y) {
    return x + y;
};
```

함수 리터럴의 구성요소

- 함수 이름
    - 함수 이름은 식별자다. 따라서 식별자 네이밍 규칙을 준수해야 한다.
    - 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자다.
    - 함수 이름은 생략할 수 있다. 이름이 있는 함수를 기명 함수, 이름이 없는 함수를 무명/익명 함수라 한다.
- 매개변수 목록
    - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분한다.
    - 각 매개변수에는 함수를 호출할때 지정한 인수가 순서대로 할당된다.
    - 매개변수는 함수 몸체 내에 변수와 동일하게 취급된다. 따라서 매개변수도 식별자 네이밍 규칙을 준수해야한다.
- 함수 몸체
    - 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행 단위로 정의한 코드 블록이다.
    - 함수 몸체는 함수 호출에 의해 실행된다.

리터럴은 값을 생성하기 위한 표기법인데 함수 리터럴도 평가되어 값을 생성한다. 즉, 함수는 객체다

함수는 객체지만 일반 객체와는 다르게 함수는 호출할 수 있다. 그리고 일반 객체에는 없는 함수 객체만의 고유한 프로퍼티를 갖는다.

# 12.4 함수 정의

> 함수 정의란 함수를 호출하기 이전에 인수를 전달받을 매개변수와 실행할 문들, 그리고 반환할 값을 지정하는 것을 말한다
> 

함수를 정의하는 방법에는 함수 선언문, 함수 표현식, Function 생성자 함수, 화살표 함수(ES6) 4가지가 있다.

## 12.4.1 함수 선언문

```jsx
function add(x,y) {
 	return x + y;
}

// 함수 참조
// console.dir은 console.log와는 달리 함수 객체의 프로퍼티 까지 출력한다.
// 단 node.js 환경에선느 console.log와 같은 결과가 출력된다.
console.dir(add); // f add(x, y)

// 함수 호출
console.log(add(2, 5)); // 7
```

함수 선언문은 함수 리터럴 형태가 동일하다.

단, 함수 선언 문은 함수 이름을 생략할 수 없다.

```jsx
function (x,y) {
 	return x + y;
}
// SyntaxError: Function statements require a function name
```

함수 선언문은 표현식이 아닌 문이다. 표현식이 아닌 문은 값으로 평가될 수 없으므로 변수에 할당할 수 없지만 다음 예제는 함수 선언문이 변수에 할당되는 것 처럼 보인다

```jsx
// 함수 선언문은 표현식이 아닌 문이므로 변수에 할당할 수 없다.
// 하지만 함수 선언문이 변수에 할당되는 것처럼 보인다.
var add = function add(x, y) {
    return x + y;
};

// 함수 호출
console.log(add(2, 5)); // 7
```

이렇게 동작하는 이유는 자바스크립트 엔진이 코드 문맥에 따라 동일한 함수 리터럴을 두 가지의 경우로 나눠서 해석하기 때문이다.

- 표현식이 아닌 문인 함수 선언문으로 해석하는 경우
- 표현식인 문인 함수 리터럴 표현식으로 해석하는 경우

```jsx
// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() {
    console.log("foo");
}
foo(); // foo
```

```jsx
// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() { console.log('foo') };
foo(); // foo

// 함수 리터럴을 피연산자로 사용하면 삼수 선언문이 아니라 함수 리터럴 표현식으로 해석된다.
// 함수 리터럴에서는 함수 이름을 생략할 수 있다.
(function bar() { console.log('bar') } );
bar(); // ReferenceError: bar is not defined
```

함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자 ⇒ 함수 몸체 외부에서는 함수 이름으로 함수를 호출할 수 없다.

함수는 함수이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다. 즉, 함수 선언문으로 생성한 함수는 함수 이름 add가 아니라 자바스크립트 엔진이 암묵적으로 생성한 식별자 add인 것이다.

```jsx
// 함수 선언문 의사코드 => 선언 문이 변환 되면 식별자 add가 생긴다.
var add = function add(x,y) {
  return x + y;
  };

console.log(add(2,5)); // 7
```

## 12.4.2 함수 표현식

> 값의 성질을 갖는 객체를 일급 객체라 하는데 자바스크립트의 함수는 일급 객체이기 때문에 함수를 값처럼 자유롭게 사용할 수 있다.

함수 리터럴로 생성한 함수 객체를 변수에 할당한 함수 정의 방식을 함수 표현식이라 한다.
> 

```jsx
var add = function(x, y) { // 익명함수
  return x + y;
};

console.log(add(2, 5)); // 7
```

함수를 호출할때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다.

```jsx
var add = function foo(x, y) {
  return x + y;
};

console.log(add(2, 5)); // 7

// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

## 12.4.3 함수 생성 시점과 함수 호이스팅

```jsx
console.dir(add) // f add(x,y)
console.dir(sub); // undefined

console.log( add(2,5) ); // 7
console.log( sub(2,5) ); // TypeError: sub is not a function

// 함수 선언문
function add(x,y) {
  return x + y;
}

// 함수 표현식
var sub = function(x,y) {
 return x - y;
}
```

- 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있다.
- 함수 표현식으로 정의한 함수는 함수 표현식 이전엔 호출할 수 없다.

⇒ 각각 정의한 함수의 생성 시점이 다르기 때문이다.

코드가 실행되기 시작하는 런타임에는 이미 함수 객체가 생성되어 있고 함수 이름과 동일한 식별자에 할당까지 완료된 상태다. 따라서 함수 선언문 이전에 함수를 참조할 수 있으며 호출할 수도 있는데, **코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅이라 한다.**

- 함수 선언문: 표현식이 아닌 문으로 함수 호이스팅에 의해 어디서든 호출된다.
- 함수 표현식: 표현식인 문으로 변수 호이스팅이 발생하여 할당문이 실행되는 시점에 함수 객체가 된다.

함수 호이스팅은 함수를 호출하기 전에 반드시 함수를 선언해야 한다는 당연한 규칙을 무시한다. 이 같은 문제 때문에 JSON을 창안한 더글라스 크락포드는 **함수 선언문 대신 함수 표현식을 사용**할 것을 권장한다.

## 12.4.4 Function 생성자 함수

> 자바스크립트가 기본 제공하는 빌트인 함수인 Function 생성자 함수에
> 
> 
> 매개변수 목록과 함수 몸체를 문자열로 전달하면서
> 
> new 연산자와 함께 호출하면 함수 객체를 생성해서 반환한다.
> 

생성자 함수는 객체를 생성하는 함수를 말한다. 아래는 Function 생성자 함수로 함수를 생성하는 예시이다.

```jsx
var add = new Function('x', 'y', 'return x+y'); // new 연산자 없이 사용해도 결과는 동일

console.log(add(2,5)); // 7
```

- Function 생성자 함수로 함수를 생성하는 것은 바람직하지 않다
    - 클로저를 생성하지 않는다.
    - 함수 선언문이나 함수 표현식으로 생성한 함수와 다르게 동작

```jsx
var add1 = (function () {
  var a = 10;
  return function(x,y) {
    return x + y + a;
  }
};
}());
console.log(add1(1,2)); // 13

var add2 = (function () {
  var a = 10;
  return new Function('x', 'y', 'return x+y+a;');
}());
console.log(add2); // ReferenceError: a is not defined
```

## 12.4.5 화살표 함수

> ES6에서 도입된 화살표 함수는 function 키워드 대신 화살표 ⇒ 를 사용해 좀더 간략한 방법으로 함수를 선언할 수 있다.
> 
> 
> 화살표 함수는 항상 익명 함수로 정의한다.
> 

```jsx
const add = (x, y) => x + y;
console.log(add(2,5)); // 7
```

- 화살표 함수는 생성자 함수로 사용할 수 없으며, 기존 함수와 this 바인딩 방식이 다르고, prototype 프로퍼티가 없으며, arguments 객체를 생성하지 않는다.

# 12.5 함수 호출

> 함수는 함수를 기리키는 식별자와 한쌍의 소괄호인 함수 호출 연산자로 호출한다.
> 

함수 호출 연산자 내에는 0개 이상의 인수를 쉼표로 구분해서 나열한다.

함수를 호출하면 현재 실행 흐름을 중단하고 호출된 함수로 실행 흐름을 옮긴다.

이때 매개변수에 인수가 순서대로 할당되고 함수 몸체의 문들이 실행된다.

## 12.5.1 매개변수와 인수

> 함수를 실행하기 위해 필요한 값이 있는 경우 매개변수를 통해 인수를 전달한다. 인수는 값으로 평가될 수 있는 표현식이어야한다. 인수는 함수를 호출할때 지정하며, 개수와 타입에 제한이 없다.
> 

```jsx
function add(x,y) {
  return x + y;
}

var result = add(1,2);
```

매개 변수는 함수를 정의할 때 선언하며, 함수 몸체 내부의 변수와 동일하게 취급된다. 즉, 함수가 호출되면 함수 몸체 내에서 암묵적으로 매개변수가 생성되고 매개변수와 마찬가지로 암묵적으로 undefined로 초기화된 이후 인수가 순서대로 할당된다.

```jsx
function add(x,y) {
  console.log(x,y); // 2 5
  return x + y;
}

add(2,5);

// 매개변수의 스코프(유효범위)는 함수 내부다.
// add 함수의 매개변수 x, y는 함수 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined
```

```jsx
// 함수는 매개변수의 개수와 인수의 개수가 일치하는지 체크하지 않는다. 
// 인수가 부족해서 인수가 할당되지 않은 매개변수의 값은 undefined다.
function add(x,y) {
  return x + y;
}

console.log(add(2)); // NaN
```

```jsx
// 매개변수보다 인수가 더 많은 경우 초과된 인수는 무시된다.

function add(x,y) {
  return x + y;
}

console.log(add(2, 5, 10)); // 7
```

```jsx
// 사실상 초과된 인수가 그냥 버려지는 것은 아니고, 모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관된다.
function add(x,y) {
  console.log(arguments);
  // Arguments(3) [2,5,10, callee: f, Symbol(Symbol.iterator): f]
  return x + y;
}

add(2, 5, 10);
```

## 12.5.2 인수 확인

```jsx
function add(x, y) {
 return x + y;
}
console.log(add(2)); // NaN
console.log(add('a','b')); // 'ab'
```

- 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않는다
- 자바스크립트는 동적 타입 언어이기 때문에 매개변수의 타입을 사전에 지정할 수 없다.

```jsx
// 타입 확인

function add(x, y) {
 if(typeof x !== 'number' || typeof y !== 'number) {
  throw new TypeError('인수는 모두 숫자 값이어야 합니다.');
 }
 return x + y;
}
console.log(add(2)); // TypeError: 인수는 모두 숫자 값이어야 합니다.
console.log(add('a','b'));  // TypeError: 인수는 모두 숫자 값이어야 합니다.
```

```jsx
// 기본값 설정

function add(a = 0, b = 0, c = 0) {
    return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

ES6에서 도입된 매개변수 기본값을 사용하면 인수를 전달하지 않았을 경우와 undefined를 전달했을때 유용하다.

## 12.5.3 매개변수의 최대 개수

> 매개변수가 많다는 것은 함수가 여러 가지 일을 한다는 증거이므로 바람직하지 않다. **이상적인 함수는 한 가지 일만 해야 하며 가급적 작게 만들어야 한다.**
> 

```jsx
$.ajax({
    method: "POST",
    url: "/user",
    data: { id: 1, name: "Lee" },
    cache: false,
});
```

많은 매개변수가 필요하다면 하나의 매개변수를 선언하고 객체를 인수로 전달하는 것이 유리하다. 객체를 인수로 사용하는 경우 프로퍼티 키만 정확히 지정하면 매개변수의 순서를 신경 쓰지 않아도 된다.

주의해야 할 점은 함수 외부에서 함수 내부로 전달한 객체를 함수 내부에서 변경하면 함수 외부의 객체가 변경되는 부수 효과가 발생한다.

## 12.5.4 반환문

> 함수는 return 키워드와 표현식(반환값)으로 이뤄진 반환문을 사용해 실행 결과를 함수 외부로 반환할 수 있다.
> 

반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나간다. 따라서 반환문 이후에 다른 문이 존재하면 무시한다.

```jsx
function multiply(x, y) {
    return x * y; // 반환문
    // 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
    console.log("실행되지 않는다.");
}

console.log(multiply(3, 5)); // 15
```

반환문은 return 키워드 뒤에 오는 표현식을 평가해 반환한다. return 키워드 뒤에 반환값으로 사용할 표현식을 명시적으로 지정하지 않으면 undefined가 반환된다.

```jsx
 function foo() {
   return;
}

console.log(foo()); // undefined
```

반환문은 생략할 수 있다. 이때 함수는 함수 몸체의 마지막 문장을 실행한 후 암묵적으로 undefined를 반환한다.

```jsx
function multiply(x, y) {
    // return 키워드와 반환값 사이에 줄바꿈이 있으면
    return // 세미콜론 자동 삽입 기능(ASI)에 의해 세미콜론이 추가된다.
    x * y; // 무시된다.
}

console.log(multiply(3, 5)); // undefined
```

return 키워드와 반환값으로 사용할 표현식 사이에 줄바꿈이 있으면 세미콜론 자동 삽입 기능에 의해 세미콜론이 추가되어 의도치 않은 결과가 발생할 수 있다.

```html
<!DOCTYPE html>
<html><body><script>
      return; // SyntaxError: Illegal return statement
    </script></body></html>
```

반환문은 함수 몸체 내부에서만 사용할 수 있다. 전역에서 반환문을 사용하면 문법 에러(SynTaxError: Illegal return statement)가 발생한다.

# 12.6 참조에 의한 전달과 외부 상태의 변경

> 매개변수도 함수 몸체 내부에서 변수와 동일하게 취급되므로 매개변수 또한 타입에 따라 값에 의한 전달, 참조에 의한 전달 방식을 그대로 따른다.
> 

```jsx
// 매개변수 primitive는 원시 값을 전달 받고, 매개변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj){
 primitive += 100;
 obj.name = 'Kim';
}

// 외부상태
var num = 100;
var person = { name : "lee" };

console.log(num); // 100
console.log(person); // {name: "lee" }

// 원시값은 값 자체가 복사되어 전달되고 객체는 참조 값이 복사되어 전달된다.
changeVal(num, person);

// 원시값은 원본이 훼손되지 않는다
console.log(num); // 100

// 객체는 원본이 훼손된다.
console.log(person); // { name: "kim" }
```

복잡한 코드에서 의도치 않은 객체의 변경을 추적하는 것은 어려운 일이다. 객체의 변경을 추적하려면 옵저버 패턴 등을 통해 객체를 참조를 공유하는 모든 이들에게 변경 사실을 통지하고 이에 대처하는 추가 대응이 필요하다.

이러한 문제를 해결하는 방법중에 하나는 객체를 불변 객체로 만들어 사용하는 것이다. 객체를 완전히 복사(깊은복사)하여 새로운 객체를 생성하고 재할당을 통해 교체한다. 이와 같은 방법으로 부수효과를 없앨 수 있다.

# 12.7 다양한 함수의 형태

## 12.7.1 즉시 실행 함수

> 함수 정의와 동시에 즉시 호출되는 함수를 즉시 실행 함수(IIFE)라고 한다. 단 한 번만 호출되며 다시 호출할 수 없다.
> 

```jsx
// 익명 즉시 실행 함수
(function () {
    var a = 3;
    var b = 5;
    return a * b;
})();

// 기명 즉시 실행 함수
(function foo() {
  var a = 3; 
  var b = 5;
  return a + b;
}());

foo(); // ReferenceError: foo is not defined
```

즉시 실행함수는 반드시 그룹 연산자(…)로 감싸야한다. 그렇지 않으면 에러가 발생한다

## 12.7.2 재귀 함수

> 함수가 자기 자신을 호출하는 것을 재귀 호출이라한다.
> 

```jsx
function countdown(n) {
    if (n < 0) return;
    console.log(n);
    countdown(n - 1); // 재귀 호출
}

countdown(10);
```

재귀 함수는 **반드시 탈출 조건을 가지고 있어야 한다.** 탈출 조건이 없는 경우 함수가 무한 호출되어 **스택 오버플로우가 발생**한다.

## 12.7.3 중첩 함수

함수 내부에 정의된 함수를 중첩 함수 또는 내부 함수라 한다. 그리고 중첩 함수를 포함하는 함수는 외부 함수라 부른다.

중첩 함수는 외부 함수 내부에서만 호출할 수 있다. 일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수의 역할을 한다.

```jsx
function outer(){
  var x = 1;
 
  // 중첩 함수
  function inner(){
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x+y); // 3
  }
  inner();
}
outer();
```

## 12.7.4 콜백 함수

> 콜백함수는 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 말한다. 또한 변수를 통해서 함수 외부에서 콜백 함수를 전달 받은 함수를 고차함수라 한다.
> 

```jsx
// 외부에서 전달받은 f를 n만큼 반복 호출한다
function repeat(n, f) {
    for (var i = 0; i < n; i++) {
        f(i); // i를 전달하면서 f를 호출
    }
}

var logAll = function (i) {
    console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
    if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3
```

고차함수는 콜백 함수를 자신의 일부분으로 합성한다.

```jsx
// 콜백 함수를 사용하는 고차 함수 map
var res = [1, 2, 3].map(function (item) {
    return item * 2;
});

console.log(res); // [2, 4, 6]

// 콜백 함수를 사용하는 고차 함수 filter
res = [1, 2, 3].filter(function (item) {
    return item % 2;
});

console.log(res); // [1, 3]

// 콜백 함수를 사용하는 고차 함수 reduce
res = [1, 2, 3].reduce(function (acc, cur) {
    return acc + cur;
}, 0);

console.log(res); // 6
```

## 12.7.5 순수 함수와 비순수 함수

> 함수형 프로그래밍에서는 어떤 외부 상태에 의존하지도 않고 변경하지도 않는, 즉 부수 효과가 없는 함수를 **순수 함수**, 외부 상태에 의존하거나 외부 상태를 변경하는, 즉 부수 효과가 있는 함수를 **비순수 함수** 라고 한다.
> 

```jsx
var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
    return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2
```

- 순수 한수는 동일한 인수가 전달되면 언제나 동일한 값을 반환하는 함수다.
- 순수 함수는 일반적으로 최소 하나 이상의 인수를 전달받는다.
- 순수 함수는 인수를 변경하지 않는 것이 기본이다. ⇒ 순수 함수는 인수의 불변성을 유지한다.
- 순수 함수는 함수의 외부 상태를 변경하지 않는것이다 ⇒ 어떤 외부 상태에도 의존하지 않으며 외부 상태를 변경하지도 않는 함수다.

```jsx
var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화한다.

// 비순수 함수
function increase() {
    return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```
