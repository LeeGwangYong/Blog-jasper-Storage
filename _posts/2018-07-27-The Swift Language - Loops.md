---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "The Swift Language - Loops and String Interpolation"
date: 2018-07-27 00:00:00
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

# Loops and String Interpolation

Swift는 다른 언어들과 친숙한 control flow statement(`if-else`, `while`, `for`, `for-in`, `repeat-while`, `switch`)를 가지고 있습니다.

Swift는 C-style의 `for` 루프와는 다른 형식으로, **Range** 타입을 사용합니다.

각 item의 index를 원한다면 `enumerated()` 를 사용합니다. `enumerated()` 는 **tuple의 sequence**를 반환합니다. tuple은 각 <u>멤버가 다른 타입을 갖을 수 있다</u>는 것을 제외한다면 array와 유사하게 정렬되어진 값의 그룹입니다.  Objective-C에서는 tuple을 지원하지 않습니다.

```swift
let countingUp = ["one", "two", "three"]
let range = 0..<countingUp.count
for i in range {
    print(countingUp[i])
}
//"one"
//"two"
//"three"
------------------------------------------
let range = 0..<countingUp.count
for string in countingUp {
    print(string)
}
//"one"
//"two"
//"three"
------------------------------------------
for (index,string) in countingUp.enumarated() {
    print(index, string)
}
//0	"one"
//1	"two"
//2	"three"
```

```swift
let nameByParkingSpace = [13: "Alice",
						  27: "Bob"]
for (spaceNum, name) in nameByParkingSpace {
	print("Space \(spaceNum): \(name)")
}
//"Space 13: Alice"
//"Space 27: Bob"
```

`\()` 는 String Interpolation(삽입)을 나타냅니다. 이 표현법은 runtime에 평가되어지고 삽입되어집니다.

> 관련 사이트
>
> - [http://developer.apple.com/swift](http://developer.apple.com/swift)
> - [Swift 언어 개발 문서](http://swift.leantra.kr)
> - [the swift programming languageswift 4.2](https://docs.swift.org/swift-book/)