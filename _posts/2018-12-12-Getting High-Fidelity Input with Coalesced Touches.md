---
layout: post
current: post
cover:  assets/images/ios.png
navigation: True
title: "Getting High-Fidelity Input with Coalesced Touches"
date: 2018-12-12 00:00:00
tags: [Development, iOS, Apple Developer Documentation]
class: post-template
subclass:  'post tag-development'
author: leegwangyong

---

## Overview

`UIKit`은 일반적으로 약 60Hz정도로  touch를 전달합니다. 하지만 어떤 디바이스들은 최대 240Hz 까지 touch 정보를 기록할 수 있습니다. app이 추가 데이터가 필요하지 않는 경우라면,  `UIKit`은 추가적인 touch 정보를 자동적으로 전달하지 않습니다. 대신, 추가적인 touch들을 하나의 `UITouch` object로 하칩니다.  이것의 위치는 마지막으로 기록된 touch만을 반영합니다. 그러나 추가적인 정밀도를 원하는 app은 추가적인 touch 정보를 받고 사용할 수 있습니다.
> 합쳐진 touch는 추가적인 정밀도가 필요하고, 연관된 비용을 처리할 수 있는 app을 위한 것입니다. touch를 합치는 작업은 추가적인 데이터를 모으고, 컨텐트에 적용함을 뜻합니다. 만약 추가적인 정밀도가 필요하지않다면, `UIKit` 이 view의 method나 gesture recognizer로 전달하는 touch object의 집합을 계속 사용하면됩니다.

그림 1은 사용자가 Apple Pencil을 드개르할 때의 현상을 보여줍니다. `UIKit`이 app에 touch 이벤트를 보고하는 시점에 Apple Pencil은 4개의 touch 위치를 보고했지만, `UIKit`은 기본적으로 오직 마지막 touch만을 보고하고 있습니다. 남은 3개의 touch들은 합쳐진 touch로 전달되고, app은 이것들을 사용하기 위해서는 반드시 검색해야합니다.

![그림1](https://docs-assets.developer.apple.com/published/7c21d852b9/25b4cf04-2752-41a9-b1c8-fa27ac76d0de.png)

합쳐진 touch를 검색하기 위해서는 원래의 `UITouch` object를 포함하고 잇는 `UIEvent` 의 [`coalescedTouches(for:)`](https://developer.apple.com/documentation/uikit/uievent/1613808-coalescedtouches) 를 호출하면됩니다. 이 method는 실제로 app에 전달된 마지막 `UITouch` object를 포함하여  마지막 이벤트 이후의 모든 touch 배열을 반환합니다. 이벤트를 처리할 때 즉시 합쳐진 touch들을 검색해야합니다. 이벤트를 처리한 이후에는, 어떠한 합쳐진 touch들도 이용가능한 보장은 없습니다.

# Reference

- Apple Developer Documentation
	- [Getting High-Fidelity Input with Coalesced Touches](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_touches_in_your_view/getting_high-fidelity_input_with_coalesced_touches)
