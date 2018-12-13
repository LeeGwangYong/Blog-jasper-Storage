---
layout: post
current: post
cover:  assets/images/ios.png
navigation: True
title: "# Getting High-Fidelity Input with Coalesced Touches"
date: 2018-12-12 00:00:00
tags: [Development, iOS, Apple Developer Documentation]
class: post-template
subclass:  'post tag-development'
author: leegwangyong

---

## Overview

`UIKit`은 일반적으로 약 60Hz정도로  touch를 전달합니다. 하지만 어떤 디바이스들은 최대 240Hz 까지 touch 정보를 기록할 수 있습니다. app이 추가 데이터가 필요하지 않는 경우라면,  `UIKit`은 추가적인 touch 정보를 자동적으로 전달하지 않습니다. 대신, 추가적인 touch들을 하나의 `UITouch` object로 하칩니다.  이것의 위치는 마지막으로 기록된 touch만을 반영합니다. 그러나 추가적인 정밀도를 원하는 app은 추가적인 touch 정보를 받고 사용할 수 있습니다.
> 합쳐진 touch는 추가적인 정밀도가 필요하고, 연관된 비용을 처리할 수 있는 app을 위한 것입니다. touch를 합치는 작업은 추가적인 데이터를 모으고, 컨텐트에 적용함을 뜻합니다. 만약 추가적인 정밀도가 필요하지않다면, `UIKit` 이 view의 method나 gesture recognizer로 전달하는 touch object의 집합을 계속 사용하면됩니다.


