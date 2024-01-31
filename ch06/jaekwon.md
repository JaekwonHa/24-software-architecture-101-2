## 6장. 아키텍처 특성의 측정 및 거버넌스

아키텍처 특성 자체도 굉장히 다양하고, 사람마다 생각하는, 정의하는 바가 다르다

* 물리학이 아니다
* 정의가 너무 다양하다
* 너무 복합적이다
    * 아키텍처 특성들은 다시 더 작은 영역으로 세분화할 수 있다

이러한 문제를 해결하기 위해서는 아키텍처 특성을 객관적으로 정의할 필요가 있다

* 운영적 측정
    * '특정 요청에 대한 평균 응답 시간'을 어떻게 정의할 것인가?
        * 평균 응답 시간 만큼이나 특이점, 최대 응답 시간도 중요하다
    * 최초 렌더링 시간, 최초 CPU 유휴
* 구조적 측정
    * 내부 코드 품질
    * 코드의 복잡도는 순환 복잡도라는 메트릭으로 측정 가능
        * 코드에 그래프 이론을 적용. 상이한 실행 경로를 유발하는 결정점을 이용. 그래프를 그린다
        * 얼마가 적당한가? 그때그때 다르다. 그래도 50 이하가 업계 표준
* 프로세스 측정
    * 소프트웨어 개발 프로세스와 교차하는 아키텍처 특성도 있다
        * ex. 민첩성, 시험성, 배포성. 이런 것들을 달성하려면 배포 소요 시간, 성공률 같은 메트릭도 있어야 하고, 민첩하게 개발하기 위해서는 코드 구조도 그게 가능해야한다

### 6.2 거버넌스와 피트니스 함수

아키텍처 특성과 우선순위를 정해도 개발자들이 지키지 않는다면?
거버넌스 메커니즘이 필요하다. 소프트웨어 품질 보장을 위해서

익스트림 프로그래밍 -> 지속적 통합(CI) -> 운영 자동화, 데브옵스 -> 계속 발전
Building Evolutionary Architectures 책 참고


피트니스 함수: 어떤 아키텍처 특성(혹은 특성 조합)의 객관적인 무결성을 평가하는 '모든 메커니즘'
새로운 프레임워크가 아니라 새로운 시각. 다양한 도구로 구현할 수 있다

* 메트릭
* 모니터링
* 단위 테스트
* 카오스 엔지니어링
* ...

순환 의존성
-> `JDepend`라는 메트릭 도구로 패키지 간 의존성을 체크

메인 시퀀스로부터의 거리
-> `JDepend`로 수용 가능한 임계치 설정. 클래스가 이 범위를 벗어나는지 확인
-> `ArchUnit` 레이어 간의 올바른 관계를 정의, 모듈성에 특화된 테스트 작성 가능

카오스 멍키, 시미안 아미