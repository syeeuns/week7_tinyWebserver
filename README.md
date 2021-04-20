# week7_tinyWebserver
클라이언트의 request를 받고, response를 내어주는 나만의 웹서버를 만들어보는 과제입니다.
- 기간 : 7일<br>
<br>

## 개념

1. 서버와 클라이언트의 통신

    서버쪽

    - socket() : 연결 통로 준비
    - bind() : 특정IP와 연결
    - listen() : 연결 후 요청을 기다리기
    - accept() : read/write 또는 receive/send 메소드를 짝으로 사용하여 요청/응답 처리. 단, listen()에서의 스레드와 다른 스레드를 만들어 진행한다.
    → 스레드 분리 이유: 서버는 여러 요청을 받아야 하기에, listen() 스레드는(母) 놔두고 계속 기다리게 하고, accept() 스레드는 (子) 요청을 처리하도록 만들어 둠
    → 단, 우리 과제에서는 멀티프로세싱까지 다루지는 않음

    클라이언트

    - socket() : 연결 통로 준비
    - connect() : 연결. 끝. 스레드 분리하지 않음
    <br>
2. HTTP / TCP / IP 통신 등
    - IP 위에 → TCP 위에 → HTTP 가 있음. 모두 P. 즉 protocol. 규약=약속

        → Pysical 레이어에 가까울 수록 밑에 있다고 표현

    - IP단으로 갈 수록 하드웨어 환경(와이파이, LTE, 랜선, ...) 레이어를 나눠서 설계하는 이유는, 각 단계 별 환경이 변할 수 있고, 다양한 이종의 장치들이 나올 수 있기 때문

        → 한번에 설계하면 다 바꿔야 하니까, 레이어를 나눠서 약속을 정해둔 것

    - TCP는 패킷 받는 게 보장됨 vs UDP는 패킷 받는 게 보장 안됨

        → 동영상 스트리밍에 UDP 많이 씀 (중간에 화질 저하돼도 보는 데 문제 없으니까)

        → 참고로 11장은 TCP 소켓으로 만들어지게 되어있음. 2kb를 주면 2kb를 받는 구조.

