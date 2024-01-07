---
title: "JavaScript 기초 다지기"
datePublished: Mon Jul 10 2023 15:00:00 GMT+0000 (Coordinated Universal Time)
cuid: clr3bh61c000209l27ffi5eee
slug: javascript-basic-study
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704621171153/3e700f1f-1202-411f-9551-2af56893fb40.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1704621207730/18cc0d95-c42e-4e79-a16c-3b83e4073aa6.png
tags: javascript, basics, study

---

# 생성자 함수

## 리터럴

- 리터럴: 변수에 넣는 변하지 않는 데이터 그 자체
  - 코드 상에서 데이터를 표현하는 방식
    - boolean, char, double, long, int 등
  - 변수를 선언함과 동시에 값을 지정해주는 표기법

```jsx
const name = 'Rarry' // name은 상수, Rarry는 문자열 리터럴
```

- 객체 리터럴: 객체를 생성하는 방법의 일종
  - 직접 속성명과 속성값을 문자로 적어서 객체를 정의하는 방식

```jsx
let user = { name: 'Kate', age: 20 }
```

## 생성자 함수란

- 생성자 함수: 비슷한 객체를 여러 개 만들 수 있는 함수

## 생성자 함수 사용 관례

- 함수명의 첫 번째 글자 대문자
- new 함수명()

## new 키워드를 붙여 함수 호출 시 발생하는 일

1. 빈 객체 먼들고 this에 할당
2. 함수의 본문을 실행하면서 this에 각 프로퍼티를 할당
3. this를 자동으로 반환

- new 키워드를 붙이지 않았을 시 해당 함수는 아무것도 return하지 않으므로 undefined

## 참조 가능/불가능 프로퍼티

- this에 연결되어 있는 프로퍼티와 메소드는 외부에서 참조 가능(public)
- 생성자 함수 내에서 this 없이 선언된 일반 변수는 생성자 함수 내부에서는 접근 가능하나 외부에서 참조 불가능(private)

## 생성자 함수의 메소드

- this에 프로퍼티 뿐만 아니라 메소드 역시 추가할 수 있음
- 메소드 내의 this는 생성자 함수가 생성할 객체를 가리킴

## 예시 코드

```jsx
function Person(name, age) {
  // this = {}
  this.name = name
  this.age = age
  const job = 'developer'

  this.sayMyJob = function () {
    console.log(this)
    console.log(`My job is ${job}`)
  }
  // return this
}

// new + 생성자 함수 Person()에 이름과 나이를 인자로 넣어서 객체 생성
const yuza = new Person('Yuza', 10)
console.log(yuza.name) // Yuza (public)
console.log(this.job) // undefined (private)
yuza.sayMyJob()
/*
	My job is developer
	Person{
    name: 'Yuza',
    age: 10,
		sayMyJob: ƒ ()
    [[Prototype]] : Object  
	}
*/
console.log(yuza)
/*
  Person{
    name: 'Yuza',
    age: 10,
		sayMyJob: ƒ ()
    [[Prototype]] : Object  
	}
*/

let yoon = User('Yoon', 25)
console.log(yoon) // undefined
```

## 생성자 함수의 return문

- 생성자 함수가 반환해야 할 것은 모두 this에 저장되며, this는 자동적으로 반환되므로 보통 생성자 함수에는 return문이 없음
- return문 사용 시
  - 객체를 return할 경우 this 대신 해당 객체가 반환됨
  - 원시형을 return할 경우 return문이 무시됨

```jsx
// 객체를 return하는 경우
function Person(name, age) {
  this.name = name
  this.age = age
  const job = 'developer'
  this.sayMyJob = function () {
    console.log(`My job is ${job}`)
  }

  return {
    name: 'Orange',
    age: 20,
    sayMyJob: function () {
      console.log(`My job is not ${job}, but actor`)
    },
  }
}

const yuza = new Person('Yuza', 10)
console.log(yuza.name) // Orange
yuza.sayMyJob() // My job is not developer, but actor

// --------------------------------------------------------------

// 원시형(문자열)을 return하는 경우
function Person(name, age) {
  this.name = name
  this.age = age
  const job = 'developer'
  this.sayMyJob = function () {
    console.log(`My job is ${job}`)
  }

  return 'Hello, World!'
}

const yuza = new Person('Yuza', 10)
console.log(yuza.name) // Yuza
yuza.sayMyJob() // My job is developer
```
# 프로토타입 객체

## 프로토타입 기반 객체지향

- 자바스크립트는 프로토타입 기반 객체지향 프로그래밍 언어 (cf. 클래스 기반 객체지향 프로그래밍 언어)
  - 클래스 기반 객체지향 프로그래밍 언어(Java, C++ 등)
    - 객체를 생성하기 위해 클래스를 정의하며 클래스를 통해 객체(인스턴스) 생성
  - 프로토타입 기반 객체지향 프로그래밍 언어
    - 클래스 없이 객체 생성 가능: 기존의 객체를 cloning하여 새로운 객체 생성 = 객체 원형인 프로토타입을 사용하여 새로운 객체 생성
    - 객체 리터럴: `const newObj = {name: 'Mary'}`
    - Object 생성자 함수: `const person = new Object();`
    - 생성자 함수: 프로퍼티가 동일한 객체 여러 개 간편하게 생성 가능

## 프로토타입 객체

- 프로로타입 객체
  - 함수를 정의하면 다른 곳에 생성되며 다른 객체의 원형이 되는 객체
    - 생성자 함수가 정의될 때 그 함수의 멤버로 존재하는 prototype 속성은 다른 곳에 생성된 함수의 프로토타입 객체 참조
      - 해당 프로토타입 객체는 생성자 함수로 생성한 모든 객체의 원형이 되며 모든 객체가 참조하게 됨
        - 프로토타입 객체 = 같은 원형으로 생성된 객체가 공통으로 참조하는 공간
      - 자식 객체는 해당 프로토타입 객체를 `__proto__` 프로퍼티로 접근 가능
    - 프로토타입 객체의 멤버인 constructor 속성은 생성자 함수를 참조

![Untitled](https://user-images.githubusercontent.com/67324487/227777371-876bd26a-0836-4224-9c53-43a0378a258a.png)

```jsx
function Person(name) {
  this.name = name
  this.sayHi = () => {
    console.log(`Hi, I'm ${this.name}`)
  }
}

const joon = new Person('Joon')

console.log(joon) // Person {name: 'Joon', sayHi: ƒ}
joon.sayHi() // Hi, I'm Joon
console.log(joon.__proto__) // {constructor: ƒ}
```

- 자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체(=프로토타입 객체)와 연결됨
  - 프로토타입 객체의 프로퍼티, 메소드를 상속받을 수 있음
- 프로토타입도 동적으로 멤버 추가 가능
  - 모든 자식 객체는 자신의 프로토타입 객체에 접근 가능하며 동적으로 추가된 멤버도 사용 가능
  - 멤버를 추가하기 전에 생성된 객체에서도 해당 멤버를 사용할 수 있음

![Untitled](https://user-images.githubusercontent.com/67324487/227777387-5e273ff1-936a-45d0-8263-3a23415bf330.png)

```jsx
function Person(name) {
  this.name = name
  this.sayHi = () => {
    console.log(`Hi, I'm ${this.name}`)
  }
}

const joon = new Person('Joon')

Person.prototype.sayGood = function () {
  console.log('Good~')
}

joon.__proto__.sayGood() // Good~
joon.sayGood() // Good~

console.log(Person.prototype === joon.__proto__) // true
```

# 프로토타입

- 프로토타입 객체로 인해 만들어진 객체 내부의 `__proto__` 프로퍼티는 자신의 원형인 프로토타입 객체를 참조하는 숨겨진 링크
- 프로토타입 = 이 숨겨진 링크

![Untitled](https://user-images.githubusercontent.com/67324487/227777404-7f9a7a51-8244-483a-839a-6619d667f42d.png)

- 생성자 함수의 prototype 프로퍼티: 자신과 이름이 같은 프로토타입 객체(=줄여서 프로토타입)를 참조
- 객체의 `__proto__` 프로퍼티: 자신을 생성한 프로토타입 객체를 참조하는 숨겨진 링크(=프로토타입)

# 프로토타입 체인

- 특정 객체의 프로퍼티나 메소드에 접근할 때 그 프로퍼티, 메소드가 없는 경우, 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티, 메소드를 차례로 검색하는 것

```jsx
const joon = {
  name: 'Joon',
}

console.log(joon.hasOwnProperty('name')) // true
console.log(joon.__proto__ === Object.prototype) // true
console.log(Object.prototype.hasOwnProperty('hasOwnProperty')) // true
```

![Untitled](https://user-images.githubusercontent.com/67324487/227777420-4b233dbf-a1d9-422b-80da-044fbc5f5aad.png)

## 객체 리터럴 방식으로 생성된 객체의 경우

- 객체 리터럴 방식 = 내장 함수인 Object() 생성자 함수로 객체 생성하는 것을 단순화한 것
- 함수 객체인 Object() 생성자 함수는 prototype 프로퍼티 존재

```jsx
const joon = {
  name: 'Joon',
}

console.log(joon.__proto__ === Object.prototype) // true
console.log(Object.prototype.constructor === Object) // true
console.log(Object.__proto__ === Function.prototype) // true
```

![Untitled](https://user-images.githubusercontent.com/67324487/227777434-48db0d10-2107-47f6-a778-2637d72631b9.png)

## 생성자 함수로 생성된 객체의 경우

- 생성자 함수의 정의 방식
  - 함수선언식
    - 함수 리터럴 방식(= Function() 생성자 함수로 함수를 생성하는 것을 단순화 시킨 것) 사용
    - 자바스크립트 엔진이 내부적으로 기명 함수표현식으로 변환함
    - `const sayHi = function hi() { return "Hi!" }`
  - 함수표현식
    - 함수 리터럴 방식 사용
    - `const sayHi = function() { return "Hi!" }`
  - Function() 생성자 함수
- 결국 세 가지 방식 모두 Function() 생성자 함수를 통해 함수 객체를 생성하는 것으로 수렴됨

![Untitled](https://user-images.githubusercontent.com/67324487/227777455-45bbc48d-5714-4ed0-93d3-478a898ac864.png)

![Untitled](https://user-images.githubusercontent.com/67324487/227777474-b3afd451-44b8-444f-b096-e8bd7f4bd8e2.png)

# Class의 정의

- 객체를 생성하기 위해 변수와 메소드를 정의하는 틀
- 함수의 한 종류
- 객체를 정의하기 위한 상태(멤버 변수)와 메소드(함수)로 구성됨
- 생성자 함수처럼 클래스를 사용해도 객체 생성 가능
  - 클래스는 ES6에 추가된 스펙
  - new를 통해 호출했을 때 클래스 내부에 정의된 내용으로 객체를 생성하는 것은 생성자 함수와 동일함

# 기본 문법

```jsx
class MyClass {
  constructor() { ... } // 생성자 메소드
  method1() { ... } // (일반)메소드
  method2() { ... }
  method3() { ... }
  ...
}

// --------------------------------------------------------------

class Person {
  constructor(name, age, job) {
      this.name = name;
      this.age = age;
      this.job = job;
  }
  sayMyJob() {
      console.log(`My job is ${this.job}`);
  }
}
const yuza = new Person('Yuza', 10, "writer");
console.log(yuza); // Person {name: 'Yuza', age: 10, job: 'writer'}
console.log(yuza.name); // Yuza
yuza.sayMyJob(); // My job is writer
```

- new 키워드를 붙여 클래스 호출 시 발생하는 일

1. 새로운 객체 생성됨
2. constructor가 자동으로 실행되며, 인자로 받은 값들을 `this.property`에 각각 할당함

- constructor는 객체를 만들고 초기화하기 위한 생성자 메소드로서 new를 통해 호출하면 자동으로 실행됨
- 객체를 초기화하기 위한 값이 정의됨
- 암묵적으로 this, 인스턴스를 반환함 → 내부에 return문이 있으면 안됨
- constructor가 없을 시 빈 constructor가 정의됨
- 위 코드에서 클래스 문법 구조가 하는 일
  1. Person이라는 이름의 함수를 만든 뒤, 함수의 내용물은 constructor(생성자 메소드)에서 가져옴
  - constructor가 없을 시 내용물 없이 함수가 만들어짐
  2. 클래스 내에서 정의한 메소드(ex. sayMyJob)를 `Person.prototype`에 저장
  - 클래스를 통해 객체를 만든 후 메소드를 호출하면 해당 메소드를 prototype 프로퍼티를 통해 가져와서 사용함
  - 위 코드의 경우 프로토타입에 메소드가 총 2개 존재(sayMyJob, constructor)

![Untitled](https://user-images.githubusercontent.com/67324487/226158447-3c3d929f-f7e1-4e61-8733-3d425dda8e78.png)

- 즉, 클래스는 해당 클래스의 프로토타입의 constructor(생성자 메소드)와 동일

# 클래스와 생성자 함수의 차이점

## 메소드가 저장되는 위치

```jsx
const Person1 = function (name, age, job) {
  this.name = name
  this.age = age
  this.sayMyJob = function () {
    console.log(`My job is ${job}`)
  }
}
const yuza = new Person1('Yuza', 10, 'teacher')
console.log(yuza) // Person1 {name: 'Yuza', age: 10, sayMyJob: ƒ}
yuza.sayMyJob() // My job is teacher

// --------------------------------------------------------------

class Person2 {
  constructor(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
  }
  sayMyJob() {
    console.log(`My job is ${this.job}`)
  }
}
const orange = new Person2('Orange', 10, 'writer')
console.log(orange) // Person2 {name: 'Orange', age: 10, job: 'writer'}
orange.sayMyJob() // My job is writer
```

![Untitled](https://user-images.githubusercontent.com/67324487/226158458-f3b21db1-27a2-4d32-b2e6-341cefde9ad8.png)

- 클래스 내 정의된 메소드는 클래스의 프로토타입에 저장됨
- 반면에 생성자 함수 내 정의된 메소드는 객체 내부에 저장됨
  - 생성자 함수로부터 생성된 yuza는 객체 내부에 메소드인 sayMyJob이 있고, 클래스에 의해 생성된 orange는 프로토타입 내부에 존재함

## cf) 생성자 함수를 클래스와 유사하게 사용하기

- 생성자함수도 클래스처럼 메소드를 프로토타입 내부에 둘 수 있음

```jsx
const Person1 = function (name, age, job) {
  this.name = name
  this.age = age
  this.job = job
}

Person1.prototype.sayMyJob = function () {
  console.log(`My job is ${this.job}`)
}
const yuza = new Person1('Yuza', 10, 'teacher')
console.log(yuza) // Person1 {name: 'Yuza', age: 10, job: 'teacher'}
yuza.sayMyJob() // My job is teacher
```

![Untitled](https://user-images.githubusercontent.com/67324487/226158473-f4c0dacd-34b3-4358-8abc-7b6c6fe5cbbf.png)

## new 키워드 유무에 따른 에러 발생

- 만약 생성자 함수를 new 키워드 없이 호출 시 (개발자가 실수한 코드이지만) 문제 없이 동작함 → 에러 캐치 불가
  - 생성자 함수에 return문이 없는 경우엔 undefined가 할당되므로 에러 발생 X
- 클래스의 경우 new 키워드 없이 실행하면 타입 에러가 발생함
  - 자바스크립트는 클래스의 특수 내부 프로퍼티인 `[[IsClassConstructor]]: true`를 통해 클래스 여부를 판단하여 클래스가 new 키워드와 함께 사용되지 않은 경우 에러를 발생시킴

![Untitled](https://user-images.githubusercontent.com/67324487/226158482-5351727b-a587-4cf1-8a71-d1cf913d386e.png)

![Untitled](https://user-images.githubusercontent.com/67324487/226158519-a6988f5f-11e8-4309-b15d-d35b9feea536.png)

## non-enumerable method

- 클래스의 메소드는 열거할 수 없음(non-enumerable)
  - 메소드의 enumerable 플래그가 false임
  - 생성자 함수의 경우 `for...in` 을 사용하면 프로토타입 내에 정의한 메소드를 포함한 객체 내의 모든 프로퍼티들을 다 확인할 수 있음
  - 클래스의 메소드의 경우 `for...in` 에서 제외됨

```jsx
const Person1 = function (name, age, job) {
  this.name = name
  this.age = age
  this.job = job
}

Person1.prototype.sayMyJob = function () {
  console.log(`My job is ${this.job}`)
}
const yuza = new Person1('Yuza', 10, 'teacher')
for (const i in yuza) {
  console.log(i) // name age job sayMyJob
}

// --------------------------------------------------------------

class Person2 {
  constructor(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
  }
  sayMyJob() {
    console.log(`My job is ${this.job}`)
  }
}
const orange = new Person2('Orange', 10, 'writer')
for (const i in orange) {
  console.log(i) // name age job
}
```

# 클래스 상속

- 클래스 상속을 통해 클래스 확장이 가능
  - extends 키워드를 통해 부모 클래스를 상속받은 자식 클래스를 사용해 만들어진 객체는 자식 클래스 내의 메소드 뿐만 아니라 부모 클래스에 정의된 메소드에도 접근 가능

![Untitled](https://user-images.githubusercontent.com/67324487/226158530-afdac3bc-214b-49b6-b5e3-efd01ae99f76.png)

![Untitled](https://user-images.githubusercontent.com/67324487/226158536-8f2b4798-6d9e-47b9-9d78-fbd509875316.png)

- 자식 클래스가 부모 클래스를 extends 하는 것은 곧 자식 클래스의 프로토타입의 `__proto__`를 부모의 프로토타입에 연결하는 것과 유사함
  - 자바스크립트의 클래스는 다른 언어의 클래스와는 다르게 프로토타입을 기반으로 하고 있어, 자식 클래스가 부모 클래스를 ‘복사’하기 보다 부모 클래스에 ‘연결(위임)’되어있다고 이해하는 것이 적절함
    - 위 이미지에서, 만약 부모 클래스인 Person의 자식 클래스인 Crew 클래스를 통해 새로운 객체를 생성한 뒤, Person에 새로운 메소드를 생성하면, 객체에서도 프로토타입 체이닝을 통해 해당 메소드를 사용할 수 있게 됨 = “연결”

```jsx
class Person {
  constructor(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
  }
  sayHello() {
    console.log(`Hello, My name is ${this.name}.`)
  }
}

class Developer extends Person {
  introduce() {
    console.log(`I'm ${this.age} years old and I'm a ${this.job}.`)
  }
}

const yuza = new Developer('Yuza', 23, 'frontend developer')
yuza.sayHello() // Hello, My name is Yuza.
yuza.introduce() // I'm 23 years old and I'm a frontend developer.
```

## extends 키워드와 메소드

![Untitled](https://user-images.githubusercontent.com/67324487/226158543-1c6ce0c2-0967-4489-bd7b-1eedcbdc8d74.png)

- 프로토타입을 기반으로 동작
- 자식 클래스의 prototype 프로퍼티의 `__proto__` 를 부모 클래스의 prototype 프로퍼티로 설정
  - ex. 위 코드의 경우 `Developer.prototype.__proto__ == Person.prototype`
  - 그러므로 Developer 클래스 내에 없는 메소드를 부모 클래스인 Person에서 찾아서 사용
- 자식 클래스 내에 메소드가 존재하지 않는 경우 동작 과정
  1. 객체 yuza에 sayHello 메소드의 존재 확인 → 존재하지 않음
  2. yuza의 프로토타입인 `Developer.prototype`을 확인 → 존재하지 않음
  3. extends를 통해 관계 맺어진 `Developer.prototype`의 프로토타입인 `Person.prototype`을 확인 → 존재함 → 해당 메소드 사용

## 메소드 오버라이딩

- 자식 클래스는 부모 클래스의 메소드를 그대로 상속 받지만, 만약 자식 클래스에서 부모 클래스의 메소드와 같은 이름의 메소드를 자체적으로 제작(정의)할 경우, 자체 제작 메소드가 사용됨
- super 키워드
  - 사용법
    - super.method(…): 부모 클래스에 정의된 메소드(method)를 호출
      - 만약 부모 클래스의 메소드를 완전히 덮어쓰지 않고 부분적으로 활용하고자 한다면 super 키워드를 사용하여 부모 메소드를 호출할 수 있음
    - super(…): 부모 생성자를 호출하며, 자식 생성자 내부에서만 사용 가능

```jsx
class Person {
  constructor(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
  }
  sayHello() {
    console.log(`Hello, My name is ${this.name}.`)
  }
  introduce() {
    console.log(`Nice to meet you. I'm ${this.age} years old.`)
  }
}

class Developer extends Person {
  sayHello() {
    console.log(`Hello, World!`)
  }
  introduce() {
    super.introduce()
    console.log(`I'm a ${this.job}.`)
    this.sayHello()
  }
}

const yuza = new Developer('Yuza', 23, 'frontend developer')
yuza.sayHello() // Hello, World!
yuza.introduce()
/* 
	Nice to meet you. I'm 23 years old.
	I'm a frontend developer.
	Hello, World!
*/
```

## 생성자 오버라이딩

- 자식 클래스에 constructor가 없는 경우 자동으로 빈 constructor가 만들어지며 부모 constructor를 호출 → 부모 constructor에 모든 인수 전달
  - constructor는 기본적으로 부모 constructor를 호출함

```jsx
class Person {
  // ...
}

class Developer extends Person {
  /*
	constructor(...args) {
	    super(...args);
  }
*/
}
```

- 자식 클래스에 constructor 추가할 시, 반드시 `super(…)`를 호출해야 함
  - 호출하지 않을 시 에러 발생
  - 자식 클래스의 생성자 내에서 this를 사용하기 전에 반드시 super(…)를 호출해야 하기 때문
    - 이유: 자식 클래스의 생성자 함수엔 특수 내부 프로퍼티인 `[[ConstructorKind]]:"derived”`가 존재 → new 키워드를 통해 실행되었을 시 다르게 동작
      - new와 함께 실행됐을 때
        - 일반 클래스의 경우: 빈 객체가 만들어진 뒤, this에 그 객체를 할당
        - 자식 클래스의 경우: 생성자 함수가 빈 객체를 만든 뒤, this에 그 객체를 할당하는 일을 부모 클래스의 생성자가 처리해주기를 기대함
          - 따라서, 자식 클래스의 경우 반드시 `super(…)`를 통해 부모 생성자를 실행해야 this가 될 객체가 만들어짐
- super(…)의 인자로 자식 클래스 내에서 사용되는 값들을 전달하면 부모 클래스가 그것들을 인자로 받아서 this의 프로퍼티로 할당함

```jsx
class Person {
  constructor(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
  }
  sayHello() {
    console.log(`Hello, My name is ${this.name}.`)
  }
  introduce() {
    console.log(`Nice to meet you. I'm ${this.age} years old.`)
  }
}

class Developer extends Person {
  constructor(name, age, job) {
    super(name, age, job) // -> Person 클래스의 constructor의 인자로 name, age, job이 들어가게 됨
    this.field = 'frontend'
  }
  sayHello() {
    console.log(`Hello, World!`)
  }
  introduce() {
    super.sayHello()
    console.log(
      `I'm a ${this.job}. Especially, I'm interested in ${this.field}.`,
    )
    this.sayHello()
  }
}

const yuza = new Developer('Yuza', 23, 'frontend developer')
yuza.introduce()
/*
	Hello, My name is Yuza.
	I'm a frontend developer. Especially, I'm interested in frontend.
	Hello, World! 
*/
```

[참고1](https://ko.javascript.info/class)

[참고2](https://www.youtube.com/watch?v=HujbNZ9IWF8&ab_channel=우아한Tech)

[참고3](https://think0wise.tistory.com/27)


# 계산된 프로퍼티 (Computed Property)

- 객체의 key 값을 [변수]로 표현 시 변수 안의 값이 객체의 key 값으로 할당됨
  - 그 프로퍼티를 ‘계산된 프로퍼티’라고 칭함

```jsx
const key1 = 'name'
const user1 = {
  [key1]: 'Yuza',
  age: 49,
}

console.log(user1) // { name: 'Yuza', age: 49 }

// --------------------------------------------------------------

const user2 = {
  [9 + 3]: 12,
  ['say' + ' hello']: 'Hello',
}

console.log(user2) // { '12': 12, 'say hello': 'Hello' }
```

# 다양한 객체 메소드

## Object.assign(초기값, 복제할 객체): 객체 복제 메소드

- 변수에 ‘객체를 할당한 다른 변수’를 할당하는 방식으로는 제대로 복제할 수 없음
  - clone1에 person을 할당할 경우, person이 가리키던 객체를 clone1도 함께 가리키게 됨
  - clone1이 가리키는 객체와 person이 가리키는 객체는 동일 객체이므로, clone1을 통해 객체의 속성값을 변경하면 person에 할당된 객체의 속성값도 함께 변경됨

```jsx
const person = {
  name: 'Yuza',
  age: 29,
}

const clone1 = person
clone1.name = 'James'

console.log(person) // { name: 'James', age: 29 } person도 함께 바뀌어버림;;
console.log(clone1) // { name: 'James', age: 29 }
```

- Object.assign() 메소드를 활용한 객체 복제

```jsx
const person = {
  name: 'Yuza',
  age: 29,
}

// 초기값이 빈 객체인 경우
const clone2 = Object.assign({}, person)
clone2.name = 'James'

console.log(person) // { name: 'Yuza', age: 29 }
console.log(clone2) // { name: 'James', age: 29 }

// --------------------------------------------------------------

// 초기값이 존재하는 경우
const clone3 = Object.assign({ job: 'programmer' }, person)
clone3.name = 'Diane'

console.log(clone3) // { job: 'programmer', name: 'Diane', age: 29 }

// --------------------------------------------------------------

// 초기값에 동일 속성명의 속성값 존재할 시, 해당 속성값은 객체의 원래 속성값으로 덮어씌워짐
const clone4 = Object.assign({ name: 'Colin', age: 10, job: 'writer' }, person)

console.log(clone4) // {name: 'Yuza', age: 29, job: 'writer'}

// --------------------------------------------------------------

// 다수의 객체 통합
const attribute1 = {
  job: 'programmer',
}
const attribute2 = {
  location: 'Seoul',
}

const clone5 = Object.assign(person, attribute1, attribute2)

console.log(clone5) // {name: 'Yuza', age: 29, job: 'programmer', location: 'Seoul'}
```

## Object.keys(): 객체의 속성명을 배열로 반환

```jsx
const person = {
  name: 'Yuza',
  age: 38,
}

console.log(Object.keys(person)) // [ 'name', 'age' ]
```

## Object.values(): 객체의 속성값을 배열로 반환

```jsx
const person = {
  name: 'Yuza',
  age: 67,
}

console.log(Object.values(person)) // [ 'Yuza', 67 ]
```

## Object.entries(): 객체의 속성명과 속성값을 배열로 반환

```jsx
const person = {
  name: 'Yuza',
  age: 20,
}

console.log(Object.entries(person)) // [ [ 'name', 'Yuza' ], [ 'age', 20 ] ]
```

## Object.fromEntries(): 객체의 key와 value 배열을 객체로 변환

```jsx
const person = [
  ['name', 'Yuza'],
  ['age', 13],
]

console.log(Object.fromEntries(person)) // { name: 'Yuza', age: 13 }
```

# 객체 프로퍼티와 Symbol

- 객체 프로퍼티 키로 문자형과 Symbol이 올 수 있음
  - Boolean이나 숫자로 된 키는 문자형으로 반환되며 접근할 때도 문자형으로 접근 가능

```jsx
const object = {
  1: '1이다',
  false: '거짓이다',
}
Object.keys(object) // ["1", "false"]

console.log(object['1']) // "1이다"
```

- Symbol은 유일한 식별자를 만들 때 사용 = 유일성 보장
  - 유일한 식별자이므로 a와 b가 각각 다름

```jsx
const a = Symbol()
const b = Symbol()

console.log(a, b) // Symbol() Symbol()

console.log(a === b) // false
console.log(a == b) // false
```

- Symbol에 description 추가 가능
  - Symbol()에 전달되는 문자열은 Symbol 생성에 영향 끼치지 않음 = 여전히 유일성 보장

```jsx
const a = Symbol('hi')
const b = Symbol('hi')

console.log(a, b) // Symbol(hi) Symbol(hi)

console.log(a === b) // false
console.log(a == b) // false

// 생성 시 전달된 문자열 확인
a.description // 'hi'
```

- Symbol형 프로퍼티 키
  - Object.keys()나 for in문으로는 출력되지 않음 = 은폐 가능
  - 특정 객체의 원본 데이터를 건드리지 않고 속성을 추가할 때 사용됨
    - 다른 사람이 만든 객체에 자신만의 속성을 추가하여 덮어써버리지 않기 위함

```jsx
const id = Symbol('id')
const user = {
  name: 'Tom',
  age: 20,
  [id]: 'hidden id', // Symbol형 프로퍼티 키
}

Object.keys(user) // ['name', 'age'] Symbol형 프로퍼티 key 은폐됨
Object.values(user) // ['Tom', 20] Symbol형 프로퍼티 value도 은폐됨
for (let key in user) {
  console.log(key)
} // 'name' 'age' Symbol형 프로퍼티 key 은폐됨

// 숨겨진 Symbol key 보는 법
Object.getOwnPropertySymbols(user) // [Symbol(id)]
Reflect.ownKeys(user) // ['name', 'age', Symbol(id)]
```

# 전역 Symbol: Symbol.for()

- Symbol.for()
  - 보통의 Symbol은 이름이 같아도 모두 다른 존재이지만, 전역 변수처럼 이름이 같으면 같은 객체를 가리켜야 할 때 Symbol.for() 사용
    - 단 하나의 Symbol만이 보장됨
    - Symbol.keyFor(이름): 생성 시 전달한 이름 반환

```jsx
const symbol1 = Symbol.for('onlySymbol')
const symbol2 = Symbol.for('onlySymbol')

console.log(symbol1 == symbol2) // true
console.log(symbol1 === symbol2) // true

Symbol.keyFor(symbol1) // 'onlySymbol'
Symbol.keyFor(symbol2) // 'onlySymbol'
```
# Math 내장 객체

- 수학과 관련된 프로퍼티와 메소드를 가진 내장 객체

## Math.ceil(): 올림

```jsx
let num1 = 3.4
let num2 = 4.2
Math.ceil(num1) // 4 Math.ceil(num2); // 5
```

## Math.floor(): 내림

```jsx
let num1 = 3.4
let num2 = 4.2
Math.ceil(num1) // 3 Math.ceil(num2); // 4
```

## Math.round(): 반올림

```jsx
let num1 = 3.6
let num2 = 4.2
Math.ceil(num1) // 4 Math.ceil(num2); // 4
```

## Math.random(): 무작위 숫자 생성

- 0~1 사이의 숫자를 무작위로 생성

```jsx
Math.random() // 0.601497854178328
Math.random() // 0.4594827065396163

// 1~50 사이의 임의의 숫자 생성
Math.floor(Math.random() * 50) + 1 // 21
```

## Math.max(), Math.min(): 최대값과 최소값

```jsx
Math.max(4, 2, 6, 100, 0.23) // 100
Math.min(4, 2, 6, 100, 0.23) // 0.23
```

## Math.abs(): 절대값

```jsx
Math.abs(-10) // 10
```

## Math.pow(), Math.sqrt(): 제곱, 제곱근

```jsx
Math.pow(3, 3) // 27
Math.sqrt(49) // 7
```

# 기타 숫자 관련 method

## toString(): 10진수를 n진수로 변환

- 인수로 전달한 숫자의 진수로 변환
- 문자열로 반환

```jsx
let num = 50

num.toString(2) // '110010'
num.toString(16) // '32'
```

## toFixed(): 특정 소수점 자리까지 표현

- 소수점 자리수 이상의 수를 인자로 전달 시 해당 자리수까지 남는 자리는 0으로 채움
- 문자열로 반환

```jsx
let num = 12345.1234567

num.toFixed(0) // '12345'
num.toFixed(1) // '12345.1'
num.toFixed(2) // '12345.12'
num.toFixed(9) // '12345.123456700'
```

## isNaN(): NaN 여부 검사

- NaN: 잘못된 수학 계산 또는 잘못된 숫자
  - 숫자형이지만 숫자가 아닌 값
- NaN인지 검사할 수 있는 유일한 방법
  - NaN은 자기 자신인 NaN과도 같지 않다고 판단하므로

```jsx
let isNum = Number('no')

isNum == NaN // false
isNum === NaN // false
NaN == NaN // false

isNaN(isNum) // true
isNaN(4) // false
```

## parseInt(): 숫자로 변환

- 숫자로 변환 가능한 부분(숫자인 부분)까지만 숫자로 변환
- Number()과의 차이점: Number()은 숫자 + 문자의 경우 NaN 반환
- 문자로 시작하는 단어는 NaN 반환
- 소수점 이하는 무시: 정수만 반환
- 두번째 인자로 숫자 전달 시 해당 진수로 판단
  - ex) 'f3'은 문자로 시작했지만 두번째 인자로 16을 전달 시 f3을 16진수로 판단하여 숫자로 변환, 243을 반환

```jsx
let numString = '123string'
let stringNum = 'string123'
parseInt(numString) // 123
Number(numString) // NaN
parseInt(stringNum) // NaN

let num = 'f5'
parseInt(num, 16) // 245
parseInt('101', 2) // 5
```

# 특정 위치에 접근

- 특정 위치에 인덱스를 사용하여 접근 가능
  - 문자열 내 한 글자만 인덱스로 접근하여 변경은 불가능

```jsx
let sentence = 'hello'
sentence[1] = 'o'

console.log(sentence) // 'hello'
```

# str.toUpperCase()/toLowerCase(): 대문자/소문자 변환

```jsx
let sentence = 'hello'

console.log(sentence.toUpperCase()) // 'HELLO'
console.log(sentence.toLowerCase()) // 'hello'
```

# str.indexOf(): 문자열 위치 반환

- 문자를 인수로 받아 몇 번째 위치하는 지 반환
  - 찾는 문자가 해당 문자열에 없으면 -1을 반환
  - 일치하는 문자열이 여러 개 있어도 첫 번째 위치만 반환

```jsx
let sentence = 'hello, how are you?'

console.log(sentence.indexOf('how')) // 7
console.log(sentence.indexOf('hi')) // -1
console.log(sentence.indexOf('h')) // 0
```

# str.slice(n, m): 문자열 자르기

- 인덱스 n부터 m까지 문자열을 잘라서 반환
  - m이 없으면 n부터 문자열 끝까지
  - m이 양수면 n부터 m-1까지
  - m이 음수면 n부터 끝에서 m-1까지
    - 끝에서 셀 때는 -1, -2, -3...순으로 셈

```jsx
let sentence = 'hello, how are you?'

console.log(sentence.slice(7)) // 'how are you?'
console.log(sentence.slice(0, 5)) // 'hello'
console.log(sentence.slice(7, -5)) // 'how are'
```

# str.substring(n, m): 문자열 자르기

- 인덱스 n부터 m까지 문자열을 잘라서 반환
  - n과 m을 바꿔도 동일하게 동작: 작은 수부터 큰 수까지
  - 음수는 0으로 인식

```jsx
let sentence = 'hello, how are you?'

console.log(sentence.substring(7)) // 'how are you?'
console.log(sentence.substring(0, 5)) // 'hello'
console.log(sentence.substring(7, -5)) // 'hello, '
```

# str.substr(n, m): 문자열 자르기

- 인덱스 n부터 m개의 문자열을 반환
  - m이 없으면 n부터 문자열 끝까지

```jsx
let sentence = 'hello, how are you?'

console.log(sentence.substr(7)) // 'how are you?'
console.log(sentence.substr(0, 5)) // 'hello'
console.log(sentence.substr(-12, 3)) // 'how'
```

# str.trim(): 문자열 앞뒤 공백 제거

```jsx
let sentence = '  hello?   '

console.log(sentence.trim()) // 'hello?'
```
# arr.push()/pop()/unshift()/shift(): 기본 삽입, 삭제 메소드

- push(): 배열 맨 뒤에 삽입
- pop(): 배열 맨 뒤에 삭제한 뒤 해당 요소 반환
- unshift(): 배열 맨 앞에 삽입
- shift(): 배열 맨 앞에 삭제한 뒤 해당 요소 반환

```jsx
let array = [1, 2, 3, 4, 5]

array.push(6)
console.log(array) // [ 1, 2, 3, 4, 5, 6 ]

// --------------------------------------------------------------

let popped = array.pop()
console.log(popped) // 6
console.log(array) // [ 1, 2, 3, 4, 5 ]

// --------------------------------------------------------------

array.unshift(0)
console.log(array) // [ 0, 1, 2, 3, 4, 5 ]

// --------------------------------------------------------------

const shifted = array.shift()
console.log(shifted) // 0
console.log(array) // [ 1, 2, 3, 4, 5 ]
```

# arr.splice(n, m): 배열 내 요소 제거

- 인덱스 n부터 m개의 요소를 제거
  - 삭제 요소를 반환함

```jsx
let arr = [0, 1, 2, 3, 4, 5]

arr.splice(0, 2) // [0, 1]

console.log(arr) // [2, 3, 4, 5]
```

# arr.splice(n, m, x): 배열 내 요소 제거 후 추가

- 인덱스 n부터 m개의 요소를 제거 후 x를 삽입
  - m이 0이면 제거하지 않고 n에서부터 요소 추가

```jsx
let arr = [0, 1, 2, 3, 4, 5]

arr.splice(3, 0, 123, 456) // []

console.log(arr) // [0, 1, 2, 123, 456, 3, 4, 5]
```

# arr.concat(arr2, arr3...): 배열 합쳐서 새로운 배열 반환

- 인덱스 n부터 m개의 요소를 제거 후 x를 삽입
  - m이 0이면 제거하지 않고 n에서부터 요소 추가

```jsx
let arr = [1, 2]

arr.concat([3, 4], [5, 6], [7, 8]) // [1, 2, 3, 4, 5, 6, 7, 8]
```

# arr.forEach(fn): 배열 내 요소 순회

- 배열 내 요소를 순회하며 함수의 인자로서 활용
  - 콜백 함수의 첫번째 인자: 배열 내 요소
  - 두번째 인자: 해당 요소의 index

```jsx
let arr = ['A', 'B', 'C']

arr.forEach((alphabet, index) => {
  console.log(`${index}. ${alphabet}`)
})
// 0. A
// 1. B
// 2. C
```

# arr.indexOf(n)/arr.lastIndexOf(n): 배열 내 요소 인덱스 반환

- 배열 내 요소가 처음/마지막에 등장하는 인덱스를 반환
  - arr.indexOf(찾는 요소, 이 인덱스부터 찾기)

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.indexOf(4) // 3
arr.indexOf(4, 4) // 8
arr.lastIndexOf(3) // 7
```

# arr.includes(): 배열 내 요소 포함 여부 확인

- 배열 내 요소가 처음/마지막에 등장하는 인덱스를 반환
  - arr.indexOf(찾는 요소, 이 인덱스부터 찾기)

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.includes(2) // true
arr.includes(10) // false
```

# arr.find(fn): 함수를 만족하는 첫번째 요소만을 반환

- 만약 만족하는 요소 없을 시 undefined 반환

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.find((item) => item % 2 === 0) // 2
arr.find((item) => item % 123 === 0) // undefined
```

# arr.filter(fn): 함수를 만족하는 모든 요소 반환

- 만약 만족하는 요소 없을 시 빈 배열 반환

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.filter((item) => item % 2 === 0) // [2, 4, 2, 4]
arr.find((item) => item % 123 === 0) // []
```

# arr.map(fn): 배열 내 요소를 순회하며 함수를 적용한 뒤 새로운 배열 반환

- 원본 배열에는 변화 없음

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.map((item) => item * 2) // [2, 4, 6, 8, 10, 2, 4, 6, 8]
console.log(arr) // [1, 2, 3, 4, 5, 1, 2, 3, 4]
```

# arr.sort(): 배열을 재정렬

- 원본 배열을 변화시킴
- 비교 함수가 제공될 시, 비교 함수 function(a, b)의 결과가 0보다 작으면 a를 b 앞에 두며, 0과 같으면 a, b의 순서를 변경하지 않고, 0보다 크면 b를 a의 앞에 위치시킴

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.sort() // [1, 1, 2, 2, 3, 3, 4, 4, 5]
console.log(arr) // [1, 1, 2, 2, 3, 3, 4, 4, 5]

// --------------------------------------------------------------

arr.sort((a, b) => a - b) // [1, 1, 2, 2, 3, 3, 4, 4, 5]
arr.sort((a, b) => b - a) // [5, 4, 4, 3, 3, 2, 2, 1, 1]
```

# arr.reverse(): 배열을 역순으로 재정렬

- 원본 배열을 변화시킴

```jsx
let arr = [1, 2, 3, 4, 5, 1, 2, 3, 4]

arr.reverse() // [4, 3, 2, 1, 5, 4, 3, 2, 1]
console.log(arr) // [4, 3, 2, 1, 5, 4, 3, 2, 1]
```


