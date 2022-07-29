---
title: "개념정리: 의미 구조(Semantics)의 표현 방식들"
last_modified_at: 2022-06-04
categories:
    - Study
tags:
    - Programing Languages
    - TaPL
classes: wide
---

## 헷갈리지 않도록

PL과 관련된 분야를 공부하고 연구하기 시작한지도 햇수로 4년이 되어가는데, 아직도 간혹가다 헷갈리는 기본 개념들이 있다.
그럴 때마다 한없는 자괴감에 빠지곤 했는데, 차라리 조금의 창피함을 감수하더라도 블로그에 정리해두는 게 앞으로의 공부에 도움되리라 생각해 생각나는 대로 정리하기로 했다.

기록하고 싶은 개념이 생길 때마다 한 포스트에 업데이트를 할까 생각도 했지만, 이왕 정리하는 김에 주제별로 포스트를 나눠 조금은 상세하고 친절한 설명을 넣는 것이 좋을 거라는 판단에 꾸준히 여러 포스트를 올리기로 했다.

## Semantics

프로그래밍 언어에서 의미 구조(semantics)란 거의 모든 PL 연구의 처음과 끝을 관통하는 개념이라 봐도 무방하지 않을까 싶을 정도로 중요한 존재이기 때문에, 사실 크게 헷갈릴 수 없는 개념이다.
다만 이후 정리해 둘 개념들을 위해 아주 간단하게만 설명하도록 하겠다.

프로그래밍 언어의 문법 요소들(보통 term이라 하며, expression 또는 statement를 생각하면 된다)이 연산 과정(evaluation)을 거쳐 어떤 값(value) 또는 상태(state; 여기서 말하는 상태는 variable -> value와 같은 relation을 생각하면 된다)를 가질지에 대한 규칙을 우리는 의미라 한다.
이 때 의미는 엄밀하게 말해 집합으로 정의되며, 현재 주어진 상태(state 혹은 environment)에서 (문법적으로 올바른) 어떤 식(expression) 또는 구문(statement)의 실행 이후 상태는 존재하여 하나로 결정될 수도, 존재하지 않을 수도 있고, 만약 존재한다면 이는 곧 현재 상태, 식(또는 구문), 이후 상태(또는 값)의 순서쌍이 의미 집합에 존재한다는 식으로 정의된다.

이렇게 집합으로 정의된다는 것은, 곧 귀납정의(inductive definition)의 한 표현방식인 추론규칙(inference rule)으로 의미를 정의하고 서술할 수 있다는 의미이기도 하다.

## Operational Semantics vs Denotational Semantics (vs Axiomatic Semantics)

이제 정말 헷갈리기 시작하는, 그러나 헷갈려서는 안 되는 개념들이 등장하기 시작하는데, 동작 의미 구조(operational semantics)와 표시적 의미 구조(denotational semantics), 공리적 의미 구조(axiomatic semantics)이다.
(*주의: 각 용어들의 번역 용례는 [ROPAS 홈페이지의 번역 용례](http://ropas.snu.ac.kr/lib/term/)를 참고하긴 하지만, 번역이 너무 장황하거나 해당 페이지에 존재하지 않는 용어의 경우 임의로 번역하였다)
각각에 대해 간단하게 정리해 두겠다.

1. **동작 의미 구조(Operational Semantics):** 프로그램의 수행 과정, 즉 상태의 변화를 표현하게끔 정의하는 방식의 의미 구조. 현재 상태에서 특정 식 또는 구문을 실행한 뒤 상태가 어떻게 변화할지 정의한다. 가장 단순하고 직관적이므로 프로그래밍 언어의 실행기(interpreter)를 구현할 때 주로 사용된다.
1. **표시적 의미 구조(Denotational Semantics):** 프로그램이 수학적으로 어떻게 표현되어 각각의 식과 구문이 어떤 값을 가지게 되는지 엄밀히 정의하는 방식의 의미 구조. 프로그램 분석 분야에서 요약 실행(abstract interpretation) 과정을 수학적으로 정의할 때 필요하다.
1. **공리적 의미 구조(Axiomatic Semantics):** 프로그램 자체의 구체적인 수행 과정이나 의미를 정의하기보단, 그 프로그램이 실행됨으로써 입증될 수 있는 논리 명제를 얻어내게끔 정의되는 의미 구조. 이러한 특징 덕에 프로그램 논증 분야에서 굉장히 중요하게 다뤄지지만, 사실 프로그램을 실행하는 관점에서 쓸모가 있지는 않다. 완전히 같은 개념은 아니지만, Hoare logic을 떠올리면 되겠다.

## Big Step vs Small Step Semantics

동작 의미 구조는 프로그램의 수행 과정을 그대로 정의하는 형태이기 때문에, 매우 간편하며 직관적이다.
다만 더 구체적으로 들어가면, 정의 방식이 두 가지로 나뉘게 된다.
큰 걸음 의미 구조(big step semantics)와 작은 걸음 의미 구조(small step semantics)가 바로 그것이다.
이 역시 정리해 보자.

1. **큰 걸음 의미 구조(Big Step Semantics):** 동작 의미 구조에서의 계산 규칙을 한 번에 끝내는 식으로 정의하는 방식. 현재 상태에서 주어진 식 또는 구문의 실행 결과, 더이상 수행할 것이 없는 최종 상태 도는 값이 된다는 것을 한 번에 표현한다. 예를 들어, `if t1 then t2 else t3`는 계산 결과 `t1`이 `true` 값을 가지면 `t2`가 가지게 되는 값, `t1`이 `false`값을 가지면 `t3`가 가지게 되는 값을 가질 것이라고 단번에 정의한다.
1. **작은 걸음 의미 구조(Small Step Semantics):** 가능한 한 최소한의 계산 과정 하나하나를 계산 규칙으로 정의하는 방식. 큰 걸음으로는 반드시 그 식 또는 구문의 계산 결과에 해당하는 상태 또는 값이 의미구조에 포함되어야 했지만, 작은 걸음에서는 계산 과정에서 새로 도출되는 식 또는 구문이 그 자리를 대체할 수 있다. 예를 들어, `if t1 then t2 else t3`는 `t1`이 가지게 될 값 `v`에 대해(물론 `v`는 boolean 값일 것이다) `if v then t2 else t3`가 된다고 정의하며, 또 추가로 `if true then t1 else t2`가 `t1`의 값을 가지며 `if false then t1 else t2`가 `t2`의 값을 가진다는 것을 각각 따로 정의한다.