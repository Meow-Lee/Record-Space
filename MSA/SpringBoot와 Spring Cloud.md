# Spring Framework
- EJB의 복잡성에 대한 대안으로 개발되어 두각을 나타냄
- DI와 XML 기반 설정으로 POJO를 그대로 사용 가능
	- 현재는 Annotation이 중심
	- Spring을 걷어내도 Object를 그대로 사용 가능
- 복잡한 설정
	- 컴포넌트 스캔, 디스패쳐 서블릿, 뷰 리졸버, 웹 jar 등
	- 대안으로 Modern Framework 등장
# Spring Boot
- Auto Configuration
	- 특정 jar가 class path 안에 있을 경우 해당 설정을 자동화
	- Convention Over Configuration
		- 특정 폴더에 넣으면 자동으로 인식
		- 정해진 이름대로 파일을 만들면 자동으로 인식
	- @SpringBootApplication
		- @EnableAutoConfiguration + @ComponentScan + @Configuration
- Spring Boot Starter Projects
	- 자주 사용하는 의존성을 패키지화
	- 1개만 등록하면 관련된 모든 의존성이 추가됨
- Embedded Server Integration
	- Embedded Server로 독립으로 실행할 수 있는 웹서비스 구성 가능
	- Default는 Tomcat이지만 변경 가능
	- 웹서비스를 구성하고 배포하는 작업을 최소화 할 수 있음
- Actuator
	- 따로 모니터링 환경 구성하지 말고 기본적인 지표를 확인
	- 운영중인 애플리케이션의 health, metrics 등을 확인 가능
	- REST api로 쉽게 확인
	- Spring 앱과 연동되어 있는 DB 등과 같은 미들웨어의 상황도 파악 가능
# Spring Cloud
- MSA 최적화 된 개발을 위하여 Spring 진영에서 제공하는 오픈 소스
- 분산 환경에서 적용될 수 있는 다양한 아키텍처 패턴들을 구현
- 기존 Spring Application들과 쉽게 통합 가능
# Spring Cloud 와 Netflix OSS
- Netflix OSS는 Netflix에서 MSA를 운영하며 쌓아온 노하우들을 오픈소스로 공개한 것
- 그 중 일부를 Spring Cloud와 통합하여 Spring Cloud Netflix 프로젝트로 제공
	- Hystrix, Eureka, Ribbon ...
- 보다 쉽게 Spring App과 통합될 수 있는 환경 제공
# Spring Cloud Netflix Eureka
- Service Discovery Pattern을 위한 프로젝트
- Eureka Server와 Eureka Client로 구성
# Spring Cloud Config
- 설정 외부화를 위한 프로젝트
- 설정 정보를 저장하고 Serving하는 Server 구축
- 각 클라이언트는 설정 서버로부터 설정 정보 조회
# Spring Cloud Netflix Hystrix
- 한 서비스의 장애가 다른 서비스로 전파되지 않도록 사전에 차단
- 특정 서비스로의 호출이 일정 수준 이상으로 실패할 경우 호출 차단
# Spring Cloud Netflix Zuul
- Microservices 앞 단에 위치하는 API Gateway
- 클라이언트의 호출을 받아 뒷 단의 Microservices에 전달
- 모든 Service들이 처리해야하는 공통 코드를 처리
# Spring Cloud Stream
- Event Driven MSA를 구축하기 위한 프로젝트
- 다양한 Messaging Platfor과 동일한 인터페이스로 연동
- RabbitMQ, Kafka, AWS Kinesis, GCP PubSub 등을 지원
# Spring Cloud의 한계
- Java만 주로 사용 가능
- MSA는 Polyglot Architecture를 권장
- 대안으로 Kubernetes, lstio 등의 조합 사용 가능