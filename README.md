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

## 인프라 패턴

build automation : CI(지속적 통합), 도커, 젠킨스, 깃헙

deploy auto : CD(지속적 배포), AWS ECR, 도커허브, HARBOR

위에 제품들은 각 패턴유형의 대표 제품들

### 인프라에 관련된 패턴 이해

보통 클라우드 or DevOps 인프라 패턴

• 인프라플랫폼(IaaS) : AWS EC, Azure VMs , OpenStack
• 컨테이너플랫폼(CaaS): AWS ECS,EKS,AKS,GKE , k8s, DC/OS, Docker Datacenter
• 어플리케이션플랫폼(PaaS,aPaaS): Heroku,PCF,CloudFondy,OpenShift
• 함수플랫폼(FaaS) : Lambda,Azure Functions,GCF, OpenWhik
• 소프트웨어플랫폼(SaaS): Saleforce,Oracle,SAP,OpenFaaS,fission,Knative

<img width="1091" alt="image" src="https://github.com/user-attachments/assets/63da561f-c202-4181-9ba6-59399a6c5a1c">

구글 docs처럼 구글의 대표적인 제품들이 SaaS의 예시


## VM vs 컨테이너

### vm (가상 머신)

게스트 OS 관리 오버헤드, virtualbox, vmware

가상머신의 하이퍼바이저 위에 각 vm이 있고 vm은 각 게스트 os를 가지고 있는데 이때 게스트 os가 커널.

커널의 단점은 많은 라이브러리를 가지고 있어서 무겁다.

그래서 배포, 부팅 속도가 느림.

### 컨테이너

컨테이너 런타임 : OpenVZ, Docker가 사실상 표준

개발과 배포가 편해짐, 독립된 개발 환경 보장

개발/운영 환경의 통합 : 개발 환경 그대로 다른 서버에 똑같이 복제 가능

커널을 포함하지 않으므로 이미지가 크지 않고, 배포속도가 빠름

애플리케이션의 독립성과 확장성이 높아짐 : 마이크로 서비스

Stateless, 불변성

컨테이너는 하이퍼바이저가 아닌 컨테이너 런타임이 있는데 vm의 게스트 os(커널)를 공통으로 가지고(공유) 있기 때문에 빠르다.

애플리케이션 구동을 위한 라이브러리 & 실행파일을 가지고 있음.

<img width="1153" alt="image" src="https://github.com/user-attachments/assets/b4a6575a-3184-4464-8d66-adaf669752e5">

## 도커

도커엔진

도커이미지 : 컨테이너 생성시 필요한 요소, 여러개의 계층으로 된 바이너리 파일, 읽기 전용

이미지 저장소

도커컨테이너 : 도커이미지로 생성, 격리된 시스템 자원 및 네트워크를 사용할 수 있는 독립된 공간 생성

기본명령어

• Docker run –I –t ubuntu:14.04
 
실행 동작

이미지를 도커허브에 넣어놓고 우분투가 도커허브에 이미지를 가져와서 도커(컨테이너)에 실행

#### 수동작업

<img width="1060" alt="image" src="https://github.com/user-attachments/assets/b169034d-ba6c-428c-9c47-11146d6d4595">

#### 자동

Dockerfile로 이미지 생성 자동화

• 빌드 명령어 제공, 컨테이너에 설치해야 할 패키지,추가해야 할 소스코드 ,실행해야 할 명령어,쉘 스크립트등을 하나의 파일에
기록 , 도커엔진이 읽어들어 이미지 생성
• 쉽게 배포 가능

<img width="890" alt="image" src="https://github.com/user-attachments/assets/265b30e8-7083-4474-9c0c-ef4a05168b73">

### 컨테이너 라이브 사이클

도커파일로 빌드하면 이미지가 생기고 이거를 도커허브에 저장.

나중에 컨테이너를 생성하면 도커허브에 이미지를 가져와 commit 실행.

<img width="1096" alt="image" src="https://github.com/user-attachments/assets/c33aab9b-5eed-44eb-a4d7-01438c8ce52c">

### 도커 컨테이너

빌드 컨텍스트 : 이미지를 생성하는데 필요한 각종 파일, 소스코드, 메타 데이터를 담고 있는 디렉토리

기반이미지 위에 레이어, 그 위에 레이어, 그 위에 레이어 계속 쌓아감.

절차적이 아닌 선언적 방식으로 되어 있다.

어떻게 할것이 아닌 무엇을 할것인가?

### 컨테이너 오케스트레이션

하나의 호스트 머신에서 도커엔진으로 구동하다가 cpu, 메모리, 디스크용량과 같은 자원이 부족하면 어떻게 할것인가?

-> 서버 클러스팅으로 자원을 병렬로 확장

새로운 서버, 컨테이너가 추가 됐을 때 discovery 하는 일

스케쥴링 : 어떤 서버에 컨테이너를 할당할 것인가

부하분산(로드밸런서)

장애복구 : 서버가 다운되었을 때, 고 가용성 보장

#### 해결

위에 것들을 해결하기 위해 나온 제품이 바로 k8s(쿠버네티스), MESOS, Docker Swarm

컨테이너 배포, 스케일링, 로드밸런싱, 네트워킹 자동화

애플리케이션 레벨의 서비스를 제공하지는 않음

(미들웨어, 데이터처리, 데이터 스토리지)

로깅, 모니터링, 경보는 포함 되지 않음

보통 매니저 노드가 있고 그 아래 여러 워커 노드를 포함하도록 구성되어 있음.

서비스 : 같은 이미지에서 생성된 컨테이너 집합, 생성된 컨테이너를 레플리카라 함.

매니저노드가 워커노드 2개를 가지고 있엇다.

그때 하나가 죽음 다른 워커노드 안에 2개의 컨테이너를 만듬.

이때 2개의 집합을 레플리카

replica = 2

컨테이너들을 관리, 즉 자동 스케쥴링, 자동 확장, 자동 배포등을 하는 것의 대표주자가 쿠버네티스

## 쿠버네티스

• Kubernetes àk8s
• Automatic bin packing
• Self-Healing
• Horizontal scaling
• Service discovery and Load balancing
• Automated rollouts and rollbacks
• Secret and Configuration management
• Storage orchestration
• 모든리소스는오브젝트형태로관리
• 명령어보다는YAML
• Pod, Replicaset, Service,
• Deployment, Configmap,secret,
• Ingress

<img width="818" alt="image" src="https://github.com/user-attachments/assets/fe04f7d7-f4a2-482d-9e63-875c5b5fc7f5">

service discovery : 한가한 워커노드의 컨테이너를 찾은 기능

무중단 배포 관리

<img width="1103" alt="image" src="https://github.com/user-attachments/assets/8900cc96-ffdc-4bf4-af82-963585fe4130">

애플리케이션이 올라가는 컨테이너를 만드는게 도커

이 도커를 관리 해주는 쿠버네티스

### Pod

Pod : 컨테이너를 다루는 기본단위

컨테이너 = pod

1개 이상의 컨테이너로 구성

하나의 완전한 애플리케이션으로 동작

Pod 안에 Ngix컨테이너(우리가 흔히 개발하는 것), 사이드카(인증/인가, 로깅 같은거) 이렇게 있음

그냥 pod는 하나의 컨테이너다라고 인식하고 가도 됌


### 레플리카셋(replicaset)

<img width="1305" alt="image" src="https://github.com/user-attachments/assets/8bf59043-5361-4064-9f98-155a633dcc7c">


정해진 수의 동일한 포드가 항상 실행되도록 관리

노드 장애 등의 이유로 포드가 사용할 수 없다면 다른 노드에서 포드 다시 생성

replica= 3로 선언했으니 pod를 3개 만듬

이런거를 보통 yaml으로 선언적 작성.

pod, replica 각각 선언할수있는데 이거를 한꺼번에 선언하는 것이 deployment

service(clusterIP) : 알아서 라우팅, 로드밸런싱 해줌.

ingress : 서비스를 OSI 계층에서 로드밸런싱 해주는것. url기반으로

### deployment

<img width="1248" alt="image" src="https://github.com/user-attachments/assets/733417b9-548b-4b35-a824-d97a9b9b6b73">


Pod set, ReplicaSet을 한번에 = deployment

업데이트 배포를 더욱 편하게 함.

애플리케이션 변경시 레플리카셋의 변경사항을 저장하는 리비전을 남겨 롤백 가능

무중단 서비스를 위해 롤링 업데이트 전략 지정 가능

### Service

포드를 연결하고 외부에 노출

여러 개의 포드에 쉽게 접근할 수 있도록 고유한 도메인 이를 부여,

여러 개의 포드에 접근 할때 요청을 분산하는 로드밸런서 수행

clusterIP(보통 이거 씀), NodePort(어플리케이션 포트랑 머신포트랑 연결하는것, 물리적 포트, 노드의 port를 열어 외부에서 접속하도록), LoadBalancer

4개의 레플리카를 설정하고 실행. (nodeport를 30080으로 설정)

이때 스케일 아웃후 로드밸런싱 잘되는 지

확인(kubectl get deployment)하면

랜덤으로 Pod에 붙는 것을(curl host01:30080)

확인할 수 있다.

후에 하나의 pod를 죽이면

(kubectl delete pod podName(pod이름))

알아서 신규Pod를 만든다.

yaml로 레플리카set를 설정할수있고

혹은 명령어로 가능

kubectl scale --replicas=5 deployment/webapp1

명령어가 쿠버네티스 마스터안에 있는 etcd라는 곳에 저장됌

그러시면 마스터안에 컨트롤러메니저가 etcd를 주시하고 있다가 자동으로 스케일링해줌.

### ingress

url 기반으로 로드밸런싱

ssl 보안 연결

인그레스 규칙

인그레스 컨트롤러 서버, Nginx 웹서버 인그레스 컨트롤러

### Configmap(설정값)

컨테이너는 수정할 필요가 없다(상태를 가질 필요가 없다). 즉, 불변성. 이미지로 관리하니까 개발이나 운영이나 같은 환경으로 사용.

이때 이미지는 개발이나 운영이나 똑같이 배포하는 것은 좋은데 db는 다르게 해야 하잖아.

이런 가변적인요소(db 저장소)들을 컨테이너 관리와 다르게 컨테이너에서 필요한 환경 설정을 관리하는 것을 config pattern이라고 한다.

이것을 쿠버네티스에서는 컨피그맵, 시크릿 같은 것이다.

컨피그맵은 db, 이미지 같은거

시크릿(암호화 기능)은 보안쪽에 치중되어 있음.

그래서 key, value 형식으로 저장되어 있음

# DevOps 인프라(CI/CD)

인프라 패턴의 클라우드 패턴

이때 VM하고 컨테이너 차이점

컨테이너 대표적인게 도커

컨테이너가 여러 노드에 올라가기 위한 자동화 배포를 위한 관리를 오케스트레이션이 필요

이거의 대표적인게 쿠버네티스

이 클라우드 인프라 패턴을 배포하는 패턴을 CI / CD

빌드 : 컴파일, 테스트, 정적 분석 수행

배포 : 개발된 어플리케이션을 개발/테스트/스테이징/운영에 배포

수동배포 : 오류발생 높음, 시간 오래 걸림, 환경에 따른 영향이 미침

CI/CD 애자일 프렉티스에서 유래.

자동으로 통합하고 테스트하고 레포트로 남기는 활동 = CI

실행환경에 자동으로 배포하는 것 = CD
 
인텔리제이 -> 깃헙 -> 젠킨스 -> 도커 // 여기까지 형상관리 CI -> AWS ECR -> Amazon EKS // CD

이런거를 파이프라인 설계

컴파일, 테스틍, 정적분석, 패키징, 컨테이너 이미지 생성, 배포환경 구성, 배포 이거를 각 단게별 구성

마이크로서비스를 위한 파이프 라인은 독립적 배포를 지원해야 함.

대표적인게 젠킨스 : 가시적 통보, 다양한 플러그인

<img width="1211" alt="image" src="https://github.com/user-attachments/assets/250c93aa-efe7-4ac7-97d0-df07d3f5d192">

## 배포전략

배포의 전략 3가지

서비즈 중단 없이 새로운 버전 배포하기

1) 롤링 업데이트

컨테이너 이미지를 새버전으로 하나씩 교체

2) canary 카나리

새로운 배포 버전과 현행버전을 운영 환경에서 동시에 검증

롤링과 블루그린 중간 사이

신규버전 구버전 트래픽 비중을 줄수 있다.

3) blue / green

완전하게 준비된 상황에서 서비스 교체

높은 오버헤드와 서비스 장애 최소화 간 조율

<img width="1363" alt="image" src="https://github.com/user-attachments/assets/26418901-9feb-42c4-be8a-6edf3709b025">


# CSP

 Cloud Service Provider의 약자로, 클라우드 서비스를 제공하는 업체

위에 개념만 알면 어느 제공자를 선택하든 다 기능을 가져다 쓰면 된다.

클라우드 서비스 프로바이져( CSP) : aws, azure, GCP

클라우드 서비스 제공업체

가상 네트워크, 스토리지, 컨테이너, 서버 서비스

다양한 backing 서비스들

devops 서비스 (빌드/배포),

모니터링, 추적, 로깅

### 다양한 기

<img width="968" alt="image" src="https://github.com/user-attachments/assets/ca3e5186-27c8-453d-ad3b-23dcce7652eb">

Virutal Servers : Instances

PaaS(platform as a service) : 어플리케이션 그냥 던지면 알아서 구동. AWS에서는 Elastic Beanstalk라는 도구 제공

Serverless Computing : Lamda

도커기반 PaaS : AWS의 ECS

쿠버네티스 관리 : AWS의 EKS

object storage : AWS의 S3

Archive Storage(S3 장기간 보관) : Glacier

File storage : EFS

Global Content Delievery(CDN : 정적 이미지 ) : CloudFront

Managed Data WareHouse : RedShift

# MSA생태계의 발전과 패턴의 탄생

관리, 운영 플랫폼 패턴의 이해

모노리스 -> 모듈형 모노리스 -> 마이크로서비스 -> 분산 트랜잭션(각각의 데이터 저장소 가짐)

연쇄적인 장애가 생김

마이크로서비스 운용시 생겨난 문제를 해결하기 위해 넷플릭스가 OSS를 만듬

그게 리본, 휴스티릭스, 유레카 등. 테크 블로그에 오픈함.

1999년 지속적인 통합 방법론

2001년 애자일 선언

2006 AWS EC2

2009년 데브옵스

2010년 스프링 부트

2013년에 도커 컨테이너

2014년 마이크로서비스 정의 (fowler, lewis)

2014년 쿠버네티스

## Spring Cloud , BFF, API GW

넷플릭스에 대항한 스프링진영에서 만든건 spring cloud 아키텍처

여기서 BFF, API GW, Router, 로드밸런싱, 인증/인가, 중앙화된 로깅, metric, 추적등을 소스로 관리하는게 spring cloud

<img width="1370" alt="image" src="https://github.com/user-attachments/assets/735b6e69-f312-404d-81b8-6305b0a1d662">

### BFF(BackEnd for FrontEnd)

넷플릭스 채널(모바일, 컴퓨터, tv등)

채널에 따른 다양한 API 조합

API 게이트웨이를 하나로 두지 않고 프런트앤드 유형에 따라 다른 API 조합을 위해 두는 패턴

다양한 채널이 있다면 고려해볼만하다.

### API Gateway

다양한 클라이언트가 개별 서비스에 엑세스하기 위해서는 단일 진입점을 만들어 놓으면 여러모로 효율적

여기에 비즈니스 로직을 넣으면 안된다.

그러나 라우팅, 로드밸런싱, 인증/인가, 추적, 장애격리, 서비스 탐색등은 들어간다.

예를 들어 상품서비스가 리뷰서비스를 호출할때 direct가 아닌 api 게이트웨이를 통해서 호출하기 때문에 추적, 장애 등의 기능이 들어간다.

일정 시간 동안 서비스 요청에 대한 반응이 없으면 기존 요청 경로를 차단하고 다른 경로로 요청 경로를 변경하는 기능을 가진다. ==>>> 서킷 브레이커

### 라우팅, 로드밸런싱, 서비스 탐색

API 게이트웨이에서도 로드밸런싱 할수 있지만 패턴 측면에서 살펴보자.

서비스가 올라가는 컨테이너의 IP정보가 고정되어 있지 않기 때문에 이런 서비스 이름과 IP정보를 매핑하여 보관할 저장소가 필요.

처음 서비스가 등록될 때 위치정보가 저장.

서비스가 종료되면 같이 삭제

#### 라우터

어떤 서비스를 찾아갈지 찾아주는 (ex: Zuul)

#### 로드밸런싱

해당 서비스의 어떤 인스턴스를 찾아갈지 찾아주는 (ex : Ribbon)

서비스가 올라가는 컨테이너의 IP정보가 고정되어 있지 않기 때문에 이런 서비스 이름과 IP 정보를 매핑하여 보관할 저장소가 필요

#### 서비스 탐색(Service discovery)

여러 서비스 인스턴스 생성시 새로 생성된 인스턴스의 발견과 없어진 서비스 감지

레지스터리서비스가 DNS역할, 따라서 서비스 이름으로 접근

라우터가 서비스이름을 찾아서 IP로 접근

서비스 인스턴스 A 10.1.1.1:1000

서비스 인스턴스 C-1 10.1.1.2:2000

서비스 인스턴스 C-2 10.1.1.3:3000

이런 이름, IP주소, port정보를 라우팅 서비스가 활용

ex) spring eureka


### 정리

위에 꺼를 다 해서 pod로도 만들수 있음

라우팅, 로드밸런싱 -> 서비스라고 하는 오브젝트가 해줌.

그래서 이 패틴이 서비스 탐색, 라우팅, 로드밸런싱을 소프트웨어적으로 구현 안하고 쿠버네티스를 바로 적용하면 기본으로 된다.

정리하면 스프링 클라우드 gateway를 가지고 하든 쿠버네티스로 하든 라우팅, 로드밸런싱, 서비스탐색 이걸 관리해라.

# 인증/인가

인증 : 너는 누구니?

인가 : 너는 무슨 권한이 있니?

## 개발 단계

1) 각 서비스에 인증, 인가 서비스 두기

중복, 도메인에 집중하기 힘듬

2) 별도의 서비스를 둠

latency가 증가, 인증은 해결되나 인가는 각 서비스가 비즈니스에 따라 해결해야함)

3) API Gateway에서 인증/인가가 통합된 토큰 발행하자.

각 비즈니스 서비스에서 최종 리소스 허용 판단

#### Stateful

세션 사용.세션을 redis에 저장하고 관리, 서비스가 각각 관리하지 않고 별도 통합 세션 storage를 사용하는 방식

Redis-session Pattern

#### Stateless

JWT, RFC-7519

수신자가 발신자 신원을 확인 할 수 있도록 한 서명된 Json객체

근데 Stateful 이나 Stateless나 BFF에서 처리하는 방식임

## Auth

API G/W서비스가 Auth 기능 포함할 수도 있음

<img width="1270" alt="image" src="https://github.com/user-attachments/assets/6f37b395-28de-4faf-ab4b-3c5fb5edd614">


# Config Management

<img width="1136" alt="image" src="https://github.com/user-attachments/assets/88cabc87-a26d-410d-934b-4c6deb81b398">


## Config

종속성을 없애기 위한 External Configuration 패턴

12 factors 설정 원칙(클라우드에서 돌아갈 어플리케이션은 하드웨어나 컨테이너에 종속된 정보를 가지고 있으면 안된다는 원칙)

## Spring cloud Config

설정파일 변경에 따라 별로 빌드/배포 필요없음

쿠버네티스의 ConfigMap, Secret에서도 할 수 있음

플랫폼이 변경되었을때 쉽게 이동하기 힘듦. 따라서 코드에서 사용하는 환경 설정 정보는 코드와 완전히 분리되어 관리

### K8s – ConfigMap, Secret

비밀번호를 Secret에 관리할 수 있도록 하였고, Secret의 값은 각 컨테이너에 환경변수로 주입된다

<img width="1345" alt="image" src="https://github.com/user-attachments/assets/bb0e8c2f-4083-438e-a5e2-f98c4673be05">

# 중앙화된 로깅, 추적 ,매트릭, 서킷브레이크

중앙화된 metric, 중앙화된 로깅, 분산 추적

중앙화된 로깅

로컬 로깅 X, 중앙 집중형 로깅

중앙 로깅

Log aggregation, Exception tracking

ElasticSearch : 분산현 검색, 분석 엔진 (정형, 비정형, 위치정보, 메트릭 등 원하는 방법으로 검색을 수행)

Logstash : 로그 집합기 (데이터 처리 파아프라인)

Kibana : 시각화 (히스토그램, 막대 그래프, 차트 등)

<img width="1010" alt="image" src="https://github.com/user-attachments/assets/860b4270-c2cc-4902-958f-8fe61fbe6a71">

로그스태시가 수집해서 elastic에 보내서 인덱싱하고 키바나가 이걸 시각화.


## 추적

Zipkin(넷플릭스, 트위터에서 제공), Spring Cloud sleuth, Jaeger(우버에서 제공)

Spring Cloud Sleuth(zipkin client library)

traceID(추적), Span ID (구간) 부여

<img width="942" alt="image" src="https://github.com/user-attachments/assets/9489c81b-6c4c-4d83-9985-bf60a4e63849">


## 서킷 브레이크 패턴

장애격리 : 상황에 따라 서비스를 동적으로 증가시켜 과부하나 오류 상황에서도 지속 가능한 서비스가 가능하도록 관리

-> 실시간으로 관리되어 시각화하고 모니터링

<img width="671" alt="image" src="https://github.com/user-attachments/assets/d20193c6-058d-485e-a06b-f49edad5a41e">

연속 실패 횟수가 임계값을 초과하면 회로 차단기가 작동

시간초과 기간 동안 원격 서비스를 호출하려는 모든 시도가 즉시 실패 됌.

Spring cloud Circuit Breakers와

Netflix Hystrix 또는 Resilience4j 이렇게 요즘 조합한다.

코드로 구현하는 방법도 있지만 너무 노가다, 요즘에 플랫폼(프로바이저: aws)에서 제공하는 도구(서비스)들이 있다

## 중앙화된 메트릭(모니터링)

쿠버네티스 + 프로메테우스 + grafana -> 이 조합을 많이 쓴다.

Springboot(actuator) + 프로메테우스 + 그라파나

쿠버네티스가 모니터링한 내용을 저장

프로메테우스가 이걸 주시하고 있다가 인덱싱해서

그라파나에 전달 그럼 그라파나는 이걸 시각화(대시보드)

혹은 슬랙이나 웹훅으로 보내줌

<img width="1316" alt="image" src="https://github.com/user-attachments/assets/73004e31-a7e1-4dcb-b427-5e73adb06ed2">

## 서비스 메시

서비스 매쉬(mesh)

outer 아키텍처 패턴 적용에 따른 문제

서비스, 인스턴스 증가로 통신이 증가

단일 어플리케이션에서 플랫폼으로 변화.

<img width="1301" alt="image" src="https://github.com/user-attachments/assets/fa735a93-f9a2-4650-b5cf-e1fd4d64c810">

여기서 Istio가 서비스 Mesh

애플리케이션 기반, 프록시 기반

사이드카 패턴

<img width="1084" alt="image" src="https://github.com/user-attachments/assets/dfefbc4a-a9d2-410f-b452-3cc3ff3b153f">

왼쪽처럼 되어 있던 것을 오른쪽으로 변경 오른쪽의 컨테이너를 여러개 배포하면

<img width="1220" alt="image" src="https://github.com/user-attachments/assets/72c5cf67-b570-4cf2-a4c8-59f93dbb332e">

이렇게 된다. (녹색이 비즈니스, 파란색이 sidecar proxy)

이걸 서비스 메시 아키텍처라고 함.

쿠버네티스에서는 서비스 메시 컨트롤 plane을 두고 관리

즉, 서비스 로직과 통신의 분리.

서비스탐색, 로드밸런싱, 라우팅, 서킷브레이커, 분산추적, 메트릭(로그)수집등을 처리한다.

사이드카 패턴 적용

기본 애플리케이션 외 필요한 추가 기능을 별도의 애플리케이션으로 구현하고 이를 동일한 프로세스 또는 컨테이너 내부에 배치

이거의 구현체가 대표적으로 Istio (구글, IBM, Lyft가 함께 참여한 오픈소스)

<img width="749" alt="image" src="https://github.com/user-attachments/assets/4e2b6253-153c-4f1c-8217-a24f980960d5">

envoy를 기본 proxy로 사용

쿠버네티스를 기본으로 지원

#### 각 서비스에서 제공하는 기능들

맨 왼쪽이 MSA의 패턴들

<img width="1363" alt="image" src="https://github.com/user-attachments/assets/48e9c81e-89ce-47e7-88a3-9d2c49b86019">

# Application Modernization유형과 클라우드 전환 프로세스

마이크로서비스가 아닌 클라우드 아키텍처 적용만으로도 충분한 경우가 많음

Application Modernization

<img width="840" alt="image" src="https://github.com/user-attachments/assets/da94f86b-ca06-4756-9f46-011b586d72ef">

굳이 인스턴스를 여러개 쪼개지 않아도 플랫폼, 인프라에서 클라우드 아키텍처만 적용해도 충분한 경우가 많음

CSP(AWS, Azure, GCP) laaS, PaaS, 쿠버네티스 적용이나

DevOps Infra(CI/CD) 도입만 해도 이걸 어플리케이션 모던화라고 부름

Pivotal(vmware Tanzu)이 제시하는 어플리케이션 모던화 유형 /수준

1) Cloud Ready :

app에서 파일 시스템 제거, 혹은 오브젝트 스토리지 도입

독립 실행형 어플리케이션 준비

플랫폼이 관리하는 backing 서비스

2) Cloud Friendly

12 factor 고려, 수평적 확장이 가능한 구조, 플랫폼 차원에서 HA 구조를 지원

3) Cloud Resilient

장애를 고려한 IT 디자인

적극 장애 테스트

모니터링, 메트릭을 중앙화

퍼블릭, 프라이빗 클라우드 스케일 전략

4) Cloud Native

마이크로 서비스 구조 사용 원칙 준수

API 기반 아키텍처

## AWS 래퍼런스

<img width="1330" alt="image" src="https://github.com/user-attachments/assets/adddc1db-cee3-4653-9e24-1f3809a82515">

refactor : 마이크로서비스 만들어라

rehost : vm 써라

relocate : 컨테이너(도커) 써라

replatform : aws에서 제공하는 서비스 사용해라

<img width="1331" alt="image" src="https://github.com/user-attachments/assets/3d341b4e-3938-44cd-9b2f-e02cda9a0225">

## Cloud Modernization 전환 전략

<img width="1367" alt="image" src="https://github.com/user-attachments/assets/4ea4c7ae-9128-4422-928e-91c7e142ce34">

각 단계별로 진행해라.

보통 rearchitect까지만 하는것이 보통이다.

### Rehost

아키텍처, 어플리케이션 변화없이 infra만 변경

기존 레거시 vm과 data source를 그대로 Ec2 VM에 올림.

### Refactor

컨테이너화 DevOps infra구축

수평확장이 가능하도록 어플리케이션 리팩토링

세션공유처리, 내부파일 시스템 의존 제거, 서드 파트 솔루션 클라우드 지원 확인

기존 어플리케이션의 컨테이너 수평확장이 중점.

자동 빌드,배포-> 데브옵스 구축

### Rearchitecutre(Replatform)

프런트 앤드 분리(API 화)

클라우드 backing 서비스 활용(클라우드 스토리지, 오브젝트 db, cloud db활용)

장애 고려 모니터링, 매트릭 기반 서비스 활용

### Rebuild

어플리케이션 재개발 수준

어플리케이션 기능별 서비스로 분리

저장소 격리가 핵심.

# 애플리케이션 패턴

마이크로서비스

프런트앤드, 백앤드 모두 조각으로 구성

## 리액티브 선언

<img width="849" alt="image" src="https://github.com/user-attachments/assets/bc0b9b97-ab40-4ee2-aec6-7c5454b71e4d">

리액티브 선언

리액티비 아키텍처 패턴

응답성이냐 성능이냐

탄력성, 응답성 (미래의 약속)

유연성 : 요청 변화에 맞게 대응

탄력성 : request 증감소에 따른 운영

## 설계 동향

<img width="697" alt="image" src="https://github.com/user-attachments/assets/c9bc2a09-4644-4e0e-97b0-421e6cdda59d">


### ACID 일관성 모델

원자성,일관성, 격리성, 영속

트랜잭션이 종료되었을때, 데이터는 일관적이고 안정적이어야 한다. (RDB)

READ, Write 모델이 모든 인스턴스(노드)가 가지고 있음

### BASE 일관성 모델

가용성, 소프트 상태 유지, 약간의 부정확성을 허용을 통한 빠른 대응(eventual consistency)

key-value, document 데이터베이스

read, write 전용 워커를 둠.


## 마이크로 프런트엔드, 통신 패턴

### 마이크로 프런트엔드

<img width="1150" alt="image" src="https://github.com/user-attachments/assets/0eb1fe27-d3e5-40bd-af1e-8395f77e7a75">

위처럼 잘게 쪼개져 잇기 때문에 빈번한 배포가 이루어짐.

### 통신 패턴

이벤트 주도 아키텍처

REST API를 사용함으로써 발생되는 문제(동기)를 해결

메시지를 보낸 다음 응답을 기다리지 않고 일을 처리

메시지를 보내는 프로듀서

메시지를 처리하는 컨슈머

서로 직접 접속하지 않고 메시지 브로커에 연결

#### 비동기 관련 문제

에러처리

탄력성과 응답성

리액티브 아키텍처 패턴(워크플로 프로세스 패턴) : 메시지가 잘못되거나 실패하면 워크플로 프로세스가 그걸 조치(에러처리 하거나 수정)하고 메시지 보냄

데이터 손실 처리 :

1) 큐에 전달 안됌.전달 되어도 큐가 다운되는 경우.

이 구간은 비동기가 아닌 동기로 처리.

2) 메시지를 꺼내 처리 전에 장애 발생

큐에서 메시지를 저장. 퍼시스턴트 큐 ex)카프카

그리고 컨슈머가 가져갔다는 클라이언트 확인 응답모드를 이용

3) 데이터 에러로 인해 메시지 저장 실패

ACID 트랜잭션으로 처리하면 됌.

db에 저장이 되었는지 확인후 메시지 삭제

## 저장소 격리 패턴

자신이 소유한 데이터는 다른 서비스에 절대 노출X

반드시 API를 통한 접근

### 문제점

데이터 공유와 위임

항공편 검색에 항공편 테이블의 소유권을 준다. 그러면

항공편 추적, 예약은 또 다른 서비스로 분리 할 수 있음.

 <img width="1058" alt="image" src="https://github.com/user-attachments/assets/93dd6f4e-aea9-4b3b-8391-f23d06246ecc">

왼쪽은 안티패턴(안좋은 패턴). 미니 서비스

### API조합

각 서비스에 각 db를 접근하는 권한을 위임하여 서비스를 나눔

그래서 위임한 최종 서비스에서 조합

동기로 되어 있기 때문에 하나라도 죽으면 문제가 생김

### CQRS

이벤트기반

조회 전문 서비스 하나가 있음. 각 서비스별로 db가 저장, 변경되면 조회 전문 서비스에 이벤트 핸들러로 비동기 전달.

### 분산 트랜잭션 처리

분산 트랜잭션 패턴

ACID 적용의 어려움을 극복하기 위한 패턴

1) Saga패턴

서비스별 각각 로컬 트랜잭션을 생성

트랜잭션 사이에 이벤트로 연결

 * Sage 패턴 두 가지
    1) 코레오그래피 : 서로 서비스별 트랜잭션 판단해서 COMMIT 결정
     * 이벤트 기반 아키텍처의 브로커패턴
     * 보상 트랜잭션 : 주문을 생성한 트랜잭션이 끝나고 고객에서 그 주문은 안돼라고 말하면 주문을 생성한 트랜잭션을 롤백해주는 것.
 
  <img width="932" alt="image" src="https://github.com/user-attachments/assets/53865b49-1da9-4335-b669-f196b80abf3c">

  <img width="1303" alt="image" src="https://github.com/user-attachments/assets/a426c1f6-6efa-4e96-b397-8121a87fea1c">

    2) 오케스레이터
     * 이벤트 기반 아키텍처의 중재자 패턴
     * 중재자는 트랜잭션을 구성하는 파트를 하나씩 호출하여 성공/실패 여부를 기록 그 결과에 따른 흐름 조정
     * 중재자는 2단계 커밋을 사용

 <img width="850" alt="image" src="https://github.com/user-attachments/assets/7656eca5-b355-4f75-96f8-a0924d161726">



```text
 2단계 커밋(two phase commit)

첫 번째
첫 번째 단계에서는 노드들에게 트랜잭션 생성과 함께 명령을 수행한다. 여러 노드에서 실행되는 트랜잭션 관리를 위해 이 트랜잭션 id는 coordinator가 관리한다.

 
두 번째
모든 노드들에게 commit이 가능한지 물어본다. 이 요청에 각 노드들은 현재 트랜잭션을 commit 할 수 있는지 응답한다.

 
세 번째
두 번째 단계에서 모든 노드들에게 받은 응답을 취합한다. 하나라도 NO가 있다면 전체 노드들에게 abort를 보내고, 모두가 OK라면 commit을 보낸다.
여기서 재미있는 포인트는 이 요청이 실패했을 때 발생한다. 결과를 취합해서 commit 또는 abort 하라는 명령을 전파할 텐데, 이 요청이 실패하면 어떻게 될까? 아니면 이 순간에 coordinator가 정전으로 죽었다면?

각 노드 입장에서 생각해보면 commit/abort 여부를 coordinator에게 듣지 못하고서는 결정할 수 없다. 따라서 여기까지 진행이 됐다면 안타깝게도 최종 결정을 coordinator에게 들을 때까지 기다릴 수밖에 없다.
```

2) CQRS 패턴

3) 이벤트 소싱 패턴





























