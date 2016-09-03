##해쉬에서 충돌이 무엇이고, 충돌을 어떻게 회피하는지에 대해서 조사하시오.



##2. HTTP Protocol 에서 request에서 사용하는 USER-AGENT 헤더를 조사하고,

## 실제 facebook에서 open graph explorer가 사용하는 facebook의 USER-AGENT를 조사하시오. USER-AGENT 값으로 어떤 변화를 줄 수 있을까요?





* 해쉬에서 충돌은 무엇일까?



> 해시 충돌이란 해시 함수가 서로 다른 두 개의 입력값에 대해 동일한 출력값을 내는 상황을 의미한다.







* 충돌은 어떻게 피할 수 있을까?



> 1. Table Size를 소수로 한다. (ex: 37) 완벽하게 충돌을 피할 수 있는 것은 아니지만 충돌이 발생 할 확률이 적어진다. 





* 충돌이 발생했을 때 어떻게 문제를 해결 할 수 있을까?



> 크게 두가지 방법이 있다. 주소 밖에 새로운 공간을 할당하여 문제를 해결하는 방법(Chaining)

  과 처음에 주어진 해시 테이블의 공간 안에서 문제 해결(Open Addressing)방법이 있다.



> 1. Chaining : 충돌이 발생하면 각 데이터를 해당 주소에 있는 링크드 리스트에 삽입하여 문제를 해결하는 방법.



> 2. Open Addressing : Linear Probing(충돌이 발생하면 해시 테이블 내의 새로운 주소를 탐사(Probe)하여 충돌된 데이터를 입력하는 방식), Quadratic Probing(Linear Probing은 고정폭만큼 이동하는 것에 비해 Quadrativ Probing은 이동폭이 제곱수로 늘어난다), Double Hashing(클러스터 방지를 위해, 2개의 해시 함수를 준비해서 하나는 최초의 주소 방법이 있다.

                         

* User-Agent란? 


> User-Agent: <something>은 HTTP클라이언트(브라우저, 봇 등)가 HTTP 요청을 서버로 보내면서 전송하는 문자열이다. User-Agent 구문은 "/(슬래쉬)와 버전 명을 포함한 소프트웨어 제품 이름" 
으로 정의되어 있다. User-Agent 문자열이 나타난다면 클라이언트에 의해 사용된 소프트웨어 프로그램 정보를 전달한다. 이는 통계 목적과 프로토콜 위반을 추적하기 위한 것이기
때문에 반드시 포함해야 한다.



* facebook에서 open graph explorer가 사용하는 facebook의 USER-AGENT



> Facebook 크롤러는 다음 User-Agent 문자열 중 하나로 식별할 수 있다. facebookexternalhit/1.1 (+http://www.facebook.com/externalhit_uatext.php) 또는 facebookexternalhit/1.1 이러한 User-Agent 중 하나를 타겟으로 지정하여 메타데이터만 있고 실제 콘텐츠가 없는 페이지의 비공개 버전을 Facebook 크롤러에 제공할 수 있다. 그러면 성과를 최적화할 수 있고 paywall이 적용된 콘텐츠를 안전하게 유지하는 데 유용하다. 2014년 5월 28일부터 다음 User-Agent 문자열이 포함된 크롤러도 확인할 수 있다.

*  USER-AGENT 값으로 어떤 변화를 줄 수 있을까요?

> 1. User-Agent 값을 통해 모바일 사이트를 위한 반응형 디자인을 구현할 수 있다.

> 2. 모든 브라우저에 맞는 반응형 디자인을 구현할 수 있다.

> 3. 어떤 클라이언트를 통해 사이트에 접속하는지 추적, 통계를 진행할 수 있다.
