---
layout: post
current: post
cover:  assets/images/ios.png
navigation: True
title: "Functional Programming "
date: 2018-08-02 00:00:00
tags: [Development, iOS]
class: post-template
subclass: 'post tag-development'
author: leegwangyong
---

Functional Programming 공부내용 정리 포스트입니다.

##### Composition + Declarative + No Side Effect

> "Functional Programming은 **프로그래밍에 대한 생각**이다"
>
> ## "복잡한 것은 작고, 간단한 것들로 분해할 수 있다."

### 복잡한 것을 작고, 간단한 것들로 분해하기

```swift
persons를 "어떻게 만들어야하는 지(How)", Imperative
//루프를 사용
var persons: [Person] = []
for name in names {
    let person = Person(name: name)
    if person.isValid {
        persons.append(person)
    }
}
------------------------------------------


//조금 더 간단한 2개의 루프로 분해
//수행업무(Concern)를 기준으로 분리
//업무 1. 배열 생성
var possiblePersons: [Person] = []
for name in names {
    let person = Person(name: name)
//업무 2. 배열에 저장된 값들에 하나씩 접근
    possiblePersons.append(person)
}
var persons: [Person] = []
for person in possiblePersons {
//업무 3. 각각의 값에 대해 어떠한 작업을 수행
    if person.isValid {
//업무 4. 마지막에는 다른 배열에 그 결과를 저장
        persons.append(person)
    }
}
------------------------------------------
//루프 안에서 generic 형태를 발견
let possiblePersons = names.map(Person.init)
let persons = possiblePersons.filter { $0.isValid }
------------------------------------------


persons가 "무엇인지(What)", Declarative
//chaining을 이용하여 재조합
let persons = names.map(Person.init).filter { $0.isValid }
```

위 방식은 persons를 ''어떻게 만들어야하는 지(How)"에 초점을 맞추는 대신, **persons가 "무엇인지(What)"** 에 대해 알려줍니다. (**Declarative Programming**)

#### Composition

composition 방법 1. protocl + struct

```swift
extension MyStruct<T>: Sequence {
	func makeIterator() -> AnyIterator<T> {
		return ... 
    }
}
```

composition 2. type에 context(문맥) 추가하기

```swift
func login(username: String, password: String, completion: (String?, Error?) -> Void)
login(username: "rob", password: "s3cret") { (token, error) in
	if let token = token {
		// success
	} else if let error = error { 
        // failure
	}
}
------------------------------------------------------------
//token은 '규칙'을 가지고 있습니다. Token에 문맥적 의미를 부여합니다. 구조적으로 만들기 위하여 'struct'를 이용합니다.
struct Token {
	let string: String
}	
//usnername과 password를 함께(AND) 결합하는 규칙을 만듭니다.
struct Credential {
	var username: String 
    var password: String
}
//token 또는(OR) error를 표현하기 위하여 'enum'을 사용합니다
enum Result<Value> { 
    case success(Value) 
    case failure(Error)
}

func login(credential: Credential,
           completion: (Result<Token>) -> Void)
     login(credential: credential) { result in
     switch result {
     case .success(let token): // success
     case .failure(let error): // failure
     }
}
```

### Programming Technique

#### Pure Function

- 부작용(함수 스코프를 벗어나, 외부에 변화를 가하는 것)을 발생시키지 않는 함수 
- 참조 투명성 : 같은 input에 대한 동일한 output

```swift
func Log(_ message: String) {
	print(message)
}
```

#### Higher-Order Function

함수의 인자로 함수를 받는다.

```swift
var array = [2, 6, 3, 1, 7]
array.sort(by: { a,b in
    return a < b
})
```

## Functional Programming이란?

Function + **No Side-Effect** + Declarative Programming

#### Functional Programming

```swift
//non-FP
object.method()
//FP
method(data)
```

#### No Side Effect

**State (Shared mutable state) 가 존재한다 = Side Effect 발생**

- OOP(Object Oriented Programming)
  - 모듈 : 기능 하나에 연관된 Object들끼리의 집합
  - Object : State(Member variable) + Method
  - Method의 수행 결과는 멤버변수가 어떤 상태를 가지고 있는가에 의하여 달라진다. => Side-Effect
  - State(Member variable)이 존재한다 = Side-Effect가 존재한다
- Functional Programming
  - input과 output으로 구성되어있다.
  - input들에 대한 output들이 서로 연결되어, 하나의 커다란 output을 만들어낸다.
  - Pure Function => 동일한 input, 동일한 output => **No state => No Side-Effect**

#### Imperative vs Declarative

- Imperative(명령형) Programming

  - How, 어떤 과정을 통해 결과를 얻고 싶어!
  - state의 변화를 추적해줘야한다.

- **Declarative(선언형) Programming** 

  - What, 어떤 결과를 얻을 거야!
  - **사이즈는 작고, 신뢰도는 높은 함수들을 연결하여 만들면, 신뢰도가 높은 결과물**이 산출된다.

  ![Image](https://image.slidesharecdn.com/20180310functionalprogramming-180308125540/95/20180310-functional-programming-33-638.jpg?cb=1531921364){: width="100%" height="100%"}

> 관련 사이트
>
> - [https://academy.realm.io/kr/posts/tryswift-rob-napier-swift-legacy-functional-programming](https://academy.realm.io/kr/posts/tryswift-rob-napier-swift-legacy-functional-programming)
> - [https://www.slideshare.net/ChiwonSong/20180310-functional-programming](https://www.slideshare.net/ChiwonSong/20180310-functional-programming)
> - [https://www.slideshare.net/devxoul/rxswift-81314827](https://www.slideshare.net/devxoul/rxswift-81314827)