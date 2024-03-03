# 08장 제어문

> 제어문은 조건에 따라 코드 블록을 실행하거나 반복할 때 사용한다.

하지만 위에서 아래로 실행되는 코드의 흐름을 제어하여 코드의 흐름을 혼란스럽게 할 수 있다. 때문에 고차 함수를 사용하여 이를 해결하고, 복잡성을 줄일 수 있어야 한다.
> 

# 08-1 제어문의 종류

### 블록문

- 0개 이상의 문을 중괄호로 묶은 것으로 코드 블록, 블록이라고 부른다.
- 하나의 실행 단위

```jsx
// 블록문
{ 
	var foo = 10;
}

// 제어문
var x = 0;
if(x < 10){
	x++;
}

// 함수 선언문
function sum(a, b){
	return a + b;
}

```

### 조건문

- 주어진 조건의 평가 결과에 따라 코드 블록의 실행을 결정한다.
- switch문은 지원하지 않는 언어도 있고, if…else문의 비해 문법이 복잡하다.
때문에 조건이 많고, switch 문을 사용했을 때 가독성이 좋을 것 같을 때만 switch문을 고려해보자.

1. if… else 문 , 삼항 조건 연산자
    
    ```jsx
    var num = 2;
    var kind;
    
    //if...else문
    if(num > 0) {
    	kind = 'plus';
    }else if(num < 0){
    	kind = 'minus';
    }else{
    	kind = 'zero'
    }
    
    //삼항 조건 연산자, 0은 false로 취급
    var kind = num ? (num > 0 ? 'plus' : 'minus') : 'zero';
    // kind === 'plus'
    ```
    
2. switch 문
    - switch문은 표현식을 평가하여 그에 맞는 case문을 실행한다.
    - 각각의 case에 break를 작성하지 않으면 폴스루가 발생한다.
    - 여러가지 조건을 묶어서 사용할 때 폴스루를 활용할 수 있다.
    
    ```jsx
    var num = 1;
    var fruitName;
    
    switch (num) {
    	case 0 : fruitName = 'apple';
    		break;
    	case 1 : fruitName = 'banana';
    		break;
    	case 2 : fruitName = 'cherry';
    		break;
    	default : fruitName = 'etc';
    }
    console.log(fruitName); // banana
    
    // 폴스루 발생시 발생하는 문제
    switch (num) {
    	case 0 : fruitName = 'apple';
    	case 1 : fruitName = 'banana';
    	case 2 : fruitName = 'cherry';
    
    	default : fruitName = 'etc';
    }
    console.log(fruitName); // etc
    
    // 폴스루 활용
    var month = 2;
    var days = 0;
    
    switch (month) {
    	case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    		days = 31;
    		break;
    	case 4 :case 6: case 9: case 11:
    		days = 30;
    		break;
    	case 2:
    		//윤년 계산 알고리즘 
    		days = 윤년계산 ? 28 : 29
    		break;
    	default :
    		console.log('Invalid month');
    }
    
    ```
    

### 반복문

- 조건식의 평가 결과가 true일 경우 코드 블록을 실행하고, 조건식이 false일 때까지 반복한다.

1. for 문
    
    ```jsx
    for(var i = 0; i < 2; i++){
    	console.log(i);
    }
    //0
    //1
    
    //무한루프
    for(;;) { ... } 
    ```
    

1. while 문
    
    ```jsx
    var count = 0;
    
    while(count < 3) {
    	console.log(count); // 0 1 2
    	count++;
    }
    console.log(count); // 3
    
    // 무한루프
    while(true) { ... }
    ```
    
2. do… whlie문
    - 무조건 한 번 실행된다.
    - do 블록문 안에 실행할 내용을 작성.
    
    ```jsx
    var count = 0;
    
    do {
    	console.log(count); // 0 1 2 
    	count++;
    
    } while(count < 3);
    
    console.log(count); // 3
    	
    ```
    

# 08-2 break, continue

### break

- 레이블문, 반복문, switch문 탈출할 수 있다.
- 이 외에 사용 시 문법 에러가 발생한다.

```jsx

// 레이블문, 반복문, switch문이 아닐 때
if(true) {
	break; // Uncaught SyntaxError: Illegal break statement
}

// 레이블문
foo: {
	console.log(1);
	break foo; // foo 레이블 블록문을 탈출한다.
	console.log(2);
}
console.log('done!');
// 1
// done!

// 반복문
var str = 'Hello~World';
var result = '';
for(var i = 0; i < str.length; i++){
	if(str[i] == '~') break;
	else result += str[i];
}
console.log(result);
// Hello
```

### continue

- 반복문에서 사용한다.
- continue는 break와 다르게 반복문을 탈출하는 것이 아닌 실행 흐름을 반복문의 증감식으로 이동시킨다.

```jsx
var str = 'Hello~World';
var result = '';

for(var i = 0; i < str.length; i++){
	if(str[i] == '~') continue;
	else result += str[i];
}
console.log(result);
// HelloWorld
```