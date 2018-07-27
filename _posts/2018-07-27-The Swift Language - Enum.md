---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "The Swift Language - Enumerations and the Switch Statement"
date: 2018-07-27 00:00:01
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

# Enumerations and the Switch Statement

Enumeration은 개별 값 집합을 가진 타입입니다.

```swift
enum PieType {
	case apple
	case cherry
	case pecan
}
let favoritePie = PieType.apple
var name: String
switch favoritePie {
    case .apple:
    	name = "Apple"
    case .cherry:
    	name = "Cherry"
    case .pecan:
    	name = "Pecan"
}
```

```swift
let macOSVersion: Int = ...
switch macOSVersion {
    case 0...8:
   		print("A big cat")
   	case 9:
   		print("Mavericks")
   	case 10:
   		print("Yosemite")
   	case 11:
   		print("El Capitan")
}
```

### Enumerations and raw values

Swift enum은 raw value를 갖을 수 있습니다.

```swift
enum PieType: Int {
	case apple = 0
	case cherry
	case pecan
}
let pieRawValue = PieType.pecan.rawValue	//2
if let pieType = PieType(rawValue: pieRawValue) {
    //got a valid 'pieType'
}
```

> 관련 사이트
>
> - [http://developer.apple.com/swift](http://developer.apple.com/swift)
> - [Swift 언어 개발 문서](http://swift.leantra.kr)
> - [the swift programming languageswift 4.2](https://docs.swift.org/swift-book/)