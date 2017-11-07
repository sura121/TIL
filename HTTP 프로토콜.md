## HTTP 구조

**API 공부를 하기위해 기초부터 알고싶어 찾아보게 되었습니다.**

Request Line

- 요청시 맨처음 첫줄이며 세개의 빌드가 존재합니다. Method sp URL sp Version CL/RF 
	Method 는 일종의 동사 같은것이며 요청 유형(Request Type)을 정의 해두고 있습니다.
Status Line

- 요청에 대한 응답 메시지의 첫줄입니다. 필드는 마찬가지로 3개입니다.
	Version sp Code sp Phrase CL/RF
- code는 요청에 대한 응답코드입니다.
- Phrase는 응답코드에 대해 지정된 문구입니다. 

Request header

- 헤더는 요청이든 응다이든 2개의 필드를 가집니다. 
   헤더이름 : sp 값 CR/LF

- Proxy-Connection

  Connection 필드와 같은 기능을 합니다. proxy-connection은 실험용이자 완전한 표준이 아닙니다. 요청시에 이필드는 연결 유형을 정의하는 필드인데 keep-alive는 한개의 TCP연결로 다수의 요청과 응답을 처리하기 위한것입니다. Close일떄는 요청후 바로 연결을 종료하는것이며 keep-alive은 연결을 유지하는것을 나타냅니다.

- Content-length

body의 데이터 크기를 바이트단위로 나타냅니다. GET방식이면 이 필드는 필요없겠죠. 이 필드를 통해 파일업로드 같은 로직에서 제데로 업로드 됬는지등의 유효성을 검증할수있습니다. 동적으로 바디가 생성되어 요청 된다면 Transfer-Encoding: chunked 필드를 보내어 바디 사이즈를 생략할수 있습니다.

- Origin

CORS(Cross-Origin Resource Sharing)의 기능을 사용하기위해 사용됩니다. CORS는 다른 도메인의 요청을 받을수있기위해 사용됩니다.

- User-Agent

요청하는 클라이언트의 정보입니다. 우리가 모바일을 통해 다음에 접속하면 자동으로 모바일페이지로 포워딩됩니다. 이 로직에 사용되는 필드가 바로 User-Agent입니다. 

- Content-Type

말그대로 요청할때 바디영역의 컨텐츠 타입입니다. 이는 MIME 형식을 따르며 application/x-www-form-urlencoded 형태는 key-value 형태인 쿼리스트링 형태의 데이터형식을 말하며 form의 기본 MIME입니다. 파일 전송같은경우 multipart/form-data를 주로 사용합니다. 참고로 Content-Type 필드는 charset라는 값이 추가로 허용됩니다. 이를 통해 우리는 euckr, utf-8 등의 인코딩을 이용 할수있는것입니다. euckr 따위 집어 치우고 Content-Type: text/html; charset=utf-8 쓰세요 

- Accept

응답에 허용되는 컨텐츠 타입을 말합니다. 보통 Accept-Language와 같이 Content negotiation이라 합니다. 또한 status code 중 406 Not acceptable 과 관련이있습니다.

- Referer

현재 요청 URL 바로전의 web page 주소를 나타냅니다.

- Cookie

대망의 쿠키입니다. 쿠키는 보다시피 헤더정보에 포함되어 전송되는 클라이언트의 데이터입니다. 자바스크립트를 통해 접근할수있으며 흔히 http session, php 세션, jsp 세션 이라함은 이 쿠키를 통해 이루어집니다. 헤더에 포함되어 서버에 전송되는 것 때문에 가능한 일이죠. 또한 쿠키는 자동로그인, 이 광고 오늘 그만보기, 장바구니 등에 쓰입니다. 위 사진에선 TSSESSION 필드에 있는 값이 세션인거 같습니다. 참고로 쿠키를 통해서 세션을 구현하여 상태를 지원하지 않는 http 프로토콜을 일련번호를 쿠키에 저장하여 웹서버 나 WAS에서 로그인등의 기능을 구현하게 됩니다.


