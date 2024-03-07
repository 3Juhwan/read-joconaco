# 좋은 코드, 나쁜 코드 (5) 가독성 높은 코드를 작성하라

date: February 28, 2024
updatedAt: March 3, 2024 11:09 PM
tags: 📖 Review
status: Done
preview: 좋은 코드, 나쁜 코드 6장을 읽고 정리한 글입니다.

---

### 💭 서술형 명칭 사용

서술적이지 않은 이름은 코드를 읽기 어렵게 만든다. 그리고, 주석문으로 서술적인 이름을 대체할 수 없다. 


### 💭 주석문의 적절한 사용

주석문으로 달성할 수 있는 목적은 다음과 같다. 

- 코드가 **무엇**을 하는지 설명
- 코드가 **왜** 그 일을 하는지 설명
- 사용 지침 등 기타 정보 제공

하지만 대부분의 경우에 주석문은 지양하는 것이 좋다. 

- 중복된 주석문은 유해할 수 있다. 이미 코드로 잘 설명되는 작업을 굳이 주석문으로 작성할 필요 없다.
- 주석문으로 가독성 높은 코드를 대체할 수 없다.
- 주석문도 유지보수의 대상이다.
- 유지보수되지 않는 주석문은 없는 것보다 안 좋다.

다음 경우에는 주석문을 사용하는 것이 유용할 수 있다. 

- 코드가 **왜** 그 일을 수행하는지는 코드 자체로 파악하기 어렵다. 존재 이유나 목적, 배경은 주석문을 통해 작성하는 것이 유용하다.
- 유용한 상위 수준의 요약 정보를 제공할 수 있다.

### 💭 코드 줄 수를 고정하지 말라

일반적으로 코드 줄 수가 적으면 이해하기 쉬운 코드가 만들어 질 수 있다. 하지만 과도한 줄임은 역효과를 부른다. 

다음은 간결하지만 이해하기 어려운 코드이다. 


이런 경우에, 더 많은 줄이 필요하더라도 가독성 높은 코드를 작성하는 것이 좋다. 


잘 명명된 헬퍼 함수와 상수로 코드가 더 이해하기 쉽고, 하위 문제를 재사용할 수 있다는 장점이 생긴다. 

### 💭 일관된 코딩 스타일을 고수하라

자바에서 일반적으로 클래스 이름에 대해 파스칼 케이스(PascalCase)를, 변수 이름에는 캐멀 케이스(camelCase)를 사용한다. 뿐만 아니라 모든 코딩 스타일은 조직과 팀에 맞춰 따르면 된다. 

### 💭 깊이 중첩된 코드를 피하라

당연한 이야기다. 4중, 5중으로 중첩된 if문을 떠올려보면 답답하다. 중첩된 코드를 개선하는 방법은 다음과 같다. 

- 빠르게 return을 사용해서 중첩을 벗어난다.
- 중첩은 너무 많은 일을 한 결과물이다. 더 작은 함수로 분리해 보자.

### 💭 함수 호출도 가독성이 있어야 한다


위 코드는 1, true가 의미하는 바를 이해하기 어렵다. 


메서드의 매개변수를 잘 명명한다고 해도 호출부에서 매개변수의 이름을 알 방법이 없다. 


해결 방법 중 하나로 매개변수를 클래스나 열거형으로 분리할 수 있다. 하지만 때로는 해결책이 없을 수 있다. 

### 💭 설명되지 않은 값을 사용하지 말라

하드 코딩된 값에 대한 이야기로 예시는 다음과 같다. 

- 한 수량을 다른 수량으로 변환할 때 사용하는 계수
- 작업이 실패할 경우 재시도의 최대 횟수와 같이 조정 가능한 파라미터 값

하드 코드된 값에 의미를 부여하는 방법은 다음과 같다. 

1. 상수로 분리한다. Ex) `KILOGRAMS_PER_US_TON = 907.1847`
2. 상수를 반환하는 공급자 함수를 사용한다. 
3. 변환을 수행하는 헬퍼 함수를 사용한다. 
    
    

### 💭 익명 함수를 적절하게 사용하라

익명 함수는 간단한 로직에 좋다. 간단한 로직을 명명 함수로 분리하면 오히려 가독성이 떨어진다. 

복잡한 로직에 대해 익명 함수를 사용하면 가독성이 떨어질 수 있다. 

또한, 익명 함수가 길어지면 가독성이 떨어진다. 이때, 익명 함수를 여러 개의 명명 함수로 분리해 보자. 

### 💭 요약

- 코드의 가독성이 떨어져서 이해하기 어려울 때 다음과 같은 문제가 발생할 수 있다.
    - 다른 개발자가 코드를 이해하느라 시간을 허비함
    - 버그를 유발하는 오해
    - 잘 작동하던 코드가 다른 개발자가 수정한 후에 작동하지 않음
- 코드의 가독성을 높이다 보면 때로는 코드가 더 장황하게 되고 더 많은 줄을 작성해야 할 수도 있다. 이것은 종종 가치 있는 절충이다.
- 코드의 가독성을 높이려면 다른 개발자의 입장을 공감하고, 그들이 코드를 읽을 때 어떻게 혼란스러워할지를 상상해보는 것이 필요하다.
- 실제 시나리오는 다양하며 보통 그 상황에 해당하는 어려움이 있다. 가독성이 좋은 코드를 작성하려면 언제나 상식을 적용하고 판단력을 사용해야 한다.