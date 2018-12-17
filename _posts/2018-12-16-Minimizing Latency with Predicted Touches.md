---
layout: post
current: post
cover:  assets/images/ios.png
navigation: True
title: "Minimizing Latency with Predicted Touches"
date: 2018-12-16 00:00:00
tags: [Development, iOS, Apple Developer Documentation]
class: post-template
subclass:  'post tag-development'
author: leegwangyong

---
It takes time for UIKit to generate and deliver touch events to your app, and it takes time for your app to process those events and render the results

## Overview
`UIKit`이 터치 이벤트를 생성하여 전달하는데 시간이 걸리며, app이 그 이벤트들을 처리하고 결과를 렌더링하는데에 시간이 걸립니다. 실제로, 이것은 꽤나 시간이 걸리며, 사용자의 손가락 혹은 Apple Pencil의 움직임과 렌더링 결과에 대하여 눈에 보이는 끊김 현상이 발생할 수 있습니다. 터치 입력과 렌더링 내용간의 인지되어진 지연을 최소화시키기 위해, 이벤트 처리 시 예측된 터치를 통합할 수 있습니다.

Predicated touche는  다음 터치 이벤트가 어느 곳에서 발생할지에 대한 시스템의 최선의 추측입니다. Drawing Sequence 가 발생할 때,  `UKit`은 사용자의 손가락 혹은 Apple Pencil로 부터의 터치 위치를 사용하여  '다음 터치가 어디서 발생할 것인지' 예측합니다. `UIKit`은 이 예측된 위치에 대한 추가적인 `UITouch`를 생성하고 app에서 사용가능하게 합니다.

![그림1](https://docs-assets.developer.apple.com/published/7c21d852b9/333cec5b-725a-44ed-a460-ae15b99a57ed.png)

예측된 터치 정보를 가져오기 위해서는 본래의 `UITouch`를 포함하고 있는 `UIEvent`의 [`predictedTouches(for:)`](https://developer.apple.com/documentation/uikit/uievent/1613814-predictedtouches) 를 호출하면됩니다. 이 method는 마지막 실제 터치 이후에 발생될 것으로 예측되어지는 터치 배열을 반환합니다. **예측 되어진 터치는 항상 일시적인 데이터로 취급하고, 새로운 터치 이벤트가 발생하면 버려야합니다.**

# Reference

- Apple Developer Documentation
	- [Minimizing Latency with Predicted Touches](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_touches_in_your_view/minimizing_latency_with_predicted_touches)
