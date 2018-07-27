---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "The Swift Language - Types in Swift"
date: 2018-07-20 00:00:00
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

# Types in Swift

Swift types는 3가지의 기본 그룹(**Structure(Struct), Class, Enumeration(Enum)**)으로 나눌 수 있습니다.

Structure, Class, Enumeration은 **property, initializer, instance method, class or static method**를 갖습니다.

Swift의 Structure, Enum은 다른 대부분의 언어에서 보다 강력합니다. 추가로 property, initializer, method를 지원하기 위하여 **protocol**을 따르고 확장(**extension**)되어질 수 있습니다.

Swift의 "primitve" type(Numbers, Boolean etc)의 모두 Struct로 구현되어있습니다.

- Numbers: `Int`, `Float`, `Double` 
- Boolean: `Bool` 
- Text: `String`, `Character` 
- Collections: `Array<Element>`, `Dictionary<Key:Hashable,Value>`, `Set<Element:Hashable>` 

위 type들 또한 protocol을 따르고 확장(extension)되어질 수 있습니다.

> 관련 사이트
>
> - [http://developer.apple.com/swift](http://developer.apple.com/swift)
> - [Swift 언어 개발 문서](http://swift.leantra.kr)
> - [the swift programming languageswift 4.2](https://docs.swift.org/swift-book/)
>
> -  [Hashable - Swift Standard Library](https://developer.apple.com/documentation/swift/hashable)

