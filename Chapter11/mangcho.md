# 좋은 코드, 나쁜 코드 (11) 단위 테스트의 실제

date: March 10, 2024
preview: 좋은 코드, 나쁜 코드 11장을 읽고 정리한 글입니다.

---

### 💭 기능뿐만 아니라 동작을 시험하라

단순히 눈에 보이는 대로 함수 이름을 테스트 목록에 넣기보다는 함수가 수행하는 모든 동작으로 목록을 채우는 것이 좋다. 

한 메서드는 다음과 같은 동작을 한다고 생각하자. 

- 다음 중 해당하는 사항이 있으면 대출에 기각된다.
    - 신용 등급이 좋지 않다.
    - 이미 대출이 있다.
    - 대출이 금지된 고객이다.
- 주택담보대출 신청이 받아들여진다면 최대 대출 금액은 고객의 수입에서 지출을 뺀 금액에 10을 곱한 금액이다.

함수 이름을 목록에 넣는다면 1개의 테스트가 만들어진다. 하지만 동작을 테스트로 만든다면 4개 이상의 테스트가 만들어진다. 모든 동작이 테스트되었는지 확인하기 위해 코드를 검토할 때, 사용할 수 있는 체크리스트가 있다. 

- 삭제해도 여전히 컴파일되거나 테스트가 통과되는 라인이 있는가
- if문의 참 거짓 논리를 반대로 해도 테스트가 통과하는가
- 논리 연산자나 산술 연산자를 다른 것으로 대체해도 테스트가 통과하는가
- 상숫값이나 하드 코딩된 값을 변경해도 테스트가 통과하는가

### 💭 테스트만을 위해 퍼블릭으로 만들지 말라

프라이빗 함수는 구현 세부 사항이다. 테스트를 위해 퍼블릭 함수로 만드는 것의 문제점은 다음과 같다. 

- 이 테스트는 실제로 우리가 신경 쓰는 행동을 테스트하는 것이 아니다. 우리가 신경써야 할 것은 구현 세부 사항이 아니라 퍼블릭 API이다.
- 테스트가 구현 세부 사항에 독립적이지 못하게 된다.
- 다른 개발자가 퍼블릭으로 바꾼 함수에 의존할 수 있다.

퍼블릭 API만을 사용해서 테스트하는 것이 좋다. 하지만 클래스가 더 복잡하거나 많은 논리를 포함하면 퍼블릭 API를 통해 모든 동작을 테스트하는 것이 까다로울 수 있다. 이 경우는 코드의 추상화 계층이 너무 크다는 것을 의미하기 때문에 코드를 더 작은 단위로 분할하는 것이 유익하다. 

### 💭 한 번에 하나의 동작만 테스트하라

여러 동작을 한꺼번에 테스트하면 테스트가 제대로 안 될 수 있다. 테스트 코드를 이해하기 어려운 단점도 존재한다. 이를 해결하는 방법은 각 동작을 자체 테스트 케이스에서 테스트하면 된다. 코드 중복이 많아진다는 단점도 존재하지만 이것은 매개변수화된 테스트로 방지할 수 있다. 

### 💭 공유 설정을 적절하게 사용하라

테스트 케이스에 의존성을 설정하거나 테스트 데이터를 만드는 것은 비용이 많이 들 수 있다. 이를 해결하는 방법은 다음 2가지가 있다. 

- **상태 공유**
    
    모든 테스트 케이스 전에 한 번 실행된다. 설정된 모든 상태는 모든 테스트 케이스 간에 공유된다. Ex) BeforeAll
    
- **설정 공유**
    
    테스트 케이스는 이 코드에 의해 모든 설정을 공유한다. 각 테스트 케이스 전에 실행되므로 테스트 케이스 간에 공유되는 상태는 없다. Ex) BeforeEach
    


비용을 줄이기 위해 상태와 설정을 공유하더라도 오히려 비용이 증가하는 경우가 발생한다. 적절하게 사용하는 것이 중요하다. 또한 상태와 설정을 공유하게 되면 초기화 등의 문제가 발생할 수 있으므로 조심해야 한다. 

### 💭 적절한 어서션 확인자를 사용하라

적절한 어서션은 테스트가 실패했을 경우에 이유를 잘 설명한다. 


**적절한 어서션 확인자**



### 💭 테스트 용이성을 위해 의존성 주입을 사용하라

데이터베이스와 같이 외부 의존성을 갖는 코드는 테스트하기 어렵다. 이는 의존성 주입을 통해 해결할 수 있다. 


### 💭 테스트에 대한 몇 가지 결론

- 통합 테스트: 여러 구성 요소와 하위 시스템을 연결하는 프로세스를 통합이라고 한다. 이런 통합이 잘 이루어져 작동하는지 확인하기 위한 테스트
- 종단 간 테스트: 소프트웨어의 처음부터 끝까지 통과하는 모든 여정을 테스트

- 회귀 테스트: 소프트웨어의 동작이나 기능이 바람직하지 않은 방식으로 변경되지 않았는지 확인하기 위해 정기적으로 수행하는 테스트
- 골든 테스트: 특성화 테스트라고도 하며, 주어진 입력 집합에 대해 코드가 생성한 출력을 스냅샷으로 저장한 것을 기반으로 한다. 테스트 수행 후 코드가 생성한 출력이 다르면 테스트는 실패한다.
- 퍼즈 테스트: 많은 무작위 값이나 '흥미로운' 값으로 코드를 호출하고 그들 중 어느 것도 코드의 동작을 멈추지 않는지 점검

### 💭 요약

- 각 함수를 테스트하는 것에 집중하다 보면 테스트가 충분히 되지 못하기 쉽다. 보통은 모든 중요한 행동을 파악하고 각각의 테스트 케이스를 작성하는 것이 더 효과적이다.
- 결과적으로 중요한 동작을 테스트해야 한다. 프라이빗 함수를 테스트하는 것은 거의 대부분 결과적으로 중요한 사항을 테스트하는 것이 아니다.
- 한 번에 한 가지씩만 테스트하면 테스트 실패의 이유를 더 잘 알 수 있고 테스트 코드를 이해하기가 더 쉽다.
- 테스트 설정 공유는 양날의 검이 될 수 있다. 코드반복이나 비용이 큰 설정을 피할 수 있지만 부적절하게 사용할 경우 효과적이지 못하거나 신뢰할 수 없는 결과를 초래할 수 있다.
- 의존성 주입을 사용하면 코드의 테스트 용이성이 상당히 향상될 수 있다.
- 단위테스트는 개발자들이 가장 자주 다루는 테스트 수준이지만 이것만이 유일한 테스트는 아니다. 높은 품질의 소프트웨어를 작성하고 유지하려면 여러가지 테스트 기술을 함께 사용해야 할 때가 많다.