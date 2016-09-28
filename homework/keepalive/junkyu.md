HTTP의 Keep-Alive
====

HTTP 프로토콜의 Keep-Alive는 HTTP Header의 일종이다.
이는 HTTP/1.0에서 지원하지 않던 지속 커넥션을 가능하게 하기위해서 쓰였다.

그렇다면 지속 커넥션이 뭔지부터 보자. 지속 커넥션을 보기전에 HTTP의 커넥션에 대해 알아보자.

HTTP/1.1이전에는 클라이언트와 서버사이에 트랜잭션 한번이 일어나면 HTTP Connection이 끊어졌다.
그런데 이렇게 되면 TCP 커넥션을 맺는데 발생하는 지연과 느린 시작 지연이 트랜잭션마다 발생하기 때문에, 
한 웹페이지에서 여러 이미지와 html을 요청해야하는 경우 성능이 매우 안 좋아진다.

그래서 이런 커넥션을 맺고 끊는데서 발생하는 지연을 없애기 위해서 한번 연결한 TCP 커넥션을 재활용하는 방법이 나왔는데, 
그게 바로 지속 커넥션(persistent connection)이다.

이는 HTTP/1.1에서는 디폴트로 지원하지만, HTTP/1.0에서 지속 커넥션을 사용하려면 특정한 헤더들을 추가해줘야 한다.
바로 Connection 헤더와 Keep-Alive헤더 인데, 
HTTP 요청을 보낼때 

> Connection: Keep-Alive

와 같이 Connection헤더에 Keep-Alive를 응답을 보낸다.
이는 클라이언트 측에서 커넥션을 유지하기를 바라는 요청일 뿐, 서버가 이를 지켜준다는 보장은 없다.

서버는 응답으로 

> Connection: Keep-Alive  
> Keep-Alive: max=5, timeout=120  

와 같은 Keep-Alive헤더를 추가적으로 보낼 수 있는데 
* Keep-Alive의 max 파라미터는 커넥션이 몇 개의 HTTP 트랜잭션을 처리할 때까지 유지될 것인지를 의미한다.  
* Keep-Alive의 timeout 파라미터는 커넥션이 얼마동안 유지될 것인가를 나타내고, 위의 예시에선 2분동안 커넥션을 유지하라는 내용이다.  

이 두 파리미터는 OR조건으로 작용한다.

그러나 이 Connection: Keep-Alive는 이해를 하지 못하는 프락시들이 받게되면 치명적인 버그가 발생해 클라이언트와 서버간에 커넥션이 이뤄지지 않는다.(Keep-Alive, dump proxy)

또한 Connection헤더는 여러가지 기능으로 사용되는데, 구글링을 하면 많이 나와있을 것이다.

----

TCP의 keepalive
====

keep TCP alive라고 의미를 이해하면 된다. 이는 연결된 TCP 소켓을 체크할 수 있고 TCP 연결이 여전히 진행중인지 혹은 끊어졌는지를 결정한다.

기본적으로 TCP 커넥션을 맺을 때 타이머 셋을 연결한다. 이 타이머들중 몇몇은 keepalive 절차를 다룬다.
keepalive 타이머가 0에 도달하면 연결된 상대에게 keepalive probe 패킷을 보낸다. 이 때 이 probe 패킷은 아무 데이터도 들어있지 않으며 ACK 플래그만 있다.
그리고 그에 대한 응답으로 데이터가 없는 ACK 플래그가 설정된 패킷을 받게 된다.

만약 keepalive probe를 받게되면 커넥션이 계속 유지되는 것으로 생각할 수 있다. 
