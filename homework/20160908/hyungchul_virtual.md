nginx/apache의 경우 Virtual Host 라는 기능이 제공됩니다. www.a.com, www.b.com 이 같은 ip이더라도 도메인만으로 다른 위치의 데이터를 전달할 수 있는 기능인데, HTTP header 중에 어떤 정보를 이용하여 구현되는지에 대해서 정리하세요.
=====

## (배경지식) Virtual Host(가상 호스트)란?

----

> 웹서버에 기본적으로 존재하는 호스트를 주호스트(main host)라고 한다. 하나의 웹서버에 main host이외에 별도의 홈디렉토리를 가진 여러개의 호스트를 설정하여 운용할 수 있다. 이는 주로 웹호스팅 서비스에 사용되고, main host이외의 호스트들을 가상 호스트라고 부른다. (가상호스트를 가장 적절하게 이용하는 것이 웹호스팅 서비스) 이런 웹호스팅 서비스를 위해서는 아파치 웹서버에서는 가상호스트로 설정하면 해결가능하다.

Web Server에는 기본적으로 존재하는 Host가 있으며, 이를 Main Host라고 한다.
하나의 Web Server에는 Main Host 외에 별도의 디렉토리를 가진 여러개의 Host를 설정하여 사용할수 있다.

  이 중 Main Host 외에 나머지 Host를 모두 Virtual Host라고하며, 
  이를 이용하여 하나의 컴퓨터에서 여러개의 Web Site(예를 들어 Embian1.com, Embian2.com)를 서비스할수 있다.
  Apache에서는 Name-based Virtual Host 와 IP-based Virtual Host 그리고 Post-based Host 세 가지 방식을 제공한다. 

  Name-based Virtual Host 

  일명 이름 기반의 가상호스트라고 한다. 이것은 하나의 IP Address당 여러 이름을 가지는 방식이며, 가장 보편적인 방법이다. 

  IP-based Virtual Host

  일명 IP Address 기반의 가상호스트라고 하며, 각 웹 사이트마다 다른 IP Address 또는 Port를 가지는 방식이다. 

  Post-based Virtual Host
IP Address를 다르게 하는 방법도 있지만, 동일한 Ip Address를 주고 Port를 다르게 하는 방법도 있다. 

-----

Google에 virtual host http header로 검색을 해보니 Name-based Virtual Host를 사용할 때 
request header에 HOST를 지정해주어야 한다고 나와서 Name-based Virtual Host에 대해서 조사하라는 것으로 파악했다.

----

Nginx에서의 Virtual Host를 알아보았다.

nginx 에게 request 가 오면, nginx 는 일단 http header 의 Host 부분을 확인한다.
거기서 이 request가 어느 domain (또는 IP) 로 가려고 하는지 확인하고, 그에 해당하는 virtual host 로 보낸다.

이 virtual host 에 해당하는 것이 nginx 의 configuration 에 설정하는 server 이다.
 
server {
    listen      80;
    server_name example.org www.example.org;
    ...
}

server {
    listen      80;
    server_name example.net www.example.net;
    ...
}

---

참고자료 

          http://i5on9i.blogspot.kr/2016/01/nginx-server.html

          http://blog.embian.com/46

---



