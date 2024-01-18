1. Singleton pattern:
앱 전역에 걸쳐 공유되는 resource에 접근할 수 있는 단일점을 제공해주는 디자인 패턴. 
(Provide access to a shared resource using a single, shared class instance.)
\
\
**Singleton은 왜 좋지 않다고 여겨질까?**
- Singleton의 state는 전역적으로 공유된다. State의 예기치 못한 변화는 bug를 만들어내기 쉬운 원이이 되므로 주의가 필요하다.
- Signleton과 그것을 이용하는 객체 간 관계가 명확하지 않다. 스파게티 코드를 만들게 된다.
- Life cycle을 관리하기가 어렵다.
- Singleton에 정의된 property들은 optional로 접근하게 되는데, 해당 property에 접근하고자 하는 때에 값의 존재 여부가 보장되지 않으므로 bug가 발생하기 쉽게 된다. 

이러한 이유들로 인해, Singleton보다는 DI를 사용하는 것이 권장된다.

https://www.swiftbysundell.com/articles/avoiding-singletons-in-swift/