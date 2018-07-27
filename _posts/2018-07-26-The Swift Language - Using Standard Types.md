---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "The Swift Language - Using Standard Types"
date: 2018-07-26 00:00:00
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

# Using Standard Types

`var` : variable, can be changed

`let` : constant value, cannot be changed

```swift
var str = "Hello, playground" 
str = "Hello, Swift"
var constStr = str
contStr = "Hello, world" // error
```

### Inferring types

위의 `str`, `constStr` 는 타입이 없는 것이 아닌, 특정한 타입을 갖고 있다. 

컴파일러는 그들의 타입을 최초의 **값으로 부터 추론**한다. 이것을 **type inference(타입 추론)** 이라고 한다.

"Hello, playground"라는 String Value를 토대로, 컴파일러는 `str`, `constStr` 를  `String` type이라고 추론한다.

### Specifying types

만약 상수 혹은 변수가 최초의 값을 갖고있지 않거나 특정 타입을 보장하고 싶다면, 타입을 선언해주면 된다.

```swift
var str: String = "Hello, playground" 
var constStr: String = str
var number: Int
```

### Number and Boolean types

정수에 대한 가장 일반적인 타입은 `Int` 입니다. 단어 크기, signedness에 기초한 추가적인 정수타입들이 존재합니다. 하지만, Apple은 다른 것들을 쓸 이유가 있지 않는한, `Int` 의 사용을 추천합니다.

Swift에서 floating-point(부동소수점) 숫자는 3가지의 타입이 제공됩니다. `Float` (32bit), `Double` (64bit), `Float80` (80bit)

`Bool` 은 true 또는 false 의 값을 갖습니다.

### Collection Types

Swift 표준 라이브러리는 3가지의 collection을 제공합니다. `Array`, `Dictionary`, `Set`

`Array<T>` 는 원소의 정렬된 collection이며, standard type, `struct`, `class` 를 포함할 수 있습니다.

```swift
var arrayOfInts: [Int]
//var arrayOfInts: Array<Int>
```

`Dictionary<Key:Hashable,Value> ` 는 정렬되지않은 key-value 쌍의 collection입니다. 

value는 `struct`, `class` 를 포함하여 모든 타입이 될 수 있습니다. key 또한 모든 타입이 될 수 있지만, 유니크해야합니다.  특히 key는 **hashable**해야하며, 사전에서 키가 고유함을 보장하고 key의 value에 보다 효율적으로 접근할 수 있습니다.

기본적인 Swift type들(`Int`, `Float`, `Character`, `String`)은 **hashable**입니다.

```swift
var dictionaryOfCapitalsByCountry: [String: String]
//var dictionaryOfCapitalsByCountry: Dictionary<String, String>
```

 `Set` 은  `Array` 와 유사해보입니다. 하지만, `Set` 은 **정렬되지 않았으며**, 멤버들은 반드시 **유니크**할 뿐만 아니라 **hasable**해야합니다.

```swift
var winningLotteryNumbers: Set<Int>
```

### Literals and subscripting

Swit는 `Array`에 접근하기 위한 속기 수단으로서 subscripting을 제공합니다. 

```swift
print(arrayOfInts[0])
```

배열 범위 외의 인덱스를 접근한다면, runtime error가 발생합니다.

Subscripting은 `Dictionary`에서도 작용합니다.

### Initializers

지금까지, 변수와 상수들을 literal value를 이용하여 초기화하였습니다. 이 과정에서 특정 타입의 **instance**를 만든 것입니다.

**instance**는 타입의 형상화(embodiment)입니다. 역사적으로 이 용어는 오직 `class`에서만 사용되어왔지만, Swift에서는 structure, enumeration 을 표현하기 위해서도 사용됩니다.

instance를 만들기위한 다른 방법으로는 타입의 **initializer**를 사용하는 것입니다. **Initializer**는 타입의 새로운 instance 내용을 준비하는 역할을 합니다. initializer가 끝마쳤을 때, instance는 실행할 준비가 됩니다. 새로운 instance를 만들기 위해서 "TypeName()" (필요하다면, 인자가 들어가는) 형식의 initializer를 사용해야합니다. 이 특징(타입과 인자의 조합)은 특별한 initializer와 일치합니다.

어떤 standard type은 인자가 들어가지 않을때, 빈 literal을 반환하는 initializer를 가지고 있습니다.

```swift
let emptyString = String()			// ""
let emptyArrayOfInts = [Int]() 			// 0 elements
let emptySetOfFloats = Set<Float>()		// 0 elements
let defaultBool = Bool()			// false
```

타입은 여러개의 initializer를 가질 수 있습니다.

```swift
let number = 42
let meaningOfLife = String(number)
```

### Properties

타입의 instance와 연관된 value를 **property** 라고 합니다. 예를 들어, `String`은 `isEmpty`라는 property를 갖고 있고, 이 property는 `Bool` 타입으로, 문자가 비었는지에 대해서 알려줍니다.

```swift
print(meaningOfLife.isEmpty)
```

### Instance Methods

특정 타입의 특별한 함수를 **instance method** 라고 하며, 타입의 instance를 이용해 호출할 수 있습니다.

```swift
var arrayOfInts = ["one", "two"]
arrayOfInts.append("three")
```

> 관련 사이트
>
> - [http://developer.apple.com/swift](http://developer.apple.com/swift)
> - [Swift 언어 개발 문서](http://swift.leantra.kr)
> - [the swift programming languageswift 4.2](https://docs.swift.org/swift-book/)