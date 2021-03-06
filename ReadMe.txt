﻿=====================
C++ HTTP stack 라이브러리
=====================

1. 개요

 * C++ STL 라이브러리를 이용한 HTTP 클라이언트 및 서버 라이브러리 개발
 
2. 개발자 정보
  
 * 이영한
 * 이메일 : websearch@naver.com
 * 블로그 : http://blog.naver.com/websearch

3. 라이선스

 * 본 프로젝트의 라이선스는 GPLv3 이고 기업용 라이선스는 websearch@naver.com 으로 문의해 주세요.

4. 개발툴

 * 윈도우 : Visual C++ 2007
 * 리눅스 : g++

5. 폴더 설명

 * HttpParser
   - HTTP 프로토콜 파서/생성 라이브러리

 * HttpStack
   - HTTP 클라이언트/서버 라이브러리

 * SipPlatform
   - C++ SIP stack 에서 사용되는 OS 독립적인 유틸리티 라이브러리
   - https://github.com/YeeYoungHan/cppsipstack

 * TcpStack
   - TCP 클라이언트/서버 라이브러리
   - HttpStack 에서 HTTP 서버 개발에 사용된다.

6. HTTP GET 요청/응답 개발 방법

 HttpStack 라이브러리의 CHttpClient 클래스를 이용한 HTTP GET 프로토콜 연동하는 소스 코드 예제는 다음과 같습니다.
  - 테스트용 샘플 소스 코드는 TestHttpClient 프로젝트의 TestHttpClientGet.cpp 파일입니다.

 CHttpClient clsClient;
 std::string strBodyType, strBody;

 clsClient.DoGet( "http://www.naver.com", strBodyType, strBody );

7. HTTP POST 요청/응답 개발 방법

 HttpStack 라이브러리의 CHttpClient 클래스를 이용한 HTTP POST 프로토콜 연동하는 소스 코드 예제는 다음과 같습니다.
  - 테스트용 샘플 소스 코드는 TestHttpClient 프로젝트의 TestHttpClientPost.cpp 파일입니다.

 std::string strSendBody, strRecvBodyType, strRecvBody;
 CHttpClient clsClient;
 HTTP_HEADER_LIST clsHeaderList;
 CHttpHeader clsHeader( "SOAPAction", "http://www.webserviceX.NET/GetWeather" );

 strSendBody = "<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:web=\"http://www.webserviceX.NET\">"
   "<soapenv:Header/>"
   "<soapenv:Body>"
      "<web:GetWeather>"
         "<web:CityName>seoul</web:CityName>"
         "<web:CountryName>kr</web:CountryName>"
      "</web:GetWeather>"
   "</soapenv:Body>"
  "</soapenv:Envelope>";

  clsClient.DoPost( "http://www.webserviceX.NET/globalweather.asmx", &clsHeaderList, "text/xml;charset=UTF-8", strSendBody.c_str(), strRecvBodyType, strRecvBody );

8. HTTP SOAP 요청/응답 개발 방법

 HttpStack 라이브러리의 CHttpClient 클래스를 이용한 웹 서비스 연동하는 소스 코드 예제는 다음과 같습니다.
  - 테스트용 샘플 소스 코드는 TestHttpClient 프로젝트의 TestHttpClientSoap.cpp 파일입니다.

 std::string strSendBody, strRecvBody;
 CHttpClient clsClient;

 strSendBody = "<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:web=\"http://www.webserviceX.NET\">"
   "<soapenv:Header/>"
   "<soapenv:Body>"
      "<web:GetWeather>"
         "<web:CityName>seoul</web:CityName>"
         "<web:CountryName>kr</web:CountryName>"
      "</web:GetWeather>"
   "</soapenv:Body>"
  "</soapenv:Envelope>";

 clsClient.DoSoap( "http://www.webserviceX.NET/globalweather.asmx", "http://www.webserviceX.NET/GetWeather", strSendBody.c_str(), strRecvBody );

9. 초간단 HTTP 서버 개발 방법

 초간단 HTTP 서버 개발 소스 코드 예제는 TestHttpStack 프로젝트에 있습니다. TestHttpStack 프로젝트 소스 코드를 참고하시면 CHttpStack 을 이용하여서 어떻게 HTTP 서버를 개발할 수 있을지 확인하실 수 있습니다.