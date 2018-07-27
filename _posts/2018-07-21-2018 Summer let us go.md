---
layout: post
current: post
coverURL: "https://ws3.sinaimg.cn/large/006tKfTcgy1fto5y1rgmbj30m80ci74w.jpg"
navigation: True
title: "let us: Go! 2018 Summer 노트"
date: 2018-07-21 00:00:00
tags: [iOS, Seminar]
class: post-template
subclass: 'post tag-seminar'
author: leegwangyong
---

행사일정![image-20180721130817122](https://ws2.sinaimg.cn/large/006tNc79gy1fthfw4j6akj31kw11xjvw.jpg){: width="100%" height="100%"}

------

# 1. Xcode에서 디버깅 시작하기 - 이재성님

- ### Breakpoint 
  ![image-20180721131739056](https://ws2.sinaimg.cn/large/006tNc79gy1fthfua1uk5j312c09omzc.jpg){: width="100%" height="100%"}

  Break Point Navigator
  ![image-20180721131912625](https://ws3.sinaimg.cn/large/006tNc79gy1fthfubunodj30gg0eadhi.jpg){: width="100%" height="100%"}

  General Breakpoint
  ![image-20180721131957312](https://ws2.sinaimg.cn/large/006tNc79gy1fthfuaxuw4j30f408a0tt.jpg){: width="100%" height="100%"}

- ### lldb
  - lldb란?
    - Xcode에 기본으로 내장되어있는 디버거
    - GDB 스타일의 명령어를 사용가능
    - [lldb.llvm.org/lldb-gdb.html](http://lldb.llvm.org/lldb-gdb.html)
  - Command
    - print : 출력
      - p/x 16 : Hexadecimal
      - p/t 16 : Binary
    - expr : 값의 변경
    - po (print object)
  - 변수 선언
    - `e let $a = 2`
    - `p $a * 19`
    - ![image-20180721133051191](https://ws4.sinaimg.cn/large/006tNc79gy1fthfue38n9j30ye0imjue.jpg){: width="100%" height="100%"}

  - Tip
    - closure에서  `fr v %a` 를 사용
      ![image-20180721133203023](https://ws1.sinaimg.cn/large/006tNc79gy1fthfucn37rj30f202iq37.jpg){: width="100%" height="100%"}
    - Symbolic Breakpoint : 모든 `viewDidLoad`에서 break가 걸린다.
      ![image-20180721133242890](https://ws2.sinaimg.cn/large/006tNc79gy1fthfw5wozhj30qa0auwg7.jpg){: width="100%" height="100%"}
      ![image-20180721133432414](https://ws2.sinaimg.cn/large/006tNc79gy1fthfw38dnyj30f00lswhy.jpg){: width="100%" height="100%"}

- ### Symbolicate
  - crash log
  - dSYMS file
  - Archive - Crash
- ### ETC
  - View hierarchy
  - Debug
    ![image-20180721133831558](https://ws1.sinaimg.cn/large/006tNc79gy1fthfug7y17j31g00a40vd.jpg){: width="100%" height="100%"}
    ![image-20180721133908836](https://ws3.sinaimg.cn/large/006tNc79gy1fthfw1khgbj30bs06e3yu.jpg){: width="100%" height="100%"}

후기 : 아직도 배워야할 것이 많다는 것을 느꼈습니다. iOS, Swift뿐만 아니라 Xcode를 적극 활용할 수 있는 방법들도 조금씩 익혀야겠습니다. lldb를 사용한 부분이 흥미로웠으며, 디버깅에 꼭 사용을 해봐야겠습니다.

------
# 2. 코드 응집도 높이기 - 곰튀김님

**Code Defragment** : 파편화되어 있는 코드들을 응집시키자
**EASY to read, follow, understand, find, maintenance**
**wrapper를 만들어 응집시킨 후 closure를 이용하자.**

- Case #1 : Data + Logic + UI
  - Model, Context(Business Logic), ViewController
  - View → ViewController → ViewModel(Context) → Model
- Case #2 : Data Setter
  - `didSet` 

```swift
class ViewController: UIViewController {
    @IBOutlet var label: UILabel!    
    var count: Int = 0 {
        didSet {
            self.label.text = "\(count)"
        }
    }
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    func addOne() {
        count += 1
    }
    func minusOne() {
        count += 1
    }
}
```

- Case #3 :  Override
  - BaseViewController를 이용
  - `self.rx.viewWillAppear`

- Case #4 : Selector
  - Wrapper
  - `NotificationCenter.default.rx.notification()`

- Case #5 : Delegate
  - Wrapper
  - `picker.rx.didFinishPickingMediaWithInfo`

> - 관련 사이트
>   - [https://github.com/iamchiwon/CodeCohensive](https://github.com/iamchiwon/CodeCohensive)
>   - [코드 응집도 높이기 - 곰튀김님 슬라이드](https://www.slideshare.net/ChiwonSong/20180721-code-defragment-106434267)

후기 : 항상 고민하던 부분이였는데, 이런 것을 케이스를 나누어 정리해주시다니! 곰튀김님의 발표를 듣고 그래도 조금이나마 도움이 되었습니다.  뒷풀이에서 들은 얘기로 ''실제 개발에서 코드 응집도를 모두 높일 순 없다''는 말을 들었는데, 맞는 말이라고 생각합니다. 그래도 조금이라도 응집도를 높일 수 있는 방법을 고안하고, 실천해봐야겠습니다다. + Rx 공부 필수로 해야겠습니다. 😭

------

# 3. Observable Operator 적재적소 사용하기 - 엉덩숭아님

- ### FlatMap

  - `flatMap`

  ```swift
  Observable<Int>.just(10)
    .flatMap {
        return Observable<String>.repeatElement("elemnet").take(element)
    }.subscribe()
    .disposed(by: disposeBag)
  ```

  ```swift
  button.rx.tap.flatMap {
      return apiCall
  }
  ----------------------------------------------------------
  button.rx.tap.flatMap {
      return Observable<Int>
      	.interval(1, scheduler: MainScheduler,instance)
      	.take(3)
  }
  // 3번 연속 누르게된다면, event가 뒤섞이게 된다.
  ```
  - `flatMapFirst` : 먼저 생성된 옵저버블이 끝나기 전 까지 들어오는 이벤트를 무시한다.
  - `flatMapLatest` : 이벤트가 들어오면 앞에 생성된 옵저버블을 무시한다.

- ### Side Effect
  - side effect가 존재하면 안되는 곳 : `map`, `flatMap`
  - side effect가 존재해도 괜찮은 곳 : `do`, `subscribe`
  - **withLatestFrom**
    ```swift
    sendButton.rx.tap.flatMap { [weak self] in
    	send(message: self?.textField.text) //클로저 외부를 직접 접근
    }
    ----------------------------------------------------------
    sendButton.rx.tap
    .withLatestFrom(textField.rx.text) //인자로 넣는다
    .flatMap { message in
        send(message: message) //텍스트를 매개변수로 받아옴
    }
    ```

- ### Example
  - **`interval`**
    **`window`** : 하나의 observable을 여러 개의 observable로 만든다.
    ```swift
    Observable<Int>
    .interval(0.5, scheduler: MainScheduler.instance)
    .window(timeSpan: 100, count 6, scheduler: MainScheduler.instance)
    .flatMap {
        $0.do(onSubscribed: { [weak self] in
            self?.blink()
        })
    }
    ```
  - **`Scan`** : 이전 이벤트와 현재 들어온 이벤트를 가지고 현재 발행할 새 이벤트를 만든다.
    ```swift
    let numberInputs: [Observable<Int>] = buttons.enumerated()
    .map{ (index, button) in
        button.rx.tap.map {index}
    }
    let numberInput = Observable<Int>.merge(numberInputs)
    let number = numberInput.scan(0, accumulator: { (answer, element) → Int in
    	return answer * 10 + element
    })
    ```
  - **`Switch`** : 내부의 observable을 새 observable로 갈아치운다. (여러 개의 observable을 하나의 observable로 만든다. window의 역버전)
    ```swift
    EmoticonKeyboardService.instance.rx.emoticons(id: 100)
    .subscribe()
    .disposed(by: disposeBag)
    ```

후기 : Rx에 대하여 정말 기초적인 개념만 갖고 들어서 너무 아쉬웠습니다. 만약 Rx에 대한 공부를 한 후 들었더라면 정말 많은 공부가 되었을 텐데! Rx를 공부한 후 다시 한번 봐야겠습니다.

------
# 4. iOS TDD 실무에 적용하기 - AnyObject님
- ### iOS TDD 실무에 적용하기

  - 지식을 전달하는 방법
  - 동료 설득하기(다양한 타입의 개발자) - 존중 받는 느낌이 들게, 함께 찾아내 보자(철저한 준비 필수)
  - 계획하기 : 가능하면 자세하게, 빼먹지 말 것, 유지하기, 지속적인 게획 업데이트, 변경되는 기획
  - **디자인, 기획, 서버가 완전히 끝나야 개발을 시작할 수 있다고 생각해서는 안된다.**

- ### iOS TDD

  - 테스트 타겟을 메인 타겟에서 분리해서 실행
  - Testing Tips & Tricks
  - 레거시 코드
  - 사례
    1. 서버 API가 아직 준비되지 않았을 경우
       - Massive VC→MVVM + 책임 나누기 → DTO를 이용한 외부 의존성 분리
    2. UI
    3. 라이브러리 학습 테스트
  - 단계
    1. 실패하는 테스트
    2. 가장 빨리 성공하게
    3. 리펙토링
       1. 중복을 제거
       2. 의미를 드러낸다.(명확하게)

> - 관련 도서 : [테스트 주도 개발 : 고품질 쾌속개발을 위한 TDD 실천법과 도구](http://www.hanbit.co.kr/store/books/look.php?p_code=B3818551654)
> - 관련 사이트
>   - [Testing Tips & Tricks - WWDC 2018 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2018/417/)
>   - [Https://github.com/vbmania/CountdownTimerTddExam](Https://github.com/vbmania/CountdownTimerTddExam)

후기 : 'TDD를 실무에 적용한다'는 것이 정말 많은 과정이 필요하다는 것을 느꼈습니다. 특히나 다른 개발 동료, 그 외의 인원들을 설득하고, 짜임새 있게 나가는 과정들이 초반에는 정말 힘이 들겠지만, 이후에 날개를 달아주기 위해서는 꼭 필요한 과정이라고 생각합니다. 후에 TDD로 개발을 해볼 기회를 만들어야겠습니다.

------

# 5. Texture Reactive Wrapper  만들고 응용하기

- ### Texture

  - ASDipslayNode
    1. Make Subclass
    2. Make Components
    3. Init
       - `self.automaticallyManagerSubnodes = true` : 하위 노드들에 대한 관리를 한다. `addSubview`가 할 필요가 없다.
  - 특징
    - **Trhead Safe** : Thread 사용에 대하여 엄격하다. Main Thread에 접근하면 Crash `ASDisplayNodeAssertMainTrhead();` 
    - Constraints 지옥 탈출, **`LayoutSpec` 사용**
    - **Node Wrapper**
  - Texture Reactive Wrapper
    - 제한적인 RxCocoa 사용

> 관련 사이트 : [Texture](http://texturegroup.org)

후기 : 이전에 Vingle에서 진행했던 세미나의 내용과 유사하였지만, 그럼에도 흥미로웠습니다. 이전부터 Texture의 UI 처리 속도가 정말 놀라워 사용해보고 싶었습니다. 개인 프로젝트에라도 꼭 Texture를 사용해봐야겠습니다.

------

# 6. 미리보는 Marzipan

macOS 기반에서 iOS 기반의 앱을 돌릴 수 있게

macOS위에서 AppKit(macOS Frameworks )과 UIKit(iOSMac Frameworks)을 같이 돌릴 수 있다.

> 관련 사이트 : [Marzipanify](https://github.com/steventroughtonsmith/marzipanify)

후기 : 사람들의 반응이 가장 좋았다고 생각하는 마지막 Marzipan. Swift를 이용하여 만든 UIKit iOS의 어플리케이션이 macOS에서 구동되는 시연은 매우 흥미로웠습니다. 모든 iOS 어플리케이션이 macOS에서 돌아가는 날이 빨리 왔으면 좋겠습니다.