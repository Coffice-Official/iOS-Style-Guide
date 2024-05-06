# Coffice iOS app Environment History

- app status : iOS16+ / Xcode 15.2 / Tuist 3.42.2 / TCA 1.7.3
  - v1.4 ~



# iOS-Style-Guide

This is Coffice iOS App's style guide line. ⚡️


### Coffice iOS app style guide

Coffice 팀 구성원들이 SwiftUI framework, TCA architecture를 기반의 Coffice iOS앱 개발에 참고할 수 있는 style guide를 작성합니다.



## swift style guide

본 문서에서 다루지 않는 기타 컨벤션 룰은 kodeco의 [swift style guide](https://github.com/kodecocodes/swift-style-guide), swift lint 기본 rule을 따릅니다.


### indentation

- SwiftUI framework 기반 코드베이스 개발의 코드 깊이가 깊어질 수 있는 특성을 고려해서, 코드 가독성을 위해 기본 indent는 2칸을 지정하여 사용합니다.


### 기타 컨벤션

개발과정에서 자주 보일 수 있는 기타 컨벤션 룰을 정의합니다. kodeco swift style guide에도 중복 언급 될 수 있지만, 리마인딩차원에서 작성합니다.

- 공백라인은 빈 공백을 넣지 않고 비워둡니다.

- import는 사전순으로 작성합니다.

  ```swift
  import ComposableArchitecture
  import SwiftUI
  import WebKit
  ```

- self 키워드는 꼭 넣어야 하는 경우에만 명시합니다.

- guard문 끝의 else는 한번 개행해줍니다.



## TCA style guide

### Action 반환

- 단발성으로 처리되는 UI 액션, delegate 이벤트로 사용되는 action들은 .send(.foo), .run { ... } 방식으로 action을 반환할 수 있다. 

- 그 외 기타 shared logic들은 성능상 이점을 위해 State 내의 mutating func으로 처리될 수 있다.
  - [참고, TCA performance](https://pointfreeco.github.io/swift-composable-architecture/main/documentation/composablearchitecture/performance/)

  ```swift
  @Reducer
  struct SomeReducer {
    struct State: Equatable {
      mutating func updateSomething -> Effect<Action> {
        // ...
        return .send(.updateAdditionalThings)
      }
    }
    
    // ...
  }
  ```



### 프로젝트 이슈 해결방법 공유

- TCA Reducer를 사용하는 SwiftUI View의 preview crash 문제
  - Aautomatically Refresh Canvas 옵션 비활성화 후 해결

  <img width="500" alt="issue solving example" src="https://github.com/applebuddy/SeminarMemo/assets/4410021/77e4aedd-b957-445f-8456-0563bca54fbb">

- [메모리릭 이슈 간단하게 확인하는 몇가지 방법](https://0urtrees.tistory.com/420)
- [Xcode 15.2, Package.resolved PinsStorage version 이슈 해결방법](https://0urtrees.tistory.com/419)
