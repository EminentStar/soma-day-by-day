# Logging Requirements
## Required Log
1. HTTP Request: (요청날짜/시간, method)
> * 사용자 접속횟수를 분석을 위함
2. Scrap Request: (요청날짜/시간, 요청 URL, error 유무)
> * 전체 스크랩 요청 횟수 파악, URL별 스크랩 요청 횟수 파악
3. Scrap Error: (요청날짜/시간, 요청 URL, ERROR 메시지)
> * 어떤 에러가 났는지에 파악
4. Cache Access :(접근 날짜/시간, 접근캐시서버 이름, 캐시저장or조회, 접근 URL)
> * 각 캐시 서버별 접근(api 데이터 SET, GET) 횟수를 통해 각 캐시 서버별 부하 상황을 체크할 수 있기 위함.
5. Other Errors: (날짜/시간, StackTrace)
> 스크랩을 제외한 파악가능한 모든 에러의 message를 로그화한다.

## Files or DB?
### 데이터는 파일에 저장하도록 한다.
**DB에 저장을 하면 좋지않다고 생각하는 이유는,**  
1. 로그를 각각의 로컬 서버의 디비에 저장한다하더라도, 서버별로 분산된 로그디비를 통합하는 것 또한 트래픽이 되므로 부하의 원인이 될 수 있다.  
*(그러나 Scrap Error 로그 정도는 디비 관리를 고려해볼 수 도 있을 것 같긴하다. )*

### 우선적으로 텍스트 기반의 파일에 json형태로 저장하도록한다.

### (보류) 파일 저장을 위해 syslog를 사용(syslog: Unix 계열 OS의 로그 집약의 허브 역할)
* why
> 1. syslog는 facility 라벨이 붙어서 어떤 소프트웨어가 에러를 내는지 파악가능
> 2. 각 서버들은 syslog 서버에 로그를 보낼 수 있다.(로그 통합에 유리)
> 3. syslog는 unix 계열 OS의 표준 로그 솔루션으로 자리 잡아 다양하게 구현된 프로그램들이 많다.

* Disadvantage
> 1. UDP 프로토콜을 사용하기에 데이터 손실 가능
> 2. 보안이 없다고 함.

### 로그는 하루마다 수집한다. 이를 통해 주간, 월간, 년간 로그 분석이 가능할 수 있다.

### 가능하다면 로그용 서버를 두어 로그를 통합할 수 있또록 한다.

