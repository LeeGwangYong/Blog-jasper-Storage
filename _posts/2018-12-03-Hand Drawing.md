---


---

<hr>
<p>layout: post<br>
current: post<br>
cover:  assets/images/ios.png<br>
navigation: True<br>
title: “iOS Hand Drawing Apple Documentation”<br>
date: 2018-12-3 00:00:00<br>
tags: [Development, iOS]<br>
class: post-template<br>
subclass: ‘post tag-development’<br>
author: leegwangyong</p>
<hr>
<h1 id="touches-presses-and-gestures"><a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures">Touches, Presses, and Gestures</a></h1>
<p>앱의 gesture recognizer에 대한 event-handling logic을 캡슐화함으로써,  앱 전반적으로 해당 코드를 재사용할 수 있습니다.<br>
However, if you use custom views to display your content, you must handle all touch events that occur in your views. There are two ways to handle touch events yourself.<br>
만약, cutom view를 사용한다면,  view에서 발생하는 touch event들에 대해서 모두 처리를 해야합니다.</p>
<p>Touch event를 처리하는 방법은 2가지가 존재합니다.</p>
<ul>
<li>Gesture Recognizer를 이용하여 track ( <a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_uikit_gestures">Handling UIKit Gestures</a> )</li>
<li><code>UIView</code> subclass에서 직접적으로 track ( <a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_touches_in_your_view">Handling Touches in Your View</a> )</li>
</ul>
<h1 id="using-responders-and-the-responder-chain-to-handle-events"><a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/using_responders_and_the_responder_chain_to_handle_events">Using Responders and the Responder Chain to Handle Events</a></h1>
<p>App에서 _Responder Object_를 이용하여 event를 받고, 처리합니다.<br>
Responder Object는 <code>UIResponder</code> 클래스의 모든 인스턴스이며 공통 하위 클래스에는 <code>UIView</code>, <code>UIViewController</code> 및 <code>UIApplication</code>이 포함됩니다.<br>
Responder는 raw event data를 받고 event를 처리하거나 다른 responder object로 전달합니다. App이 event를 받았을 때, UIKit은 자동적으로 해당 event를 가장 적합한 responder object( <em>the first responder</em> )로 보내줍니다.</p>
<p>처리되지않은 event들은 the active <strong>responder chain</strong> 을 통하여 responder에서 responder로 보내지며, 이것은 responder object의 the dynamic configuration입니다.</p>
<p>아래의 그림은 label, textField, button, 2개의 background View가 포함된 interface가 있는 app의 responder를 보여주고 있습니다. 이 다이어그램은 the responder chain을 따라 어떻게 event들이 responder에서 다음 responder로 이동하는지 보여줍니다.<br>
<img src="https://docs-assets.developer.apple.com/published/7c21d852b9/f17df5bc-d80b-4e17-81cf-4277b1e0f6e4.png" alt="The active responder chain"></p>
<ol>
<li>만약 textField가 event를 처리하지 않는다면, <code>UIKit</code>은 textField의 parent <code>UIView</code>로 event를 보낸 후, window의 root view로 보냅니다.</li>
<li>Event를 window로 바로 보내기 전에, root view에서는 responder chain이 event를 ViewController로 우회시킵니다.</li>
<li>만약 Window가 event를 처리하지 못한다면, <code>UIKit</code>은 <code>UIApplication</code> object로 event를 전달합니다. 그리고, 해당 object가 <code>UIResponder</code>의 instance이고 아직 responder chain의 일부가 아니라면,  <code>UIApplicationDelegate</code>에 전달합니다.</li>
</ol>
<blockquote>
<p>If the window cannot handle the event, UIKit delivers the event to the <code>UIApplication</code> object, and possibly to the app delegate if that object is an instance of <code>UIResponder</code> and not already part of the responder chain.</p>
</blockquote>
<h3 id="determining-an-events-first-responder">Determining an Event’s First Responder</h3>
<p>UIKit은 event의 유형에 따라 object를 <em>the first responder</em>로 임명합니다.</p>

<table>
<thead>
<tr>
<th>Event Type</th>
<th>First Responder</th>
</tr>
</thead>
<tbody>
<tr>
<td>Touch events</td>
<td>Touch가 발생한 View</td>
</tr>
<tr>
<td>Press events</td>
<td>초점이 맞추어진 Object</td>
</tr>
<tr>
<td>Shake-motion events</td>
<td>The object that you (or UIKit) designate.</td>
</tr>
<tr>
<td>Remote-control events</td>
<td>The object that you (or UIKit) designate.</td>
</tr>
<tr>
<td>Editing menu messages</td>
<td>The object that you (or UIKit) designate.</td>
</tr>
</tbody>
</table><p>Accelerometers, gyroscopes, magnetometer과 연관된 Motion event들은 responder chain을 따르지 않습니다. 대신, Core Motion은 이 event들을 임명된 object들로 직접적으로 전달합니다. ( <a href="https://developer.apple.com/library/archive/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW27">Core Motion Framework</a> )</p>
<p>Control들은 연관된 target object와 action message를 이용하여 직접<br>
통신합니다. 사용자가 Control과 상호작용할 때, Control은 target object에 action message를 보냅니다.<br>
Action Message는 event가 아니지만, responder chain을 활용할 수 있습니다.<br>
Control의 target object가 <code>nil</code>일 경우, UIKit은 target object에서 시작하여 적절한 action method를 구현하는 object를 찾을때 까지 responder chain을 가로지릅니다. 예를 들어, UIKit editing menu는 이 동작을 사용하여 <code>cut(_:)</code>, <code>copy(_:)</code>, <code>past(_:)</code>와 같은 method를 구현하는 responder object를 찾습니다.</p>
<h1 id="reference">Reference</h1>
<ul>
<li>Apple Documentation
<ul>
<li><a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures">Touches, Presses, and Gestures</a>
<ul>
<li><a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/using_responders_and_the_responder_chain_to_handle_events">Using Responders and the Responder Chain to Handle Events</a></li>
<li>Use gesture recognizers to track the touches, <a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_uikit_gestures">Handling UIKit Gestures</a>.</li>
<li>Track the touches directly in your <a href="https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_touches_in_your_view">Handling Touches in Your View</a>.</li>
</ul>
</li>
<li><a href="https://developer.apple.com/videos/play/wwdc2015/233/">Advanced Touch Input on iOS (2015)</a></li>
<li><a href="https://developer.apple.com/videos/play/wwdc2016/220">Leveraging Touch Input on iOS (2016)</a></li>
</ul>
</li>
</ul>

