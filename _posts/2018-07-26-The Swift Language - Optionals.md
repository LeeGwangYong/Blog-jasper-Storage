---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "The Swift Language - Optionals"
date: 2018-07-26 12:00:00
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

# Optionals

Swift type은 **optional** 이 될 수 있으며, 타입 이름에 `?` 를 붙여 표시합니다.

```swift
var optionalString: String?
```

optional은 변수가 **값을 저장하지 않을 가능성**을  표현합니다. Optional value는 타입의 인스턴스이거나 **nil** 입니다.

```swift
var optionalFloat: Float?		//nil
```

Optional Float은 **Float** 또는 **nil** 값을 포함할 수 있습니다. 만약 초기값이 주어지지 않았다면, 초기값은 nil로 됩니다.

floating-point literal를 할당하여 optional float에 값을 할당할 수 있습니다.

```swift
optionalFloat = 3.14			//Optional(3.14)
```

하지만, 이 optional float이 Float value가 할당되었을 지라도,  non-optional float과 같이 사용할 수 없습니다. optional value의 값을 읽기 전에, nil이 될 가능성을 말해야합니다. 이것을 optional을 '**unwrapping 한다**'라고 합니다.

Unwrapping에는 **optional binding**과 **forced unwrapping** 방식이 있습니다.

**forced unwrapping** 은 `!` 를 붙여주면 됩니다.

```swift
print(optionalFloat!)			//3.14
```

nil이 할당되어진 optional float에 forced unwrapping을 하면 error가 발생하게 됩니다.

```swift
optionalFloat = nil
print(optionalFloat!)			//fatal error
```

더 안전한 방법으로는 `if-let` 을 이용하는 **optional binding**이 있습니다. 만약 optinal value의 값이 nil이라면, else 구문으로 넘어가게 됩니다.

```swift
var reading1: Float? = 0.2
var reading2: Float? = 3.14
var reading3: Float?
if let r1 = reading1,
	let r2 = leading2,
	let r3 = reding3 {
	let avg = (r1 + r2 + r3)/3
} else {
	print("something is nil")
}
```

위 코드에서는 reading3가 nil이므로, "something is nil"을 출력합니다.

### Subscripting dictionaries

**Dictionary subscripting 결과는 optional**입니다.

```swift
let dic = [13 : "Alice",
			27 : "Bob"]
let dic13: String? = dic[13]		//Optional("Alice")
let dic14: String? = dic[42]		//nil

if let value13 = dic[13] {
	print(value13)					//"Alice"
}
```



> 관련 사이트
>
> - [http://developer.apple.com/swift](http://developer.apple.com/swift)
> - [Swift 언어 개발 문서](http://swift.leantra.kr)
> - [Optional - Swift Standard Library](https://developer.apple.com/documentation/swift/optional/)
> - [the swift programming languageswift 4.2](https://docs.swift.org/swift-book/)