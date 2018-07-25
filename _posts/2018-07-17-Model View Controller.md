---
layout: post
current: post
cover:  assets/images/aaron.jpg
navigation: True
title: "Model View Controller"
date: 2018-07-17 00:00:00
tags: [Aaron Hillegass, Development, iOS]
class: post-template
subclass: 'post tag-aaron-hillegass'
author: leegwangyong
---

# MVC

MVC는 iOS 개발에 사용되어지는 디자인 패턴입니다. MVC에서는, 모든 instance는 **model layer**, **view layer**, 또는 **controller layer**에 속해있다.

![](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Art/model_view_controller_2x.png){: width="100%" height="100%"}

- **Model Layer**는 데이터를 저장하고 사용자 인터페이스 등 UI에 대해서는 아무것도 모릅니다.
  일반적으로 Model layer에서의 instance들은 사용자 세계의 실제 것들을 나타냅니다.
- **View Layer**는 사용자들에게 보이는 objects를 포함합니다. 
  View Object 또는 View의 예로는 Button, TextField 및 Slider가 있습니다. 
  View Object들은 application의 UI를 구성합니다.
- **Controller Layer**는 application이 관리되는 곳입니다. 
  Controller Objects, 또는 Controllers는 application의 관리자입니다.
  Controllers는 사용자들이 보는 View들을 구성하고, View와 Model objects가 동기화 상태를 유지하도록 한다.
  일반적으로, Controllers는 "And then?"을 처리한다.
- **'Model과 View는 서로 직접 이야기하지 않는다'**는 것을 알아야한다.
  **Controller는 모든 것의 중앙에 위치해, 메세지를 받고 지시를 발송한다.**

> 관련 사이트 : [MVC - Apple Developer](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html)