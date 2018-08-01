---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "Views and the View Hierarchy"
date: 2018-07-27 00:00:02
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

### View Basics

button, text field, slider와 같은 view들은 <u>user에게 보여지는 object</u>입니다.

View Object들은 Application의 UI를 구성합니다.

View는

- `UIView`의 instance이거나, subclass 중 하나의 instance입니다.
- 자신을 그리는 방법을 압니다.
- touch와 같은 event를 다룰 수 있습니다.
- Application의 winodw에 root가 있는 View 계층 내에 존재합니다.

### The View hierarchy

모든 Application들은 하나의  `UIWindow`  instance를 갖습니다. **`UIWindow` 는 모든 view들에 대한 컨테이너 역할**을 합니다.

> 관련 사이트
>
> - [View Hierarchy](https://developer.apple.com/library/archive/documentation/General/Conceptual/Devpedia-CocoaApp/View%20Hierarchy.html)