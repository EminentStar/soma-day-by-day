클라이언트에서 nginx/apache 등의 웹 서버에 데이터를 보낼때, Request 와 Response 측면에서 어떤 데이터들이 전달되는지 정리하시오. GET 형식과 POST 형식으로 보낼 때, HTTP-Header 들과 실제 데이터가 어떤식으로 전달되는지 샘플과 각각의 설명을 달아주세요.
=
----

HTTP request 구조는 다음과 같다 
Request       = Request-Line             
                        *(( general-header       
                         | request-header        
                         | entity-header ) CRLF)  
                        CRLF
                        [ message-body ]        


----

HTTP Request는 크게 세 가지 부분으로 이루어져있다.

첫 번째 라인에는 HTTP METHOD와 사용자가 질의한 파일이나 자원을 표시하는 URI, 그리고 HTTP 버전 번호로 이루어진다.
두 번째 부분은 사용자와 서버에서 보내는 데이터에 대한 정보를 제공하는 헤더 정보가 포함되고,
세 번째 부분은 사용자 요청으로 서버에게 보내는 데이터인 ENTITY의 몸체이다.  

## Request-Line = Method SP Request-URI HTTP-Version CRLF

----

Method
리소스에 어떤 일을 행할지 나타내는 역할을 하는 것이 Method이다. 

Method의 종류에는 다음과 같은 것들이 있다.
Method         = "OPTIONS"                
                      | "GET"                    
                      | "HEAD"                   
                      | "POST"                   
                      | "PUT"                   
                      | "DELETE"                
                      | "TRACE"                  
                      | "CONNECT"               
                    

GET : 정보를 요청하기 위해서 사용한다. (SELECT)
POST : 정보를 밀어 넣기 위해서 사용한다. (INSERT)
PUT : 정보를 업데이트하기 위해서 사용한다. (UPDATE)
DELETE : 정보를 삭제하기 위해서 사용한다. (DELETE)
HEAD : (HTTP)헤더 정보만 요청한다. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인하기 위해서 사용한다.
OPTIONS : 웹서버가 지원하는 메서드의 종류를 요청한다.
TRACE : 클라이언트의 요청을 그대로 반환한다. 예컨데 echo 서비스로 서버 상태를 확인하기 위한 목적으로 주로 사용한다.
CONNECT: 프록시가 사용하는 요청이다.

----

URI는 Uniform Resource Identifier의 약자이다. 요청을 적용할 자원을 식별한다.
Request-URI의 구조는 다음과 같다.
Request-URI    = "*" | absoluteURI | abs_path | authority

URI에 대한 네 가지 옵션은 요청의 성격에 따라 달라진다. 

별표 “*”는  요청이 있지만 서버의 특정 자원에 적용되지 않는다. 사용 방법은 반드시 자원에 적용되지 않는 경우에만 허용한다. 
Request-URI가 *인 예시이다. 
OPTIONS * HTTP/1.1

요청이 프록시로 이루어져 있을 때 absoluteURI가 요구된다.
프록시는 요청을 전달하거나 올바른 캐시를 서비스하고 응답을 반환하도록 요청한다.
프록시가 다른 프록시 또는 직접 서버에 요청을 전달할 수도 있다. 

absoluteURI의 예시이다.
GET http://www.w3.org/pub/WWW/TheProject.html HTTP/1.1

Authority는 CONNECT method에서만 사용되는 형식이다. 

Request-URI의 가장 일반적인 형태는 Origin server 또는 gaterway의 리소스를 식별하는데 있다. 

----

request-header filed는 다음과 같은 구조로 이루어져 있다.
request-header = Accept                   
                      | Accept-Charset          
                      | Accept-Encoding          
                      | Accept-Language      
                      | Authorization            
                      | Expect               
                      | From                    
                      | Host                     
                      | If-Match                
                      | If-Modified-Since     
                      | If-None-Match          
                      | If-Range                 
                      | If-Unmodified-Since     
                      | Max-Forwards            
                      | Proxy-Authorization     
                      | Range                   
                      | Referer                  
                      | TE                       
                      | User-Agent               


----

다음은 전형적인 HTTP request 내용이다.

GET /books/search.asp HTTP/1.1
Accept: image/gif, image/xxbitmap, image/jpeg, image/pjpeg,
application/xshockwaveflash, application/vnd.msexcel,
application/vnd.mspowerpoint, application/msword, */*
Referer: http://wahh-app.com/books/default.asp
Accept-Language: en-gb,en-us;q=0.5
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)
Host: wahh-app.com
Cookie: lang=en; JSESSIONID=0000tI8rk7joMx44S2Uu85nSWc_:vsnlc502

GET /books/search.asp HTTP/1.1
- GET메소드를 이용하여 search.asp라는 문서를 요청하며, 이 때 HTTP1.1버전을 사용한다.

User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)
  Accept: image/gif, image/xxbitmap, image/jpeg, image/pjpeg,
- 클라이언트는 서버에게 옵션헤더 정보를 보내 자신이 설정한 내용과 받아들일 문서의 형식을 알린다. 모든 헤더 정보는 각 헤더 이름과 값을 가즌 행별로 주어진다. 그리고 사용자는 헤더의 끝을 알리기 위해 공백행을 보낸다.

----

HTTP request header에 대한 설명이다.

Accept:  type/subtype [; q=qvalue]

 클라이언트가 우선적으로 받아들이는 미디어 형을 명시한다.
 여러 개의 미디어 형을 쉼표로 구분해서 나열할 수있다. 
 옵션인 qbalue는 받는 형태의 수준 순서로써 0 에서 1까지 나타낸다.

Accept-Charaset

 Accept-Charset: character_set [;q=qvalue]

 클라이언트가 우선하는 문자 세트를 지정한다.
 여러 개의 문자 세트는 쉼표로 구분하여 나열한다.
 옵션인 qvalue는 우선하지 않는 문자 세트의 수준 순서로 0 에서 1까지 나타낸다.


Accept-Encoding

 Accept-Encoding:  endoding_types

 compress 또는 gzip과 같은 클라이언트가 받아들일 수 있는 인코딩 방식을 지정한다. 
여러 개의 인코딩 방식을 쉼표로 구분하여 나열한다. 
만약 인코딩 형태를 지정하지 않으면 어떤 형태도 클라이언트에게 받아들여지지 않는다.


Accept-Language

Accept-Language: language [; q=qvalue]

 클라이언트가 우선적으로 지원하는 언어를 지정한다. 
쉼표로 구분해서 여러 개의 언어를 지정할 수 있다. 
옵션인 qvalue는 우선하지 않는 언어 순서로 0에서 1까지로 나타낸다.
 언어는 두문자로 축약해서 쓴다.(예)en, fr, kr 등


Authorization

Authorization: scheme credentials

 URI에 클라이언트가 데이터에 접근할 수 있는 권한을 제공한다.
 요청된 문서가 권한을 요구하면 서버는 요구된 권한의 유형을 설명하는 WWW-Authenticate헤더를 반환한다. 
 그리고 나서 클라이언트는 적당한 권한 정보를 요청할 때마다 이것을 반복한다.

 HTTP에 일반적으로 사용된 권한 계획은 BASIC이며, BASIC방식에서는 권한을 인증하기 위해 base64로 인코딩된 username:password 형태를 따른다.
 예를 들면, 사용 자명이 ‘webmaster’ 이고 패스워드가‘zrma4v’라면 authorization 헤더는 이것을 다음과 같이 보이게 한다.

Authorization: BASIC d2VibWFzdGVyOnpycW1hNHY=

이것의 디코딩 값은 webmaster : zrma4v이다


Cookie

Cookie: name=value

 URL을 위해 저장된 정보의 이름=값을 포함한다. 여러 개의 쿠키는 세미콜론으로 구분하여 나열된다. 넷스키이프도 쿠키를 지원한다. HTTP표준에는 포함되어 있지 않다.


From

From: email_address

 현재 사용하고 있는 클라이언트의 전자 우편 주소를 반환한다.


Host

Host: hostname[:port]

 호스트의 이름과 URI의 port번호를 지정한다.
 클라이언트는 HTTP1.1에 반드시 이정보를 공급해야 하는데
 이것은 여러 개의 호스트명이 갖는 애매한 URL을 쉽게 구별하는 데 도움이 된다.


If-Modified-Since

If-Modified-Since: date

 헤더의 값으로 주어진 날짜 이후 수정이 되었다면 URI데이터를 보낸다는 것을 명시한다. 
 이것은 클라이언트 측 캐시에 대해 유용하다.
 만약 문서가 수정되지 않았다면 서버는 304코드를 반환하여 클라이언트에게 로컬에 있는 사본을 보여준다.
 단 지정한 날짜는 Date헤더 아래에 설명된 형식을 따라야 한다.


If-Match

If-Match: entity_tag

 조건적으로 요청하는 것으로 주어진 ENTITY태그와 매치된다.
 *기호는 어떠한 ENTITY와도 매치되며, ENTITY가 존재해야만 트랜잭션이 계속된다.


If-None-Match

If-None-Match: entity_tag

조건적으로 요청하는 것으로 주어진 엔티티 태그와 어떠한 것도 매치되지 않는다.

*기호는 어떠한 엔티티와도 매치되며 엔티티가 존재하지 않아야만 트랜잭션이 계속된다.


If-Range

If-Range: entity_tag | date

 조건적으로 요청하는 것으로 실체의 일부가 변하지 않았는데 찾을 수 없고, 그것이 실체의 전부를 나타낸다.
 Range헤더와 함께 사용되어야 한다. ENTITY 태그나 날짜 둘 중 하나는 이미 주어진 실체의 일부분을 식별할 수 있다.


If-Unmodified-Since

If-Unmodified-Since: date

 주어진 날짜 이후로 수정되지 않았다면 URI데이터를 보내도록 지정한다. 지정한 날짜는 Date헤더 아래에 설명된 형식을 따라야 한다.


Max-Forwards

Max-Forwards: n

 요청을 전달한 프록시나 게이트 웨이의 개수를 제한한다.
 TRACE 메소드와 함께 사용하여 디버깅에 유용하며, 무한 루프를 피할 수 있다.


Proxy-Authorization

Proxy-Authorization: credentials

 클라이언트가 권한을 요구하는 프록시에 대해 자신을 식별하기 위해 사용한다.


Range

Range: bytes= n-m

 문서가 요구하는 부분적인 범위를 명시한다. 여러 개의 범위는 세미콜론으로 구분하여 나열한다.
 만약 쉼표로 구별된 바이트 범위인 첫번째 숫자가 없다면 범위는 문서의 끝에서부터 없어진다고 가정한다.
 만일 두번째 숫자가 없다면 범위는 끝에서 n바이트까지이다. 첫번째 바이트는 0바이트이다.


Referer

Referer: url

 요청된 URI를 참조하는 문서의 URI에 전달한다.


User-Agent

User-Agent: string

클라이언트 프로그램에 대한 식별 가능한 정보를 준다.

----

HTTP Response

다음은 전형적인 HTTP Respose 내용이다.

HTTP/1.1 200 OK

Date: Sat, 19 May 2007 13:49:37 GMT

Server: IBM_HTTP_SERVER/1.3.26.2 Apache/1.3.26 (Unix)

Set-Cookie: tracking=tI8rk7joMx44S2Uu85nSWc

Pragma: no-cache

Expires: Thu, 01 Jan 1970 00:00:00 GMT

Content-Type: text/html;charset=ISO-8859-1

Content-Language: en-US

Content-Length: 24246

(                                공백행                                    )


HTTP/1.1 200 OK

서버는 HTTP버젼, 상태코드, 설명으로 응답을 한다. 
HTTP버전은 서버가 응답하기 위해 사용하는 HTTP의 버전을 나타내며,
상태코드는 사용자가 요청한 서버의 결과를 나타내는 세자리 숫자이다.
설명은 우리들이 이해할 수 있는 텍스트로 되어있다.

 위의 내용의 서버가 사용자의 요청에 HTTP 1.1버전을 사용했다는 것을 나타내고
 200이란 상태 코드는 사용자의 요청이 성공적으로 됐다는 것을 의미한다. OK는 200에 대한 우리들이 이해할 수 있는 텍스트이다.


공백행은 헤더의 끝을 나타낸다.


----

서버 응답 헤더


Accept-Ranges

Accept-Ranges: bytes|none

 URI를 위한 요청 범위의 승인을 나타내며 또는 받아들인 요청의 범위가 없을 경우 none을 지정한다. 범위의 단위는 byte이다.


Age

Age: seconds

seconds에 문서의 나이를 지시한다.


Proxy-Authenticate

Proxy-Authenticate: scheme realm

 확인 계획과 이URI와 그 현재의 연결에 대해 프록시에 대한 적용할 수 있는 매개변수를 나타낸다. 응답으로 407을 사용한다.


Retry-After

Retry-After: dateseconds

응답코드 5 0 3(Service Uncavailable)과 함께 사용된다. 정수나GMT 날짜와 시간(D a t e헤더 형태를 설명)둘 중 하나를 포함한다. 만일 값이 정수이면 seconds의 숫자로 해석하여 요청이 발생한 후 지정한 seconds만큼 기다린다.

예) Retry-After: 3500

Retry-After: Fri, 17 May 1999 12:24:17 GMT


Server

Server: string

서버의 이름과 버전 번호를 포함한다.

예) Server: NCSA/1.3


Set-Cookie

Set-Cookie: name=value [; option ]

U R L을 위해 보유한 정보의 이름/값 쌍을 포함한다. 넷스케이프 쿠키를 지원하기 위

한 것으로 HTTP 표준에는 포함되어 있지 않다.

옵션의 예)

expires=date

지정된 날짜가 지나면 쿠키가 유효하지 않게 된다.

path=pathname

쿠키가 유효한URL 범위

domain=domain_name

쿠키가 유효한 도메인명의 범위

secure

보안이 적용된 연결에서만 쿠키를 반환한다.


Vary

Vary: *| headers

엔티티가 다중 자원을 가지고 있으므로 요청한 헤더를 지정한 목록이 상황에 따라 변할 수 있다는것을 지정한다. 여러 개의 헤더는 세미콜론으로 구분하여 나열한다.

*기호는 요청한 헤더가 반환되는 문서에 영향을 미칠 수도 있는 다른 요인을 의미 한다.


Warning

Warning: code host [ :port] string

 프록시 캐싱에서 사용하기 위한 상태 코드의 추가 정보를 나타낸다. host필드는 이름 또는 서버 호스트의 익명을 포함하며, 선택적으로 포트 번호를 포함한다. 두 자리 경고 코드와 그것을 설명하는 문자열은 다음과 같다.

10 Response is stale

응답 데이터는 오래된 것으로 알려져 있다.

11 Revalidation failed

응답 데이터는 오래된 것으로 알려져 있으며 그 이유는 프록시가 데이터를 재검증하는 데 실패했기 때문이다.

12 Disconnected operation

캐시가 네트워크로부터 연결되지 않았다.

13 Heuristic expiration

데이터는2 4시간 이상 된 것이며, 캐시는2 4시간 보다 더 이전에 만들어진 것을 사용한다.

14 Transformation applied

프록시는Content-Encoding이나 Content-Type 헤더에 명시한 대로 인코딩이나 문서의 미디어 형을 변경시켰다.

99 Miscellaneous warning

임의의 정보가 클라이언트에게 접속되거나 나타났다.


WWW-Authenticate

WWW-Authenticate: scheme realm

 401(Unauthorized) 응답 코드와 함께 사용된다. 요청된 URI에서 클라이언트로부터 요청된 권한의 범위와 권한의 계획을 명시한다. 많은 다른 권한 범위는 서버에 존재한다. 일반적인 권한 계획은 BASIC이며 사용자명과 패스워드를 요구한다.

예) WWW-Authenticate: BASIC realm="admin"



ENTITY Header

Allow

Allow: methods

지정한 URI에서 허락하는 메소드를 쉼표로 구분된 목록을 포함한다. 요청된 정보에 유용한 메소드들을 클라이언트에게 알리는 코드 405(Method Not Allow)를 서버 응답에 사용한다.


Content-Encoding

Content-Encoding: encoding_schemes

엔티티 몸체를 전송할 때 사용할 인코딩 체계(scheme)를 지정한다. 값으로는gzip(또는 x-gzip)과 compress(또는 x-compress)를 사용할 수 있다. 만약 여러 개의 인코딩 체계(쉼표로 구별한 목록 안에)가 지정되어 있다면 소스 데이터에 적용한 명령을 나열해야 한다.


Content-Language

Content-Language: languages

전송될 엔티티 몸체에서 의도하는 언어를 지정한다. 언어는 두 자리 숫자 코드로 나타낸다.(예, en, kr 등)


Content-Length

Content-Length: n

이 헤더는 전송된 엔티티 몸체가 가진 데이터의 길이(byte 단위로)를 지정한다. 어떤요청은 동적인 성질을 가질 수 있기 때문에 컨텐츠의 길이를 알 수 없을 경우도 있고, 이 경우에는 이 헤더를 제거한다.


Content-Location

Content-Location: uri

엔티티에 대한 URI를 제공한다. 이 경우 문서가 독립적으로 접근 가능한 위치에 다중 엔티티를 갖고 있을 수 있다. U R I는 절대 혹은 상대 경로로 지정할 수 있다.


Content-MD5

Content-MD5: digest

인수한 메시지의 완전성을 검사하기 위해 엔티티의 MD5 다이제스트를 제공한다.


Content-Range

Content-Range: bytes n-m/length

수반하는 엔티티 몸체 일부에 삽입되며, 전체 엔티티 몸체의 크기를 지정한다.

예)Content-Range: bytes 6143-7166/15339


Content-Transfer-Encoding

Content-Transfer-Encoding: scheme

네트워크에 전달되는 엔티티 몸체에 적용되는 어떤 변화를 지정한다. 일반적인 값으로는 7bit, 8bit, binary, base64, 그리고 quoted-printable이 있다.


Content-Type

Content-Type: type/subtype

엔티티 몸체의 미디어 형과 부미디어 형을 설명한다. 이는 같은 값을 클라이언트의Accept 헤더로 사용하며, 서버는 그 클라이언트가 우선적으로 지원하는 포맷 양식에 따르는 미디어 형을 반환해야 한다.


ETag

ETag: entity_tag

If-Match와 If-None-Match 요청 헤더를 위한 태그를 정의한다.


Expires

Expires: date

문서가 변경될 수도 있을 때의 시간 또는 그것의 정보가 유효하지 않을 때의 시간을명시한다. 그 시간 이후, 문서는 변경 또는 삭제되거나 그렇지 않을 수 있다. 값은 Date 헤더에서 설명한 것과 같은 유효한 형태의 날짜와 시간이다.


Last-Modified

Last-Modified: date

지정한 URI가 마지막으로 변경된 때를 명시한다. 값은Date 헤더에 설명한 것과 같은 유효한 형태의 날짜와 시간이다.


Location

Location: uri

문서의 새로운 위치를 지정한다. 일반적으로 응답 코드 201(Created), 301(MovedPerm anently), 또는302(Moved Temporarily)와 함께 사용된다. 주어진URI는 절대 주소로 지정해야 한다.


쿠키

항구적인 상태에 있는 클라이언트측 쿠키는 넷스케이프 네비게이터에서 소개한 것으로, 서버가 클라이언트의 장치에서 클라이언트가 지정한 정보를 저장할 수 있게 하기 위한 것이다. 서버는 클라이언트에 의해 다시 특정한 페이지나 서버에 접근할 때 그 정보를 이용할 수 있다. 쿠키 작동 형태는 서버가 각 클라이언트에 보내는 페이지를 개별화할 수 있도록 해주거나 사이트의 다양한 페이지들을 브라우징할 때 클라이언트가 선택했던 것들을 기억할 수 있게 해준다. 따라서 서버측에서 복잡한 CGI나 데이터베이스 시스템을 사용하지 않아도 된다.

쿠키는 다음과 같은 방법으로 작동한다. CGI 프로그램은 새로운 사용자를 식별할 때,서버가 클라이언트의 입력에서 조금씩 모아둔 정보와 그 사용자에 대한 식별자를 포함에 부가 헤더를 추가한다. 이 헤더는 클라이언트의 쿠키 파일에 사용자의 쿠키정보를 추가하라고 쿠키를 사용할 수 있는 브라우저에 알린다. 그러면, 웹 브라우저 URL의 모든 요청은 기타 헤더의 요청에 그 쿠키 정보를 포함시킬 것이며, CGI 프로그램은 특정한 사용자에게 맞추어진 문서를 보여줄 때 이 정보를 사용한다.

쿠키는 클라이언트의 하드 드라이브에 저장되므로 정보는 웹 브라우저가 닫히고 다시 열어도 남아 있다.


Set-Cookie 응답 헤더

사용자가 처음으로 사이트나 페이지를 방문하면 쿠키가 생성된다. CGI 프로그램은 사용자 요청을 받으면 이전의 쿠키 정보를 검색한다. 만약 쿠키가 없다면 Set-Cookie 헤더를 포함하는 응답을 보낸다. 이 헤더에는 클라이언트에 대해 유지하고자 하는 정보를 담고 있는 이름/값 으로 포함되어 있다. 헤더에 다른 선택 필드들도 포함시킬 수 있다.

Set-Cookie 헤더는 다음과 같은 구문을 사용한다.

Set-Cookie: name=value; expires=date;

path=pathname; domain=domain-name; secure

여러 개의 Set-Cookie 헤더는 서버 응답에 포함될 수 있다. ‘이름=값’으로 이루어진쌍은 이 헤더에 요구되는 유일한 속성이며, 처음에 와야 한다. 그 다음 속성들은 순서 없이 사용할 수 있고 다음과 같이 정의한다.

name=value

이름과 값 모두에 세미콜론, 공백(space), 또는 탭(tab)을 포함하지 않는 문자열을 지정한다. 스크립트를 다룰 준비가 되는 한, 실체가 그 이름이나 값에서URL 인코딩과 같은 인코딩을 요구한다면 사용할 수 있다.

expires=date

이 속성으로 쿠키의 유효 기간이 끝나는 날짜를 설정한다. 날짜의 형식은 표준적인 방법을 따르지 않고 다음과 같이 지정한다.

Wednesday, 01-Sep-96 00:00:00 GMT

이 날짜가 지나면 쿠키의 유효성이 만료하여 웹 브라우저가 더 이상 쿠키를 보내지 않는다. 만료일 표시에는 G M T(Greenwich Mean Time)만 사용된다. 만료일을 지정하지 않으면 쿠키는 현재 세션에서만 사용된다.

path=pathname

path 속성은 쿠키가 유효한 URL의 범위를 제공한다. 예를 들어, 경로명을/ pub라고 설정하면 /pub에 있는 /pub/docs나 /pub/images와 같은 하위 수준의 URL에도 쿠키를 보낸다. ‘/’의 pathname을 나타낸다면 쿠키가 지원하는 사이트의 모든 URL에 쿠키를 사용할 것이라는 뜻이다. path 속성이 없다면 쿠키는 URL에 지원하는 곳에서만 유효하다는 것을 뜻한다.

domain=domain-name

이 속성은 쿠키가 반환되는 범위의 도메인 이름을 지정한 것이다. domain-name에는 적어도 두 개의 점(.)이 포함되어 있어야 한다. 예를 들면,  .naver.com이라는 값은 www.naver.com와 cafe.naver.com, 그리고 기타 다른 naver.com 도메인을 갖는 서버 전체를 포괄한다.

secure

이 속성은 보안이 되는 연결(SHTTP와 SSL을 통한)에서만 쿠키를 반환한다는 것을 뜻한다. 이 속성이 없으면 쿠키는 연결에 상관없이 항상 반환된다.



쿠키 요청 헤더

웹 브라우저는 매번 웹 페이지로 가서 U R L을 위해 저장된 쿠키에 대한 쿠키 파일이있는지 검사한다. 파일이 있으면 웹 브라우저는 요청에 쿠키의‘이름=값’쌍을 포함하는 Cookie 헤더를 포함시킨다.

Cookie: name1=value1;name2=value2;…

쿠키 파일 안에 반환된 쿠키가 여러 개의 항목으로 구성되어 있다면, 경로명 범위와도메인의 범위로 구성한다. 다음 헤더에 같은 사이트에 대해 두 개의 쿠키가 설정되어 있는 예이다.

Set-Cookie: AbcBook=book; path=/

Set-Cookie: AbcBook=Bitems; path=/books

브라우저가 /books 경로에 있는 사이트의 한 페이지를 요청하면, 그것을 반환한다.

Cookie: AbcBook=Bitems; AbcBook=Bitems

양쪽 항목이 같은 이름을 공유하지만, 그것은 별개의 쿠키이며, 양쪽 다 /books 같은 특정한 URL에 적용된다. 쿠키가 반환될 때, 웹 브라우저는 매치 여부를 따져 가장 정확한 경로명이나 도메인을 먼저 반환한다.

Cookie 헤더를 만나면 많은 서버들은 HTTP_COOKIE 환경 변수를 사용하는CGI 프로

그램으로 헤더의 값을 전달한다.

 또한 쿠키들의 개수와 크기에 대한 제약이 있다.

- 클라이언트는 합쳐서 적어도 3 0 0개의 쿠키를 지원할 수 있어야 한다. 서버는 사

용자가 더 이상 저장하는 것을 기대해서는 안 된다.

- 각 쿠키(이름과 값을 조합해서)의 크기는4 K B를 넘어서는 안 된다.

- 각각의 서버 또는 도메인은 최대 2 0개의 쿠키를 지원한다. 이 제약 사항은 각기 지정한 서버 또는 도메인에 적용되므로 www.naver.com에서 20개를 저장할 수 있고 cafe.naver.com에서도 20개가 가능하며, 쿠키들의 이름 전체를 각기 명시 할 수 있다.


하지만 문제는 헤더와 관련된 프록시 서버에서 일어난다. 페이지가 캐시되거나 수정되지 않았을지라도, Set-Cookie와 Cookie 헤더 모두는 프록시를 통해 전파되어야 한다(If-Modified-Since 조건에 따라서). 또한 Set-Cookie 헤더는 프록시에 의해 결코 캐시 되어서는 안 된다.

---

