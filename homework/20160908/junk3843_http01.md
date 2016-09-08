클라이언트에서 nginx/apache 등의 웹 서버에 데이터를 보낼때, Request 와 Response 측면에서 어떤 데이터들이 전달되는지 정리하시오. GET 형식과 POST 형식으로 보낼 때, HTTP-Header 들과 실제 데이터가 어떤식으로 전달되는지 샘플과 각각의 설명을 달아주세요.
=
----

## 클라이언트에서 웹 서버로 Request를 보낼 때, 자주 사용하는 메소드로는 GET과 POST가 있다.

GET 메소드는 웹 서버로부터 데이터를 요청하지만, 서버의 데이터를 수정하지는 않는다.

POST 메소드는 서버의 상태를 변화시킬 수 있다.

----

GET 방식의 전송되는 데이터로는
* Request Line
* Request Header
가 있다.

POST 방식의 전송되는 데이터로는
* Request Line
* Request Header
* Message body

가 있다.

## Request Line은 HTTP메소드와 웹서버상에서의 자원에 대한 경로, 파라미터, 프로토콜 버전을 담고있다.

----

> GET / HTTP/1.1

## Request Header에 들어갈 수 있는 필드는 아래와 같다.
* Accept: 요청에 대한 응답이 가능한 Content-Type을 서술해놓은 것
>> Accept: text/plain

* Accept-Charset: 수용가능한 Character set
>> Accept-Charset: utf-8


* Accept-Encoding: 수용가능한 인코딩 목록
>> Accept-Encoding: gzip, deflate


* Accept-Language: 응답을 위한 수용가능한 자연어 목록
>> Accept-Language: en-US

* Accept-Datetime:  원래 리소스의 희망되는 과거 상태 Datetime을 가리킨다.
>> Accept-Datetime: Thum 31 May 2007 20:35:00 GMT

* Authorization: HTTP 인증을 위한 인증 스펙
>> Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

* Cache-Control: 요청-응답 체인에서 모든 캐싱 메카니즘에 의해 복종되어져야만하는 모든 지시를 상세화시키기 위해 사용되는 것
>> Cache-Control: no-cache

* Connection: 현재 커넥션, 그리고 hop-by-hop 요청 필드의 목록에 대한 컨트롤 옵션
>> Connection: keep-alive

>> Connection: Upgrade

* Cookie : Set-Cookie와 함께 서버에 의해서 이전에 보내진 HTTP Cookie
>> Cookie: $Version=1; Skin=new;

* Content-Length : request body의 길이
>> Content-Length: 348

* Content-MD5 : request body의 Base64의 인코딩된 바이너리 MD5의 총합
>> Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

* Content-Type : request body의 MIME 타입 
>> request body의 MIME 타입 

* Date : 요청 메시지가 발생된 날짜 및 시간
>> Date: Tue, 15 Nov 1994 08:12:31 GMT

* Expect : 클라이언트에 의해 요구되어지는 서버의 특정 행동을 가리킴
>> Expect: 100-continue

* Forwarded : HTTP 프락시를 통해 웹서버에 연결된 클라이언트의 노출된 원래 정보
>> Forwarded: for=192.0.2.60;proto=http;by=203.0.113.43 Forwarded: for=192.0.2.43, for=198.51.100.17

* From : request를 생성한 유저의 email 주소
>> From: user@example.com

* Host : 서버의 도메인 이름과 서버가 listening하고 있는 TCP 포트 번호; HTTP/1.1부터 의무로 쓰여야 함.
>> Host: en.wikipedia.org:8080

* If-Match : 만약 entity가 제공하는 클라이언트가 서버에서의 entity와 같다고 매치될때만 수행하는 것?; 이것은 PUT메소드와 같이 리소스를 수정할 때 사용하는 메소드를 위한 것
>> If-Match: "737060cd8c284d8af7ad3082f209582d"

* If-Modified-Since : 만약 컨텐츠가 바뀌지 않았다면 304 Not Modified가 리턴되는 것을 허락함.
>> If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT

* If-None-Match : 만약 컨텐츠가 바뀌지 않았다면 304 Not Modified가 리턴되는 것을 허락함.
>> If-None-Match: "737060cd8c284d8af7ad3082f209582d"

* If-Range : entity(어떤 entity지)가 변하지않았다면, 놓치고있는 파트를 전송한다. 그렇지않다면 전체의 새로운 entity를 보낸다. 
>> If-None-Match: "737060cd8c284d8af7ad3082f209582d"

* If-Unmodified-Since : 오직 entity가 특정 시간 이후로 수정되지 않았을때만 응답을 보낸다.
>> If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT

* Max-Forwards : 게이트웨이나 프락시를 통해 메시지가 포워딩될 수 있는 횟수 제한
>> Max-Forwards: 10

* Origin : Cross-Origin Resource Sharing을 위한 요청을 초기화한다.
>> Origin: http://www.example-social-network.com

* Pragma : 요청-응답 체인 어디에서도 다양한 효과를 가지는 특정 필드의 구현
>> Pragma: no-cache

* Proxy-Authorization : 프락시로의 접속을 위한 인증 스펙
>> Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

* Range : entity의 일부만 요청한다. 바이트는 0부터 가능하다.
>> Range: bytes=500-999

* Referer : 이 페이지가 요청한 이전 페이지가 무엇인지를 알려준다.
>> Referer: http://en.wikipedia.org/wiki/Main_Page

* TE : User-agent가 수용할 만한 전송 인코딩
>> TE: trailers, deflate

* User-Agent : User-agent의 user-agent 문자열
>> User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:12.0) Gecko/20100101 Firefox/21.0

* Upgrade : 서버에게 다른 프로토콜로 업그레이드하라고 요청한다.
>> Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket

* Via : 요청이 보내진 곳을 통해 서버의 프락시를 알아낸다.
>> Via: 1.0 fred, 1.1 example.com (Apache/1.1)

* Warning : entity body와 함께 가능성 있는 문제에 대한 일반적인 경고
>> Warning: 199 Miscellaneous warning

----

## POST 메소드의 Request에는 Request Line과 Request Header뿐만 아니라 Message Body도 추가된다. GET에서는 Request Line에 파라미터를 붙였지만, 길이제한이나 보안적 이슈 때문에 POST에서는 Message Body에 추가되며 제한이 없다.

### HTTP의 응답은 Status-Line(headers)과 body로 구성되어 있다.

Response Header
------
* Access-Control-Allow-Origin : Cross-Origin Resource Sharing에서 웹사이트가 참여할 수 있는지를 상세화한다.
>> Access-Control-Allow-Origin: * 

* Accept-Patch: 서버가 어떤 patch document 형식을 지원하는지 기술한다.
>> Accept-Patch: text/example;charset=utf-8

* Accept-Ranges : byte serving을 통해 서버가 지원하는 어떤 부분의 컨텐츠 범위 타입
>> Accept-Ranges: bytes

* Age : 프락시 캐시에서 오브젝트가 존재한 시간(초)
>> Age: 12

* Allow : 특정 리소스에 유효한 action. '405 Method not allowed'에 사용된다.  
>> Allow: GET, HEAD

* Alt-Svc : 서버에서 사용되는데, 서버의 리소스가 다른 네트워크에서 접속 가능하거나 다른 프로토콜을 사용할 수 있다는 것을 가리킨다.
>> Alt-Svc: h2="http2.example.com:443"; ma=7200

* Cache-Control : 서버로부터 클라이언트로의 모든 캐싱 메카니즘; 이것이 캐시될것이라는 것을 말해준다.
>> Cache-Control: max-age=3600

* Connection : 현재 커넥션과 hop-by-hop 목록을 위한 컨트롤 옵션
>> Connection: close

* Content-Disposition : 컨텐트 타입의 옵션이기도 하고, 실제로 지정된 파일명을 지정함으로써 더 자세한 파일의 속성을 알려줄 수 있다.
>> Content-Disposition: attachment; filename="fname.ext"

* Content-Encoding : 데이터에서 사용되는 인코딩 타입
>> Content-Encoding: gzip

* Content-Language : 콘텐츠에서 응답을 받는 사용자의 자연어
>> Content-Language: da

* Content-Length : response 바디의 길이
>> Content-Range: bytes 21010-47021/47022

* Content-Location : 반환되는 데이터를 위한 대안적 위치 
>> Content-Range: bytes 21010-47021/47022

* Content-MD5 : 응답 콘텐츠의 Base64 인코딩 바이너리 MD5의 합
>> Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

* Content-Range : 전체 바디 메시지에서 해당 메시지가 속해있는 위치
>> Content-Range: bytes 21010-47021/47022

* Content-Type : 컨텐츠의 MIME 타입
>> Content-Type: text/html; charset=utf-8

* Date : 메시지가 보내진 날짜와 시간
>> Date: Tue, 15 Nov 1994 08:12:31 GMT

* ETag : 리소스의 특정 버전을 위한 id; 주로 메시지 다이제스트가 쓰인다.
>> ETag: "737060cd8c284d8af7ad3082f209582d"

* Expires : 응답이 만기되는 날짜/시간
>> Expires: Thu, 01 Dec 1994 16:00:00 GMT

* Last-Modified : 요청된 객체가 마지막으로 수정된 날짜
>> Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT

* Link : 서버에서 클라이언트가 요청된 리소스에 대한 메타데이터를 포함하는 또다른 데이터를 가리키는 걸 허락한다.
>> Link: </feed>; rel="alternate" 

* Location : 리디렉션에서 사용되거나, 새로운 리소스가 생성되었을 때 사용한다.
>> Location: http://www.w3.org/pub/WWW/People.html

* P3P : P3P 정책을 설정하는 필드이다.
>> P3P: CP="This is not a P3P policy! See http://www.google.com/support/accounts/bin/answer.py?hl=en&answer=151657 for more info."

* Pragma : 요청-응답 체인 어디에서도 다양한 효과를 가지는 특정 필드의 구현
>> Pragma: no-cache

* Proxy-Authenticate : 프락시에 접근하기 위한 Request 인증
>> Proxy-Authenticate: Basic

* Public-Key-Pins : 웹 클라이언트에게 특정한 암호학적 공개키가 사용됬다는 걸 알려준다.
>> Public-Key-Pins: max-age=2592000; pin-sha256="E9CZ9INDbd+2eRQozYqqbQ2yXLVKB9+xcprMF+44U1g=";

* Refresh : 리디렉션에서 사용되거나 새로운 리소스가 생성될때 사용된다. 아래의 refresh는 5초후에 리디렉트된다.
>> Refresh: 5; url=http://www.w3.org/pub/WWW/People.html

* Retry-After : entity가 일시적으로 사용불가능할때 이것은 클라이언트가 나중에 시도하도록 지시한다.
>> Retry-After: 120

* Server : 서버의 이름
>> Server: Apache/2.4.1 (Unix)

* Set-Cookie : HTTP Cookie
>> Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1

* Status : HTTP 응답의 상태를 표시한 CGI 헤더 필드
>> Status: 200 OK

* Strict-Transport-Security : HTTP 클라이언트가 얼마나 HTTPS을 캐싱 할 것인가와 이것을 서브도메인에도 적용할 것인가를 알려주는 HSTS 정책
>> Strict-Transport-Security: max-age=16070400; includeSubDomains

* Trailer : 헤더 필드가 chunked transfer coding으로 인코딩 된 메시지의 trailer에서 표현된다는 것을 나타내는 필드
>> Trailer: Max-Forwards

* Transfer-Encoding : entity를 유저에게 안전하게 전송하기 위한 인코딩 폼
>> Transfer-Encoding: chunked

* TSV : Tracking Status Value의 줄임말; 응답에서 추적하지 말아야할 값
>> TSV: ?

* Upgrade : 클라이언트에게 다른 프로토콜로 업그레이드하라고 요청한다.
>> Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket

* Vary : 캐시된 entity가 다중 지원을 가지고 있으므로 요청한 헤더를 지정한 목록이 상황에 따라 변할 수 있다는 것을 지정한다.
>> Vary: *

>> Vary: Accept-Language

* Via : 브라우저로 응답을 보낸 프락시 클라이언트 정보
>> Via: 1.0 fred, 1.1 example.com (Apache/1.1)

* Warning : entity body와 함께 가능성 있는 문제에 대한 일반적인 경고 

* WWW-Authenticate : 요청된 entity에 접속하는데 사용되어져야하는 인증 스키마
>> WWW-Authenticate: Basic

* X-Frame-Options : 브라우저가 frame, iframe, 또는 object에서 페이지를 렌더링하는 것을 허락할 건지에 대한 것으로 사용된다.
>> X-Frame-Options: deny

HTTP 호출 구조 및 데이터 전송방식(GET/POST)
----

> **URL 분석**: 먼저 요청을 보내게되면 웹 클라이언트에서 URL 분석을 한다. 입력한 URL을 분석해 프로토콜, 호스트, 서버 포트, 호출 파일등을 분석한다. 

> **도메인 해석 및 서버 접속**: 웹 클라이언트에서 서버로 접속을 할 때, 도메인을 IP 주소로 변환하는 과정이 필요하다. DNS 서버에 질의를 하여 호스트명을 IP주소로 반환한 값을 얻어와 해당 IP주소와 포트로 접속을 하게 된다. 

> **Request Header 전송**: 
>> GET 메소드는 request URI에서 지정한 어떤 정보든간에 가리지 않고 Entity body(=message body)로 전달해 달라고 요청할 수 있다. 

>> POST 메소드는 message body에 포함되있는 데이터를 request line에 있는 request URI로 넘겨준다. 이때  Content-Length 헤더만 빼먹지 않는다면 CGI 프로그램이 처리가 가능하다. 서버가 매번 request message에 대해 똑같은 응답을 할지를 알 수 없기에 클라이언트에서는 캐싱을 할 필요가 없다.

> **Request Data 전송**: POST 방식으로 데이터를 전송할때는 Request Header를 서버로 전송한 후에 Request데이터를 보낸다. 데이터를 보내는 방식에는 2가지가 있다.
 1. form-urlencoded: 일반적인 폼데이터(주로 텍스트)만 전송
 2. multipart-formdata: 서버로 파일을 전송할 때

> **Response Header 전송**: Request에 대한 응답 헤더를 전송한다.

> **Response Body 전송**

----

## http://www.coupang.com GET 전송
#### Request Header
```
GET / HTTP/1.1 
Host: www.coupang.com 
Connection: keep-alive 
Cache-Control: max-age=0 
Upgrade-Insecure-Requests: 1 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.89 Safari/537.36 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8 Accept-Encoding: gzip, deflate, sdch 
Accept-Language: ko-KR,ko;q=0.8,en-US;q=0.6,en;q=0.4 
Cookie: 100=a370788z_1:147572606@; _mkto_trk=id:155-EZY-629&token:_mch-coupang.com-1470233793412-85268; SUID="junk3843@naver.com"; gd1=Y; trackingNumber="NXUweFQ0WTM4cjJmMlMzbVlwRmRqM21NU05ZeTVVN0xvK1NrSXNIR0dGb0d4KzZRRUhGTzIzMk9kbU42aE1oa21aMnJrWDFwdXZ0L3ZLeXdNaXhPTWZBTUh5cGFKMHJEdHdFdWZ0NGJkeC9GSWw2L0p5VXJTSHM5d1p3cno3VnNsaVlPM1NpeUVzNlNvVFViZG5zQ2R3PT0="; member_srl=41220082; overrideAbTestGroup=%5B%5D; ABTESTGROUP_MWEB=%7B%2229%22%3A%22A%22%2C%2269%22%3A%22A%22%2C%22151%22%3A%22A%22%2C%22168%22%3A%22A%22%2C%22279%22%3A%22A%22%2C%220%22%3A%22B%22%2C%22366%22%3A%22A%22%2C%22357%22%3A%22A%22%2C%22405%22%3A%22B%22%2C%22406%22%3A%22B%22%2C%22407%22%3A%22B%22%2C%22432%22%3A%22B%22%2C%22514%22%3A%22A%22%2C%22579%22%3A%22B%22%2C%22669%22%3A%22A%22%2C%22691%22%3A%22B%22%2C%22954%22%3A%22B%22%2C%221002%22%3A%22B%22%2C%221088%22%3A%22B%22%2C%221176%22%3A%22B%22%2C%22864%22%3A%22A%22%2C%22909%22%3A%22B%22%2C%221250%22%3A%22A%22%2C%221184%22%3A%22B%22%2C%221245%22%3A%22B%22%2C%221179%22%3A%22B%22%2C%221218%22%3A%22B%22%2C%221495%22%3A%22B%22%2C%221580%22%3A%22C%22%2C%221307%22%3A%22B%22%2C%221324%22%3A%22B%22%2C%221417%22%3A%22B%22%2C%221493%22%3A%22A%22%2C%221558%22%3A%22B%22%2C%221639%22%3A%22B%22%2C%221660%22%3A%22B%22%2C%221670%22%3A%22A%22%2C%221698%22%3A%22B%22%2C%221760%22%3A%22C%22%2C%221736%22%3A%22B%22%7D; helloCoupang=Y; _gat=1; PERSON_CTGR_HOME_CODE=NO_LOGIN; SUBCARTIC=0; _ga=GA1.2.999212496.1469506746; _gat_UA-17885426-32=1; PCID=28364572469837488412176; sid=7d1f5126362a4ca39ea2f82625bcc8e8ee4e0f94; baby-isWide=small
```

우선 이 Request는 GET 메소드로 요청되었고, 웹서버에서의 자원에 대한 경로는 /이며 HTTP 1.1 프로토콜을 사용한다.
클라이언트와 서버간의 연결은 keep-alive로 정의된 시간까지 접근이 없더라도 대기를 하며 계속 연결된 상태를 유지한다.
Cache는 max-age=0으로 지정하여 항상 새로 요청을 한다.
User-Agent는 Mac OS X의 크롬브라우저를 사용중이다.
요청에 대한 응답이 가능한 Content-Type으로는 text/html, application/xhtml+xml, application/xml, 그리고 내가 이해하지 못한 이상한 포맷들이 있다.
클라이언트가 요청에서 허용하는 인코딩 유형으로는 gzip, deflate, sdch가 있다.
수용가능한 언어로는 한국어, 영어가 있다.
또한 서버로부터 이전에 보내진 HTTP 쿠키가 남아있다.

----

#### Response Header
```
HTTP/1.1 200 OK 
Server: nginx 
Content-Type: text/html;charset=UTF-8 
Vary: Accept-Encoding 
X-UA-Compatible: IE=edge 
Pragma: no-cache 
Expires: Thu, 01 Jan 1970 00:00:00 GMT 
Cache-Control: no-cache 
Cache-Control: no-store 
Content-Language: ko-KR 
Content-Encoding: gzip 
Date: Thu, 08 Sep 2016 17:16:17 GMT 
Content-Length: 44030 
Connection: keep-alive 
Set-Cookie: sid=7d1f5126362a4ca39ea2f82625bcc8e8ee4e0f94; Domain=coupang.com; Expires=Tue, 13-Sep-2016 17:16:17 GMT; Path=/ Set-Cookie: PERSON_CTGR_HOME_CODE=NO_LOGIN; Domain=.coupang.com; Expires=Thu, 08-Sep-2016 17:26:17 GMT; Path=/
```

응답의 상태 코드는 200으로 리퀘스트가 정상으로 처리되었음을 나타내고, 웹 서버는 nginx이다.
응답 컨텐츠의 MIME Type은 text/html이고, charset은 utf-8이다.
해당 사이트에서 추천하는 렌더링 엔진은 IE-edge이고, 
Pragma와 Cache-Control을 no-cache로 지정함으로써 브라우저나 프락시 서버로 부터 요청시에 캐시된 문서를 사용하지 말고 매번 서버로부터 새로운 문서를 다시 전송받아 사용하도록 한다. 또한 브라우저에서는 캐시를 저장하지 않으며 응답되는 메시지의 언어는 한국어이다. 응답에서 사용하는 압축 알고리즘은 gzip이고, 응답 메시지가 보내진 시간은 2016년 9월 8일 목요일 17시 16분 17초이다. Response body의 전체 길이는 44030바이트이며, 클라이언트-서버간 연결은 keep-alive방식이다.

----

POST 방식의 데이터 샘플을 브라우저에서 추출하려고하는데, POST 요청을 날리면 바로 GET 으로 재호출을 해서 request 및 response를 확인을 할 수 없는 것 같다. 방법을 강구해봐야겠다.



