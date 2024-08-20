# msa-study


인프라가 가변적으로 쉽게 변경되는 클라우드 환경

이때 수평확장을 위한 가장 효율적인 시스템 유형

cloud native application == miroservice

# 모노리스와 마이크로서비스

## 모노리스 시스템

어플리케이션이 한 덩어리로 구성

단일 프로세스로 실행

한꺼번에 수정, 배포가 되어야 함

하나가 실패하면 모두 실패 됨을 의미

모노리스를 클라우드 인프라에서 활용 시에 스케일 아웃의 대상은 모노리스 전체가 된다.

그것만으로 충분히 확장성, 탄력성이 보장이 가능하나 비용 효율적이지 않음

## 마이크로서비스

어플리케이션이 여러개 서비스 조각으로 구성

각기 독립적인 기능 제공

서비스가 사용하는 저장소는 다른 서비스와 완벽히 격리

따라서 독립적 수정 가능, 별도 배포, 확장 가능

하나의 서비스 실패는 전체 실패가 아닌 부분적인 실패

여러 개의 작은 서비스 집합으로 개발하는 접근 방법

각 서비스는 개별 프로세스에서 실행

HTTP 자원 API(RESTFUL API) 수단 사용 통신

서비스는 Biz 기능 단위로 구성(중앙 집중적 관리 최소화)

각 서비스는 서로 다른 언어, 데이터, 저장 기술 사용 가능

*  Polyglot : 각자의 서비스에 잘 맞는 언어, db, 프레임워크등 사용할 수 있는 것

### 마이크로서비스 성공 조건

클라우드 적용시 가장 이상적인 어플리케이션 유형은 마이크로서비스.

이는 기술 아키텍처 변화에 국한되지 않은 개발 프로세스, 조직, 개발 문화 등의 변화가 필요함.

* 조직 : 특정 도메인에 자율적인 권한과 책임을 지는 DevOps 조직

* 인프라 : 언제나 쉽게 확장 가능한 유연한 인프라 구성
  * 유연하고 민첩하게 제공되는 가변적인 인프라
  * public, private hybrid Cloud 설정
  * Infra as Code
  * Immutable Infra 배포된 후 변경되지 않는 인프라 패러다임

* 자동화 : 개발지원 도구 자동화, DevOps Infra(CI/CD)
   * 개발 지원용 자동화 도구 필요
   * 개발 지원 도구
   * 형상관리, 빌드/테스트/배포 자동화 CI/CD
   
* 개발 프로세스 : 피드백 기반의 개발 프로세스, 반복/점진적인 애자일 프로세스

* 개발 문화 : 공유/협업하고 학습하여 계속 진화하는 개발 문화(공유, 협업, 책임, 학습)

* 설계 방식 : 데이터 중복, 결과적 일관성 추구

테스트서버, 운영서버 배포했을 때 똑같이 돌아가도록 환경을 구성해야한다.

빌드 -> 패키징 -> 구성 -> 테스트 -> 배포

이 과정을 파이프라인으로 구성해서 개발, 운영 똑같이 만든다.

요즘 시대는 예전처럼 장기간 프로젝트를 통해 개발 X

2~3주의 Iteration 또는 스프린트(스크럼이라는 애자일에서 나온 용어)를 통한 개발 -> 피드백


**마이크로서비스 아키텍처 적용한다고 우리 회사가 넷플릭스고 아마존인가? 아니다. 개발문화, 프로세스 등 조직 전반에 걸쳐 바꿔야 한다.**

기존에는 개발과 운영이 따로 생각. 그러나 이제는 개발과 운영이 같이 가야한다. 벽이 없다.

기획자 + 디자이너 + 설계자 + 개발자 + 테스터 = 신속한 개발

속도, 책임감, 문제 발생시 쉬운 개선 => 완벽한 DevOps 조직

* 콘웨이 법칙 : 다 기능 팀 내부의 응집력 높이기

다기능 간의 의존성은 낮게

그럼 이런 다 기능을 가진 조직을 만들어야 하냐?

하면 좋다만 안된다면 그 간격(개발과 운영)을 줄이기 위한 노력을 해라.

#### 전체적인 상세 조건

피드백이 가시화, 작업간격 축소.

지속적인 피드백, 빠른 문제 감지 및 복구

(자동화 테스트, 피어 리뷰)

생산적인 신뢰 / 협업 문화 생성

(실험, 비난하지 않는 포스트 모텀(post-mortems, 지속적인 학습, 내부 기술 컨퍼런스)

결국은 신속 / 정확 / 협업 등이 잘 이루어진 조직을 먼저 만들어야 마이크로서비스가 잘 된다.

#### 장애처리

장애가 난다.

개인이 문제인가?

개인의 문제가 아닌 조직의 문제 관점으로 보자.

개인이 만든 개발 코드를 배포전까지 자동화 프로세스가 없던거 아닐까?

장애들의 대해서 문제를 서로 얘기하고 학습하고 공유하는 문화

#### Polyglot Persistence 접근 방법 사용

서비스 별 데이터베이스 설계 (각 저장소 분산 필수, 다른 서비스 저장소 호출 불가능, API만 통하여 접근 가능)

데이터 중복, 결과적 일관성 -> 이게 중요.

마이크로서비스로 설계하면 데이터 일관성 문제가 발생

언제든지 실패할 수 있음.

실패해서 더 이상 진행할 수 없을 때도 자연스럽게 대응할 수 있도록 설계.

자동으로 테스트할 수 있는 환경 설정

실패 감지 및 대응을 위한 실시간 모니터링 체계 필요

#### 서킷 브레이크 패턴

서비스 모니터링 서비스 다운 또는 실패 시 호출하는 서비스의 연계 차단, 적절한 대응을 위해 만듦.


#### 결론

성공적인 마이크로서비스를 만들기 위해서 3가지.

1) 유연하고 자동화된 개발환경

2) 점진, 반복적인 개발 프로세스

3) 자율적인 업무 기능 팀과 개발 문화


# 마이크로서비스 성숙도

No silver Bullet

만병통치약은 없다.

마이크로서비스는 MSA의 구성요소 중 하나임.

 
## 오해

* 컨테이너, 쿠버네티스 사용하면 MSA를 하는 것이라고 생각

* 클라우드 인프라 위에 무조건 마이크로서비스 올라가야 함

* 마이크로서비스로 구축하면 시스템 유연해지고 확장성 높아지고 비즈니스도 민첩해질 것이다.

* 대기업이 되기 위해서는 마이크로서비스가 필수다.

위에 모두 오해이다. 아키텍처는 정답이 없다.

아키텍처는 각기 다른 상황에 따른 최선의 선택이고 trade-off 해야한다.

## MSA 아키텍처 발전과정

<img width="1069" alt="image" src="https://github.com/user-attachments/assets/8230e7c9-0318-4d69-a6ac-f632abd1c08c">

좌측에서 우측으로 갈 수록 점진적인 진화형태

많은 시간과 비용이 듦. 대신 리스크가 커짐

당연히 오른쪽으로 갈수록 확장성, 배포성, 탄력성 확보

성능은 오른쪽으로 갈수록 떨어짐. 왜냐하면 결국 인스턴스가 따로 만들어지기 때문에 네트워크 문제가 발생(반응 시간 : latency)

마이크로서비스의 경우 고도의 디커플링을 요구

재사용은 커플링을 유발하기 때문에 재사용보다 중복을 우선시 함. (각 인스턴스가 같은 데이터를 가지고 있는 것)

잦은 네트워크 호출이 필요하므로 성능은 다소 부정적이며 보안처리, 분산 트랜잭션 등 난이도와 복잡도가 높아짐.

저장소의 완벽한 격리 필요하며, 통합 데이터 모델링 사상과 상충되며 데이터 중복, 복제가 고려되어야 함.

따라서 데이터 일관성 처리를 위한 결과적 일관성 매커니즘 필요(복잡도 증가)

## 아키텍처 개념 과 레이어드 아키텍처

아키텍처를 큰 구조, 청사진, 패턴 이렇게 부르는 거임.

아키텍처를 결정하는 여러가지 조건을 따져보고 맞게 선택

특성 : 가용성, 신뢰성, 시험성, 확장성, 보안, 민첩성, 탄력성, 성능, 배포성, 학습성

결정 : 시스템의 제약조건, 개발자가 해도 되는것, 안되는것 정의

설계원칙 : 아키텍처 결정을 만족시키는 가이드 라인

시스템 구조 : 아키텍처 결정 및 설계 원칙에 적합한 상위 수준의 시스템 구조를 정의


비즈니스 요건을 분석 -> 그에 맞는 아키텍처 특성 도출

정의된 아키텍처에 기반한 컴포넌트 모듈화, 식별하고 적절한 역할 및 책임을 부여함.

도메인 기능이 응집되도록 컴포넌트를 도출하고 컴포넌트 간 의존관계를 줄이도록 함.

## 아키텍처 종류

레이어드

파이프라인

마이크로커널

서비스 기반 (이게 soa)

이벤트 기반

공간 기반

오케스트레이션 기반

마이크로서비스

* 책추천 : Fundamentals of Software Architecture 마크 리처드, 닐포드, 한빛 미디어


## 레이어드 아키텍처

엔터프라이즈에서는 사실상 표준 아키텍처

### 특징

관심사의 분리

기술 분할

아키텍처 결정사항 : 레이어 개방/폐쇄 여부

이키텍처 싱크홀 안티 패턴 (바로 아래 레이어가 아닌 두,세 단계 아래 레이어 바로 접근할수 있게 정의 할수 있음, 성능이나 여러 이유로 인해서)

단순, 소규모, 비용작음

의존성의 역전(요청 역전)으로 구성할수도 있음

대표적 구현된 아키텍처 : OSI 7계층

 
### MVC 패턴의 오해

MVC는 프레젼테이션 레이어를 구현한 하나의 패턴일뿐

이게 전체 어플리케이션을 구성하는 아키텍처는 아니다.

프레젠테이션 레이어가 controller이고 결과가 나온 값을 주는게 model이고 이걸 보여주는 view


## 파이프라인 아키텍처

파이프와 필터

Bash, Zsh 등 유닉스 터미널 쉘 언어의 기초 원리

### 필터의 종류

1)프로듀서, 프로세스 시적점, 소스

2)변환기, 입력을 받아 일부 또는 전체를 변환한 후 전달, map

3)테스터: 기준에 따라 테스트, 결과 생선, reduce

4)컨슈머: 흐름 종착역, 데이터베이스 저장, 화면출력

단방향 단순, 조합 가능

EDI(전자데이터 교환), ETL(추출, 변환, 적재)

필터 -> 필터 -> 필터 -> 필터

이때 필터 사이에 파이프를 두는 것

배치에서 자주 사용


## 마이크로 커널 아키텍처

플러그인 아키텍처라고 보면 됌

이클립스 IDE, 지라, 젠킨스, 크롬 같이

내가 원하는 마켓에서 플러그인 설치해서 내가 원하는 코어 시스템 추가 확장 변경 하는 것.

단순하고 비용이 적음.

자동차 옵션이라고 보면됌
 
## 서비스 기반 아키텍처

MSA는 서비스 기반 아키텍처 중에 하나이다.

유연성 있는 대규모 분산 레이어 구조

도메인 서비스 보통 4 ~12개, 평균 7개

REST, RPC, SOAP

중앙 공유 데이터베이스 사용(조인 기능 사용)

신뢰성, 내고장성

그럼 MSA랑 다른건?

구조가 크다.

데이터베이스가 하나이다.

### 여러 형태의 변형

1. 유저 인터페이스 변경

   1) 하나의 유저인터페이스
   
   2) 2개 이상의 유저인터페이스, 3개 이상의 서비스
   
   3) 각 서비스별 유저인터페이스

서비스, 유저인터페이스를 쪼갤수록 변경하기 쉬움

마이크로 프론트앤드(ex: 아마존).

대신 성능은 조금 떨어질수 있음

<img width="749" alt="image" src="https://github.com/user-attachments/assets/6fe2da35-1db5-4f63-b401-d0da4116d05d">


2. 데이터 베이스 변경

개별 데이터베이스로 분리(마이크로서비스랑 유사)

각 데이터베이스에 있는 도메인 데이터를 다른 도메인의 서비스가 필요하지 않도록 설계하는 것이 중요.

통합db, 도메인별db, 조회용db, 서비스별db 격리

읽기용 서비스 db, 쓰기용 서비스 db (이게 CQRS)

이때 쓰기용 db랑 조회용 db랑 일관성을 맞춰야함.

어떻게 맞출꺼냐?

CUD가 일어날때마다 읽기 db에 넘겨주기 (이때 살짝 딜레이를 줌, entual consistency)

<img width="969" alt="image" src="https://github.com/user-attachments/assets/014df2f2-9c4b-4c52-8e6f-f3b29434fe1a">


3. 서비스 내부 설계

서비스 안에는 레이어드 설계 vs 도메인 설계(도메인 분할)

세분도가 크기 때문에 API 퍼사드 통한 내부 클래스 수준의 오케스트레이션 필요

<img width="1033" alt="image" src="https://github.com/user-attachments/assets/4f9be9cb-ecce-43b0-b69f-098d33feea70">

4. 서비스 내부 설계

서비스 안에는 레이어드 설계 vs 도메인 설계(도메인 분할)

세분도가 크기 때문에 API 퍼사드 통한 내부 클래스 수준의 오케스트레이션 필요

<img width="1019" alt="image" src="https://github.com/user-attachments/assets/534db24e-2159-420d-a246-24579e748a94">


* 정리 

일반적으로 모놀리식 데이터베이스 공유

데이터베이스 커플링 문제, 스키마 변경 시 변경 영향도 문제 발생

이를 낮추기 위해 논리적으로 분할, 전용 공유 라이브러리화, 도메인별 접근권한 분리

<img width="1012" alt="image" src="https://github.com/user-attachments/assets/905eca62-d635-4d3b-899e-729d7ed4ffcd">


## 이벤트기반 아키텍처

확장성이 뛰어난 고성능 어플리케이션 개발에 쓰이는

비동기 분산 아키텍처.

다른 아키텍처에 내장 가능(ex: 이벤트 기반 마이크로서비스 아키텍처)

브로커 토폴로지

이벤트(사건)에 액션이 반응하는 방식 진행

RabbitMQ, ActiveMQ등 경량 메시지 브로커

### 스타일은 두가지가 있음
 
1) 코레오그래피(choreography): 각자 자율적 이벤트 처리

장점 : 확장성, 응답성, 성능(이건 좀 상대적)

단점 : 트랜잭션 통제 힘듬, 교착상태, 데이터비일관성, 에러처리 어려움

<img width="680" alt="image" src="https://github.com/user-attachments/assets/3c0021eb-b2a0-4e8f-a78d-02605e2cf4d3">

2) 오케스트레이션

이벤트는 사건이 아니라 커멘드(일어나야할일)

장점 : 에러처리

단점 : 확장성, 중재자가 병목지점, 커플링으로 성능저하

<img width="859" alt="image" src="https://github.com/user-attachments/assets/db2733d0-bee8-4f47-a89d-12e5e9db2967">

## 공간 기반 아키텍처 스타일

높은 확장성, 탄력성, 동시성

동시 유저수가 매우 가변적이라 예측조차 곤란한 애플리케이션에 유용

복제된 인 메모리 그리드

데이터펌프, 데이터라이터, 데이터리더

<img width="973" alt="image" src="https://github.com/user-attachments/assets/b5a911ae-b3c0-42f3-87b9-373d74d0136d">


## 오케스트레이션 기반 서비스 지향 아키텍처 스타일

제약이 많은 분산 아키텍처

벤더 중심, 기술분할에 집착

비즈니스 행위 재사용 강조

오케스트레이션 엔진

재사용으로 인한 서비스 간 의존성 높아짐

사실상 실패 아키텍처

<img width="763" alt="image" src="https://github.com/user-attachments/assets/a1413059-136f-491e-b55f-fb5c45b823f1">


## 마이크로 서비스 기반 아키텍처 스타일

분산 아키텍처, 성능은 그닥, 세분도가 중요.

데이터 격리, 재사용보다 중복, 프로토콜 인지 이종간 상호 운용성

API 레이어(API gateway), 고도의 디커플링 추구

API 레이어는 가볍게, 비즈니스 로직이 X

<img width="854" alt="image" src="https://github.com/user-attachments/assets/b26f5f39-23fd-4419-b682-f34dde86fa92">

### 정리

아키텍처를 결정하기 전에 비즈니스의 요구사항을 잘 알아야함.

ex) 데이터의 즉시 일관성이 필요? 그럼 이벤트 기반 아키텍처는 힘듬.

도메인, 데이터 아키텍처, 조직역량, 개발 프로세스등

애자일 프로세스 역량이 없는데 최신기술? ㄴㄴ

소프트웨어 아키텍처의 모든 것은 트레이드 오프

어떻게 보다 '왜'가 더 중요하다.


# 마이크로서비스 아키텍처 구성요소

## MSA 패턴 유형

MSA는 여러 개의 서비스간의 연계를 통해 시스템을 구축하는 SOA의 범주에 있다.

SOA(service-oriented architecture)는 서비스 인터페이스를 통해 소프트웨어 구성 요소의 재사용과 상호 운용성을 가능하게 하는 방법을 정의합니다. 

서비스는 공통 인터페이스 표준과 아키텍처 패턴을 사용하므로 새로운 애플리케이션에 신속하게 통합될 수 있습니다. 

이로써 애플리케이션 개발자는 기존의 기능을 재개발 또는 복제하거나 기존의 기능을 연결하거나 상호 운용성을 제공하는 방법을 알아야 했던 수고를 덜 수 있습니다.

* innner architecture : 개발자가 흔히 개발하는 인스턴스 안에 들어가는 비즈니스 아키텍처

* outer architecture : 서비스(인스턴스)가 효과적인 운영 관리 지원을 위한 것

<img width="683" alt="image" src="https://github.com/user-attachments/assets/47ea2087-0689-4ec5-9a42-9fceb56bff13">

## MSA 패턴

<img width="1076" alt="image" src="https://github.com/user-attachments/assets/65887ef2-7994-4bb7-a35d-773bc857f40d">

***MSA를 돕든 제품들이 왜 필요한가? 이렇게 접근해야함.***

그 전에도 말했듯이 최신? 잘 쓰니까? 이게 아니라 왜 쓰는가?

MSA의 패턴을 이해하는 것이 중요


## MSA 구성요소

<img width="1030" alt="image" src="https://github.com/user-attachments/assets/5976018e-2207-46fa-8da7-1cf10062e0e7">

## 구조화

<img width="1081" alt="image" src="https://github.com/user-attachments/assets/8b7edd9b-a1a4-4055-b0a0-8c6af2a4f724">


### 인프라와 플랫폼에 관련된 패턴 이해

코드 개발

코드 저장(repo) : git

// 여기까지 CI

build automation (image store에 저장(도커)

deploy automation(도커의 이미지를 환경설정(config store)에 따라서 배포)

container management platform(ex : 쿠버네티스, vm, 오케스트레이션 컨테이너)이 배포된 이미지를 backing service에 맞게 운영

// 여기까지 CD

라우터 : 웹, 모바일 등 클라이언트가 서비스를 찾아 가기 위해 찾아주는 것

서비스 디스커버리 : 컨테이너 IP와 서비스 이름 찾는것. DNS같은

로드 밸런싱 : 어떤 컨테이너로 보낼것인가

인증/인가

모니터링 : 로그

diagnostics : 추적, tracing, 서킷브레이크

# 인프라









