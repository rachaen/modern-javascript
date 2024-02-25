# 06장 데이터 타입

> JavaScript의 모든 값은 데이터 타입을 가지고, 데이터 타입을 통해 값의 종류가 정해진다.
또한 데이터 타입을 통해 변수에 할당되어야 하는 메모리 공간의 크기가 결정된다.

<br/>

# 06-1 데이터 타입이 왜 필요할까?

> 값은 메모리에 저장하고 참조할 수 있어야 한다. 
때문에 메모리에 저장되는 값의 공간을 확보해야 하고,
공간의 크기를 최소화해야 낭비와 손실을 줄일 수 있다.
> 
1. 값을 저장할 때 확보해야 하는 메모리 공간의 크기 결정
2. 값을 참조할 때 필요한 메모리 공간의 크기를 결정
3. 메모리에서 읽은 2진수를 어떻게 해석할지 결정 <br/>
    -> 메모리에서 0100 0001을 해석할 때 데이터 타입이 숫자라면 65, 문자열이라면 ‘A’

<br/>

# 06-2 데이터 타입의 종류

> JavaScript 데이터 타입에는 7종류가 있고, 크게 원시 타입과 객체 타입으로 나뉜다.


## 원시 타입

1. 숫자 타입 
    - JavaScript에서 숫자 타입은 한 개만 존재한다.
    - 모든 수를 실수로 처리하며 정수만을 표현하기 위한 데이터 타입은 없다.
    - 3가지의 특별한 값 Infinity, -Infinity, Nan이 있다.
    
    ```jsx
    var integer = 10;
    var double = 10.00;
    console.log(integer === double); // true
    
    var binary = 0b01000001; // 65의 2진수
    var octal = 0o101; // 65의 8진수
    var hex = 0x41 // 65의 16진수
    
    console.log(binary === octal); // true
    console.log(octal === hex); // true
    
    console.log(10 / 0); // Infinity
    console.log(10 / -0); // -Infinity
    console.log(1 * 'String'); // NaN
    ```
    
2. 문자열 타입
    - 문자열은 작은따옴표(’ ‘), 큰따옴표(” “), 백틱(``)으로 텍스트를 감싸서 사용한다.
    - ES6 부터 백틱(``)을 사용한 템플릿 리터럴이 추가되었다.
    이를 통해 멀티라인 문자열, 표현식 삽입, 태그트 템플릿 등 편리한 문자열 처리가 가능하다.
        
        
        **멀티라인 문자열**
        
        ```jsx
        // 일반 문자열
        var template = '<ul> \n\t <li><a href = "#">Home></li>\n</ul>';
        
        // 템플릿 리터럴
        var template = 
        `<ul>
        	<li><a href = "#"></a></li>
        </ul>`;
        
        //출력 결과는 아래와 동일하다
        <ul>
        	<li><a href = "#"></a></li>
        </ul>
        ```
        
        **표현식 삽입**
        
        ```jsx
        var first = "my name is";
        var last = "Lee";
        
        //ES5 문자열 연결
        console.log('Hi' + first + ' ' + last + '.');
        
        //ES6 표현식 삽입
        console.log(`Hi ${first} ${last} .`);
        
        //출력 결과는 아래와 동일하다
        Hi my name is Lee.
        
        //다음과 같이 계산식을 사용할 수 있다.
        console.log(`1 + 2 = ${1 + 2}`); // 3
        
        ```
        
    
3. 불리언 타입
    - 논리적 참, 거짓을 나타내는 값으로 true, false를 사용한다.
4. undefined 타입
    - 변수가 선언되면 암묵적으로 undefined로 초기화된다.
    - 만약 변수에 값이 없다는 걸 표시하고 싶다면 undefined보단 null을 할당하는 것이 좋다.
5. null 타입
    - 변수에 값이 없다는 것을 의도적으로 명시할 때 사용한다.
6. 심벌 타입
    - ES6에서 추가된 타입으로, 다른 값과 중복되지 않는 유일무이한 값이다.
    
    ```jsx
    var key = Symbol('key');
    console.log(typeof key) // symbol
    
    //객체에서 충돌할 위험이 없는 symbol 값을 프로퍼티 키로 이용할 수 있다.
    var obj = {};
    obj[key] = 'value';
    ```
    

## 객체 타입

- 객체 타입은 6가지의 원시 타입을 제외한 것들이며 객체, 함수, 배열 등이 있다.

<br/>

# 06-3 동적 타이핑

## 정적 타입 언어

- C, Java와 같은 정적 타입 언어는 변수를 선언할 때 타입을 선언되고, 변수의 타입을 변경할 수 없다.
- 컴파일 시점에 타입 체크를 수행하고, 선언한 데이터 타입에 맞는 값이 할당되었는지 검사한다.
- <span style="color:DarkGreen; background-color:#F1F1EF;"> 타입 에러로 인한 문제를 초기에 잡을 수 있다.</span>
- <span style="color:Crimson; background-color:#F1F1EF;">매번 코드 작성 시 타입을 결정해야 하여 유연성이 낮음 </span>

## 동적 타입 언어

- var, let, const 키워드를 사용해 변수를 선언할 뿐, 타입을 선언하지 않는다.
- 선언이 아닌 할당에 의해 타입이 결정되고, 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다.
- <span style="color:DarkGreen; background-color:#F1F1EF;"> 런타임까지 타입에 대한 결정을 가지고 가기 때문에 유연성이 높다. </span>
- <span style="color:Crimson; background-color:#F1F1EF;">전역변수, 스코프에 의한 참조, 변경을 통해 의도치 않은 오류가 발생할 수 있다.</span>

### 동적 타입 언어를 사용하며 주의할 점

1. 변수의 무분별한 사용하지 않기 (최소한으로 유지)
2. 변수의 유효 범위 (스코프)를 이해하고 최대한 좁게 만들어 오류 억제
3. 전역 변수는 최대한 사용하지 말기 
4. 변수보다는 상수를 사용해 값의 변경을 억제 → Const 키워드 사용
5. 변수의 네이밍은 항상 심사숙고하여 존재 이유를 파악할 수 있는 이름으로 만들기