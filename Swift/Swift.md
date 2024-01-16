### **Swift**: Advanced features and best practices.
1. **Swift의 옵셔널 체이닝(Optional Chaining)은 어떤 상황에서 사용하는 것이 가장 효과적인가요?**
    - 옵셔널 체이닝과 강제 언래핑(Forced Unwrapping)의 차이점을 어떻게 설명하시겠습니까?
    \
    \
    옵셔널은 값이 있을 수도 있고 없을 수도 있다는 것을 나타내는 타입입니다. 옵셔널 체이닝은 값이 nil일 수도 있는 옵셔널 타입의 값에 `?`를 사용해서 프로퍼티나 메서드 등을 호출하는 방식을 의미합니다. 값이 존재하는 경우에만 성공하므로, 원하는 프로퍼티나 메서드 호출이 성공하는 지 확인하기 위해서 사용합니다.
    \
    \
    강제 언래핑은 `!` 를 사용해서 옵셔널의 값을 강제로 언래핑하는 방식입니다. 만일 옵셔널이 값을 갖지 않은 경우라면 runtime error가 발생하게 되므로 값이 확실히 있는 경우에만 주의해서 사용해야하는 방식입니다.
    

2. **Swift에서의 메모리 관리 방법(ARC)에 대해 설명하고, 순환 참조(Circular Reference)를 방지하기 위한 전략은 무엇인가요?**
    - 순환 참조를 해결하기 위한 `weak`와 `unowned` 참조의 차이점은 무엇인가요?
    - ARC를 효과적으로 관리하기 위한 코드 작성 방법은 어떤 것이 있나요?
\
\
    ARC는 Swift의 메모리 관리 방식입니다. 객체의 life time을 reference count로 관리하는 방식입니다. ARC는 class instance들이 더 이상 사용되지 않는 시점에 메모리에서 해제합니다. 
    \
    \
    weak와 unowned는 둘 다 순환 참조를 방지하기 위한 방식으로, reference count를 증가시키지 않습니다. weak는 객체가 nil일 수 있을 때 사용하고 unowned는 항상 값을 가질 때 사용해야 합니다. 
    \
    \
    ARC를 효과적으로 관리하기 위해서는, weak나 unowned같은 keyword를 적절하게 사용해도 되고, 또 life cycle로 인한 bug를 막기위해서 접근 제어자를 private으로 제한해서 메모리에서 객체가 해제되었을 때에 외부에서 접근을 시도하지 못하도록 하는 방식을 사용하는 것도 좋습니다. 뿐만 아니라, 순환참조 자체가 발생하지 않도록 model design을 tree 구조로 변경한다던지, function에서는 defer과 같은 방식을 사용하는 것도 도움이 됩니다.



3. **Swift의 프로토콜 지향 프로그래밍(Protocol-Oriented Programming)의 장점은 무엇이며, 이를 클래스 기반 프로그래밍과 비교했을 때 어떤 차이점이 있나요?**
    - 프로토콜을 활용한 설계에서 주의해야 할 점은 무엇인가요?
    - 프로토콜 확장(Protocol Extension)을 사용하여 코드 재사용성을 높이는 방법은 무엇인가요?
\
\
다중 상속을 지원하지 않는 Swift에서 다중 상속과 유사한 효과를 낼 수 있다는 것이 장점입니다. 그리고 공통적으로 사용될 method나 properties를 정의할 수 있기 때문에, 코드를 모듈화하여 재사용성을 높여준다는 장점이 있습니다. 
class 뿐만 아니라 struct, enum에서 사용 가능합니다. 
\
\
Protocol에 extension을 사용하면, default값이나 기존 값을 override할 수 있습니다. 그래서 반복적으로 동일한 값을 매번 정의할 필요 없이 extension에 명시하여 코드 재사용성을 높일 수 있습니다.


```

예시:

https://www.kodeco.com/6742901-protocol-oriented-programming-tutorial-in-swift-5-1-getting-started

https://byby.dev/swift-protocol-oriented

https://www.hackingwithswift.com/articles/74/understanding-protocol-associated-types-and-their-constraints
(Associatedtype 과 Generic 같이 활용하기!)

```

4. **Swift의 제네릭(Generic)을 사용하는 이점과 구현 시 고려해야 할 사항은 무엇인가요?**
    - 제네릭 타입의 제약 조건(Type Constraints)을 설정하는 방법과 그 중요성은 무엇인가요?
    - 제네릭과 관련된 성능 문제는 어떻게 해결할 수 있나요?

\
\
Generic을 사용하면 코드의 재사용성을 높일 수 있습니다. 예를 들어, Swift Array 같은 경우, 여러 가지 타입을 모두 사용할 수 있는데, 만일 이 때 Generic을 사용하지 않는다면 구체적인 타입별로 지원하는 Array 로직을 만들어 주어야 해서 번거롭고 오류를 양산할 가능성이 생깁니다. 
Generic을 설정하려면, <> 괄호 안에 type의 placement로 사용할 단어를 명시해주고, 해당 단어를 type처럼 사용해주면 됩니다. 


5. **Swift의 함수형 프로그래밍 요소(예: map, filter, reduce)를 사용하는 경우, 어떤 장점이 있으며, 언제 사용하는 것이 적절한가요?**
    - 함수형 프로그래밍 패러다임을 채택함으로써 발생할 수 있는 단점은 무엇인가요?
    - 함수형 프로그래밍과 객체지향 프로그래밍을 어떻게 효과적으로 조합할 수 있나요?
    \
    \
함수형 프로그래밍 요소를 사용하면 깔끔해보이는 코드를 작성할 수 있습니다. 그리고 기존 데이터를 변경하지 않고 새로운 데이터를 만들어서 side effect를 발생시키지 않기 때문에 매번 동일한 결과물을 return할 수 있습니다. 이러한 특성은 결과 예상을 쉽게 하고 테스트를 쉽게 만들어 주는 장점이 있습니다. 

함수형 프로그래밍 요소를 사용하면 조금 더 깔끔해보이는 코드를 작성할 수 있지만, 익숙하지 않은 경우에는 오히려 이해하기가 어려울 수 있다는 한계가 있습니다. 

6. **Swift에서의 오류 처리(Error Handling) 방법과 모범 사례에 대해 설명해 주세요.**
    - 사용자 정의 오류 타입을 만들 때 고려해야 할 사항은 무엇인가요?
    - 오류 전파(Error Propagation)와 오류 처리 패턴의 선택 기준은 무엇인가요?
\
\
Swift에서 오류 처리하는 방식에는 크게 네 가지가 있습니다.
1) 에러를 throw하기: fucntion에서 throws keyword를 return arrow 전에 붙여주어, 해당 function을 호출하는 곳에서 에러를 처리하도록 만듭니다.
2) do catch 구문을 사용합니다. do-catch 구문을 사용해서 에러가 발생하였을 때 어떻게 핸들링 할 것인지 구체적으로 명시해 줄 수 있습니다. catch 구문을 여러번 사용하여 에러 종류별로 다른 액션을 취할 수도 있습니다.\
뿐만 아니라, throws와 do-catch를 같이 사용할 수도 있습니다. 특정한 에러는 핸들링을 바로 하고, 나머지 에러는 propagate하여 다른 호출 부위에서 처리될 수 있도록 하는 것입니다. 

3) try? 를 사용해서 optional value로 변환할 수 있습니다. 모든 에러들을 동일하게 다루고 싶을 때 try?를 사용하면 간결하게 코드를 작성할 수 있습니다.
4) try! 를 사용해서 에러를 발생시키지 않도록 할 수도 있습니다. 이는 run time에 에러가 발생하지 않을 것이라는 게 확실한 경우에만 사용해야 합니다.
`let photo = try! loadImage(atPath: "./Resources/John Appleseed.jpg")`
위의 예시처럼 jpg 이미지가 앱과 함께 전달이 되는 경우에는 image load가 실패할 일이 없으므로 try!를 사용해서 에러 처리를 간결하게 하였습니다.

어떤 식으로 에러 처리를 하게 되든, block이 끝나기 전에 수행되어야 할 작업이 있다면 defer에 명시해주면 됩니다.


참고자료
 https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling/


7. **Swift의 클로저(Closure) 사용 시 성능적인 측면을 고려해야 하는 경우는 어떤 것들이 있나요?**
    - 클로저에서 메모리 누수(Memory Leak)를 방지하기 위한 전략은 무엇인가요?
    - 클로저를 사용하여 비동기 작업을 관리하는 방법은 무엇인가요?





8. **Swift의 패턴 매칭(Pattern Matching) 기능을 효과적으로 사용하는 방법은 무엇인가요?**
    - `switch` 문과 패턴 매칭을 사용할 때의 모범 사례는 무엇인가요?
    - 패턴 매칭을 사용하여 복잡한 데이터 구조를 처리하는 예시는 무엇인가요?

\
\
패턴은 단일 또는 복합 value의 `structure`를 의미합니다. 예를 들어서, tuple의 구조는 comma로 나뉘는 두 elements라고 할 수 있습니다. 패턴은 특정한 값이 아니라 값의 구조를 나타내기 때문에, 여러가지 값과 매치될 수 있습니다. 예. (x, y) 패턴은 (1, 2), (10, 23) 등과 매치될 수 있다.

\
패턴 매칭을 사용하여 복잡한 데이터 구조를 처리하는 예시:\
optional value array를 for loop으로 순회할 때, case let을 사용해서 nil값이 아닌 값들만 처리할 수 있다. compactMap을 사용하는 것과 동일한 효과를 갖는다.
```swift
let arrayOfOptionalInts: [Int?] = [nil, 2, 3, nil, 5]
// Match only non-nil values.
for case let number? in arrayOfOptionalInts {
    print("Found a \(number)")
}
// Found a 2
// Found a 3
// Found a 5
```
https://docs.swift.org/swift-book/documentation/the-swift-programming-language/patterns/



9. **Swift의 효율적인 컬렉션 사용 방법에 대해 설명해 주세요. 배열(Array), 딕셔너리(Dictionary), 세트(Set) 사용 시 성능에 영향을 미치는 요소는 무엇인가요?**
    - 큰 데이터 세트를 처리할 때 컬렉션의 성능을 최적화하는 방법은 무엇인가요?
    - 컬렉션 타입의 선택 기준은 어떻게 결정하나요?

Array: 배열은 순서가 있고 index로 접근이 가능합니다. Index를 사용해서 데이터에 접근하므로, index를 알고 있으면 O(1)으로 데이터를 빠르게 찾을 수 있습니다. 하지만 데이터를 삭제하거나 삽입하는 경우 모든 데이터를 이동해야 해서 비교적 느린 성능을 보입니다.
\
Set: Set은 순서가 없고 중복을 허용하지 않는 컬렉션입니다. 순서가 없기 때문에 index로 데이터에 접근할 수는 없습니다. Set에는 Hashable한 type만 저장될 수 있습니다. 
\
 Dictionary는 key-value pair로 이루어졌고 순서가 없는 컬렉션입니다. key값을 알고 있다면 데이터를 빠르게 찾을 수 있습니다.


10. **Swift의 모듈화 및 패키지 관리를 위한 전략은 무엇이며, 이를 통해 얻을 수 있는 이점은 무엇인가요?**
    - Swift Package Manager의 사용 방법과 이점은 무엇인가요?
    - 모듈화된 코드베이스를 유지 관리하는 데 있어서 고려해야 할 주요 요소는 무엇인가요?

접근 제어자를 잘 활용하는 것과 코드 블록이 최소한의 기능을 담고 있는지 여부 라고 생각합니다. 
모듈은 프로젝트 전역에서 사용되므로, 접근 허용 범위를 명확하게 규정하여야 의도치 않은 결과가 생기지 않을 것입니다. 그리고 하나의 function이나 property가 너무 포괄적인(혹은 여러가지) 행동을 한다면, 활용성이 저하될 수 있으므로 기능을 분리해서 작성하는 것이 중요하다고 생각합니다.


11. **Swift의 접근 제어(Access Control)를 활용한 안전한 코드 작성 방법은 무엇인가요?**
    - 접근 제어를 통해 코드의 캡슐화를 강화하는 방법은 무엇인가요?
    - `public`, `private`, `internal`, `fileprivate`, `open` 접근 수준의 차이점과 사용 상황은 무엇인가요?
    \
    \

Access Control은 다른 소스 파일이나 모듈에서 코드에 접근 하는 것을 제한 하기 위한 방식입니다. 코드의 캡슐화를 강화하려면, 외부에서 접근을 제한하도록 접근 제어자를 설정해주면 됩니다. 예를 들어서, constant나 variable의 외부에서의 변경을 막기위해서 private으로 설정한 다음, internal 혹은 public의 getter method를 만들어서 read-only만 가능하도록 할 수도 있습니다. 아니면 프로퍼티의 set인 경우만 접근 제어자가 private이 되도록 설정할 수도 있습니다. 
\
\
-  open: Subclassing과 override 허용. class와 class member에게만 사용 가능. module 내/외의 모든 source file에서 접근 가능.
-  public: Subclassing과 override 불가. module 내/외의 모든 source file에서 접근 가능.
-  internal: 해당 모듈 내 모든 source file에서 접근 가능.
-  file-private: 정의되어 있는 source file에서만 접근 가능.
-  private: 선언된 곳과 extension 내에서만 접근 가능.

https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol/

    
12. **Swift의 확장(Extension) 사용 시 모범 사례는 무엇이며, 확장을 사용할 때의 주의점은 무엇인가요?**
    - 확장을 통해 기존 타입에 기능을 추가할 때의 이점과 한계는 무엇인가요?
    - 기존 클래스나 구조체에 확장을 추가할 때, 충돌 방지를 위한 전략은 무엇인가요?
\
\
Extensions은 존재하는 class, structure, enum or protocol type에 **새로운 기능을 추가** 하는 방식입니다. original source code에 접근 권한이 없는 경우에도 적용할 수가 있습니다 (retroactive modeling). Objective-C의 Category와 유사한 개념입니다.
\
Extension은:
- computed instace properties 와 computed type properties를 추가할 수 있습니다.
- instance methods와 type methods를 정의할 수 있습니다.
- 새로운 initializer를 추가할 수 있습니다.
- subscripts를 정의할 수 있습니다.
- nested types을 정의하고 사용할 수 있습니다.
- 존재하는 type이 protocol에 conform하도록 할 수 있습니다.
\
\
주의해야 할 사항은, extension을 사용하게 되면서 여러가지 기능을 많이 넣게 될 수 있는데, OOP의 원칙 중 하나인 single responsibility를 어기게 될 수 있다는 것을 염두에 두어야 한다.

13. **Swift에서의 런타임 최적화 방법은 무엇이며, 성능 분석을 위한 도구 사용 방법은 어떻게 되나요?**
    - 코드 최적화를 위한 프로파일링 도구의 사용 예시는 어떤 것들이 있나요?
    - 런타임 성능에 영향을 미치는 주요 요소들은 무엇인가요?

     \
     \
     런타임 성능 향상을 위해서 동적 디스패치를 줄이는 방법이 있다. Dynamic(동적) Dispatch는 줄이고 Static(정적) Dispatch를 주로 사용하는 것이다. Static Dispatch는 런타임에서 판단할 필요가 없기 때문에 런타임 성능에 이점이 있다. 값, 참조 타입 모두 지원하며 열거형과 구조체는 여기에 속한다.\
     Dynamic dispatch는 참조타입만 지원한다. 상위 혹은 하위 클래스의 method 참조해야하는 지 재정의의 가능성으로 인해 컴파일 타임에 결정할 수가 없어서 런타임에 결정된다. \
     access control과 final keyword를 이용해서 성능 향상에 도움을 줄 수 있습니다.
     \
     \
     코드 최적화를 위한 프로파일링 도구에는 `instruments`가 있습니다.
     //TODO: 자세한 내용 추가하기.

14. **Swift의 리터럴과 연산자 오버로딩을 통해 얻을 수 있는 이점과 주의사항은 무엇인가요?**
    - 사용자 정의 타입에 대한 리터럴 표현을 구현하는 방법은 무엇인가요?
    - 연산자 오버로딩을 사용할 때 코드의 가독성과 유지보수성에 미치는 영향은 무엇인가요?




15. **Swift에서의 Type Inference(타입 추론)의 작동 원리와 효율적 사용을 위한 전략은 무엇인가요?**
    - 타입 추론이 컴파일 시간에 미치는 영향은 무엇인가요?
    - 명시적 타입 선언과 타입 추론 중 어느 경우가 더 바람직한가요?
16. **Swift의 Associated Types(연관 타입)에 대해 설명하고, 프로토콜에서 이를 사용하는 방법과 장점은 무엇인가요?**
    - 연관 타입을 사용하는 예시와 그 이점은 무엇인가요?
    - 연관 타입을 사용할 때 제네릭과의 관계는 어떻게 되나요?
17. **Swift의 키-값 관찰(Key-Value Observing, KVO)과 프로퍼티 옵저버(Property Observer)의 차이점과 각각의 사용 시나리오는 무엇인가요?**
    - KVO를 사용할 때의 주의사항은 무엇인가요?
    - 프로퍼티 옵저버를 통해 얻을 수 있는 이점과 한계는 무엇인가요?
18. **Swift의 델리게이트 패턴(Delegate Pattern)을 사용하여 컴포넌트 간 통신을 구현하는 방법은 무엇인가요?**
    - 델리게이트 패턴의 장단점은 무엇인가요?
    - 델리게이트 패턴과 노티피케이션 센터(Notification Center)를 비교했을 때의 차이점은 무엇인가요?
19. **Swift의 리플렉션(Reflection)과 메타 타입(MetaType)을 사용하는 경우와 주의사항은 무엇인가요?**
    - 리플렉션을 사용하는 예제는 무엇인가요?
    - 리플렉션을 사용할 때의 성능적 영향은 어떤 것이 있나요?
20. **Swift의 커스텀 서브스크립트(Custom Subscript) 구현 방법과 사용 시의 이점은 무엇인가요?**
    - 서브스크립트를 사용하여 컬렉션 또는 클래스의 데이터 접근을 단순화하는 방법은 무엇인가요?
    - 서브스크립트 오버로딩을 사용하는 경우의 예시는 무엇인가요?
21. **Swift에서의 비동기 이미지 로딩과 캐싱을 위한 전략은 무엇인가요?**
    - 이미지 로딩 시 성능과 메모리 관리를 최적화하는 방법은 무엇인가요?
    - 네트워크로부터 이미지를 비동기적으로 로딩하고 캐싱하는 프로세스를 설계하는 방법은 무엇인가요?
22. **Swift의 커스텀 연산자(Custom Operator)를 정의하고 사용하는 방법은 무엇인가요?**
    - 커스텀 연산자를 사용할 때의 이점과 잠재적 위험은 무엇인가요?
    - 커스텀 연산자의 가독성과 유지보수에 미치는 영향은 어떻게 되나요?