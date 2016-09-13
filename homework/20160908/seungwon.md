#HTTP 조사 과제 
@(소마)

클라이언트에서 nginx/apache 등의 웹 서버에 데이터를 보낼 때, Request 와 Response 측면에서 어떤 데이터들이 전달되는지 정리하시오. GET 형식과 POST 형식으로 보낼 때, HTTP-Header 들과 실제 데이터가 어떤식으로 전달되는지 샘플과 각각의 설명을 달아주세요.

---

##전달되는 데이터 형식

요청(Request)과 응답(Response)에 전달되는 데이터 형식은 아래와 같습니다.

`Request`

> Request-Line
> Request-Header
> [ message-body ]

`Response`

> Status-Line
> Response-Header
> [ message-body ]

---

### Request

이제 HTTP Request를 구성하는 요소에 각각에 대해 설명하겠습니다. 

`Request Line`
Request Line은 요청에 첫줄에 전달되는 데이터로 아래와 같은 형식으로 구성되어 있습니다.
> [HTTP 요청 메서드] [요청 URL] [HTTP 버전]
> (예시) GET /index.html HTTP/1.1

`Request-Header`
Header에 들어있는 필드는 이름, 값 쌍으로 이루어져 있으며 HTTP 통신을 제어합니다.  HTTP 필드는 아래와 같습니다. 

- Accept 
> 응답으로 받아들일 수 있는 콘텐츠의 형식을 명시한 값입니다.
> ex> Accept : text/plain

- Accept-Charset
> 응답으로 받아들일 수 있는 문자 형식을 명시한 값입니다.
> ex> Accept-Charset: utf-8

- Accept-Encoding
> 응답으로 받아들일 수 있는 인코딩 형식을 명시합니다.
> ex> Accept-Encoding : gzip, deflate

- Accept-Language
> 응답으로 받아들일 수 있는 언어를 명시한 값입니다.
> ex> Accept-Language : en-US

- Accept-Datetime
> 응답으로 받아들일 수 있는 버전 시각을 명시한 값입니다.
> ex> Accept-Datetime: Thu, 31 May 2007 20:35:00 GMT

- Authorization
> 인증 자격을 담은 값입니다.
> ex> Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

- Cache-Control
> 요청 응답 과정에서 반드시 따라야하는 모든 캐시 매커니즘에 대한 지시를 명시한 값입니다.
>ex> Cache-Control: no-cache

- Connection
> 현재 연결에 대한 제어 옵션을 담은 값입니다.
> ex> Connection: keep-alive
> ex> Connection: Upgrade

- Cookie
> 이전에 서버에서 Set-Cookie 과정을 통해 보내진 쿠키 값이 담은 값입니다.
> ex> Cookie: $Version=1; Skin=new;	

- Content-Length	
> requset body의 길이가 담겨 있는 값입니다.
> ex> Content-Length: 348

- Content-MD5
> request body에 담긴 컨텐츠의 md5 값입니다.
> ex> Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

- Content-Type
> request body의 MIME type입니다. POST와 PUT  메서드에 의한 요청에서 사용됩니다. 
> ex> Cookie: $Version=1; Skin=new;	

- Date
> 메시지가 생성된 시각을 담고 있는 값입니다. 
> ex> Date: Tue, 15 Nov 1994 08:12:31 GMT

- Expect	
> 클라이언트에 의해서 요구되는 특정 서버의 행동을 명시한 값입니다.
> 	ex> Expect: 100-continue

- Forwarded	
> HTTP proxy 를 통한 웹 서버 연결을 할 때 클라이언트의 원래 정보를 드러내는 값입니다. 
> ex> Forwarded: for=192.0.2.60;proto=http;by=203.0.113.43 

- From 
> 요청을 만든 이의 이메일 주소입니다. 
> ex> From: user@example.com

- Host
> 서버가 listen하고 있는 도메인과 포트번호입니다. 
> ex> Host: en.wikipedia.org:8080

- If-Match
> 클라이언트의 엔티티가 서버의 엔티티가 일치될 때만 수행되기를 원할 때 설정하는 값입니다. 이 필드는 PUT과 같은 메서드에서 유저가 마지막으로 수정한 이후 수정되지 않았을 때만 업데이트가 수행되도록 할 수 있습니다.
> ex> If-Match: "737060cd8c284d8af7ad3082f209582d"

- If-Modified-Since
> 컨텐츠가 바뀌지 않았을 때만 304 Not Modified가 반환되는 것을 허락합니다.
> ex> If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT

- If-None-Match
> 컨텐츠가 바뀌지 않았을 때만 304 Not Modified가 반환되는 것을 허락합니다.
> ex> If-None-Match: "737060cd8c284d8af7ad3082f209582d"

- If-Range
> 만약 엔티티가 바뀌지 않았다면 내가 빠진 데이터의 부분을 보내도록 하는 엔티티값을 명시합니다.
> ex> If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT	

- If-Unmodified-Since
> 특정 시각 이후에 수정되지 않았다면 응답하로도록 명시할 수 있는 값이 담겨있습니다.
> ex> If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT

- Max-Forwards	
> 프록시나 게이트웨이에 의해 포워딩 되는 최대 횟수를 제한하는 값을 명시합니다.
> ex> Max-Forwards: 10

- Origin
> 서버에게 Access-Control-Allow-Origin response 필드가 있는지 물어봅니다.
> ex> Origin: http://www.example-social-network.com

- Pragma
> 요청 응답 과정에서 다양한 영향을 끼칠 수 있는 필드입니다.
> ex> Pragma: no-cache

- Proxy-Authorization
> 프록시 연결에 대한 자격을 명시합니다. 
> ex> Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

- Range
> entity의 일부만 요청합니다. 
> ex> Range: bytes=500-999

- Referer
>  현재 페이지로 요청되기 전에 뒤 따른 링크가 담겨있습니다.
> ex> Referer: http://en.wikipedia.org/wiki/Main_Page

- TE
> user agent가 받아들이고자 하는 인코딩에 대한 전달값입니다.
> ex> TE: trailers, deflate

- User-Agent
> user agent를 명시하는 값이 담겨있습니다.  
> ex> User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:12.0) Gecko/20100101 Firefox/21.0

- Upgrade
> 서버에게 다른 프로토콜로 업그레이드 할 것을 요청합니다. 
> ex> Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket

- Via
> 요청이 전송된 프록시 서버를 알립니다.
> ex> Via: 1.0 fred, 1.1 example.com (Apache/1.1)

- Warning
> 엔티티 바디 문제에 대한 가능한 일반적인 경고를 명시한 값입니다.
> ex> Warning: 199 Miscellaneous warning

`message body`
message body에는 전달하려는 추가 데이터가 담겨있습니다. GET에서는 Requset Line에 파라미터를 붙여서 데이터를 담지만 길이제한이나 보안적 이슈 때문에  POST에서는 길이 제한이 없는 message body에 추가됩니다.


----

##Response

`status line`
Status line은 응답의 첫 줄에 전달되는 데이터로 아래와 같은 형식으로 구성되어 있습니다.
> [HTTP 버전] [상태 코드] [Reason-Phrase]
> (예시) HTTP/1.1 200 OK

`response header`

- Access-Control-Allow-Origin
> cross-origin resource sharing 에 참여할 수 있는 웹사이트를 명시합니다.
> ex> Access-Control-Allow-Origin: *

- Accept-Patch
> 서버가 지원하는 문서 포멧을 명시합니다.
> ex> Accept-Patch: text/example;charset=utf-8

- Accept-Ranges
> 서버가 지원하는 컨텐츠의 범위 
> ex> Accept-Ranges: bytes

- Age
> 프록시 캐시가 존재하는 시간 (단위 초)를 명시한 값입니다.
> ex> Age: 12

- Allow
> 유효한 http 메서드에 대해 명시한 값입니다.
> ex> Allow: GET, HEAD

- Alt-Svc
> 받아열드질 수 있는 다른 네트워크 위치를 명시합니다.
> ex> Warning: 199 Miscellaneous warning

- Cache-Control
> 서버로 부터 클라이언트 사이의 모든 캐시 메커니즘을 명시합니다.
> ex> Cache-Control: max-age=3600

- Connection
> 현재 연결에 대한 컨트롤 옵션입니다.
> ex> Connection: close

- Content-Encoding
> 데이터에 사용된 인코딩 타입입니다.
> ex> Content-Encoding: gzip

- Content-Language
> 응답 받는 사용자의 언어입니다.
> ex> Content-Language: da

- Content-Length
> response body 의 길이 입니다.
> ex> Content-Range: bytes 21010-47021/47022

- Content-Location
> 반환 되는 데이터를 위한 위치 입니다.
> ex> Content-Range: bytes 21010-47021/47022

- Content-MD5
> 응답 콘텐츠의 인코딩 바이너리의 md5합 입니다.
> ex> Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

- Content-Range
> 전체 바디 메시지에서 특정 메시지가 속해 있는 위치입니다.
> ex> Content-Range: bytes 21010-47021/47022

- Content-Type
> 컨텐츠의 MIME 타입 입니다.
> ex> Content-Type: text/html; charset=utf-8

- Date
> 메시지가 보내진 날짜와 시간 입니다.
> ex> Date: Tue, 15 Nov 1994 08:12:31 GMT

- ETag
> 리소스의 특정 버전을 위한 id입니다.
> ex> ETag: "737060cd8c284d8af7ad3082f209582d"

- Expires
> 응답이 만료되는 시간입니다.
> ex> Expires: Thu, 01 Dec 1994 16:00:00 GMT

- Last-Modified
> 요청된 리소스가 마지막으로 수정된 시각
> ex> Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT

- Link
> 서버에서 클라이언트가 요청된 리소스에 대한 메타데이터를 포함하는 다른 데이터를 가리키는 것을 허락합니다.
> ex> Link: </feed>; rel="alternate"

- Location
> 리이렉션에서 사요되거나 새로운 리소스가 생성 되었을 때 사용합니다.
> ex> Location: http://www.w3.org/pub/WWW/People.html

- Proxy-Authenticate
> 프록시에 접근하기 위한 자격을 명시한 값입니다.
> ex> Proxy-Authenticate: Basic

- Public-Key-Pin
> 웹 클라이언트에게 특정한 공개키가 사용되었음을 알려줍니다.
> ex> Public-Key-Pins: max-age=2592000; pin-sha256="E9CZ9INDbd+2eRQozYqqbQ2yXLVKB9+xcprMF+44U1g=";

- Refresh
> 리다이렉션에서 사용되거나 새로운 리소스가 생성되었을 때 사용합니다. 5초후 리다리엑션 될 때 아래와 같이 명시합니다.
> ex> Refresh: 5; url=http://www.w3.org/pub/WWW/People.html

- Retry-After
> 엔티티가 일시적으로 사용불가능할 때 클라이언트가 나중에 시도하도록 지시합니다.
> ex> Retry-After: 120

- Server
> 서버의 이름입니다.
> ex> Server: Apache/2.4.1 (Unix)

- Set-Cookie
> 서버가 설정한 http 쿠키를 담습니다.
> ex> Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1

- Status
> http 응답 상태를 표시한 필드입니다.
> ex> Status: 200 OK

- Strict-Transport-Security
> HTTP 클라이언트가 얼마나 캐싱할 것인지와 이것을 서브도메인에도 적용할 것인가를 알려주는 정책 입니다.
> ex>Strict-Transport-Security: max-age=16070400; includeSubDomains

- Upgrade
> 클라이언트에게 다른 프로토콜로 업데이트하라는 요청을 명시한 값입니다.
> ex> Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket

- WWW-Authenticate
> 요청된 엔티티에 접속하는데 사용되어져야하는 인증 스키마 입니다.
> ex> WWW-Authenticate: Basic


- X-Frame-Options 
> 브라우저가 frame, iframe 또는 object에서 페이지를 렌더링하는 것을 허락할 건지에 대한 여부를 위해 사용된다.
> ex> X-Frame-Options: deny

##실제 요청

네이버에 GET요청해서 받은 응답 결과

HTTP/1.1 200 OK
Server: nginx
Date: Tue, 13 Sep 2016 06:50:28 GMT
Content-Type: text/html; charset=UTF-8
Transfer-Encoding: chunked
Connection: close
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
P3P: CP="CAO DSP CURa ADMa TAIa PSAa OUR LAW STP PHY ONL UNI PUR FIN COM NAV INT DEM STA PRE"
X-Frame-Options: SAMEORIGIN
Length: unspecified [text/html]