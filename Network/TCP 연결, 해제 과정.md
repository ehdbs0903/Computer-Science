## TCP 연결 성립 과정

TCP는 신뢰성을 확보할 때 '3-way handsahke' 라는 작업을 진행한다.

![image](https://github.com/ehdbs0903/Computer-Science/assets/82309982/67f4de97-b91f-4fba-8610-52be62024f94)
<br></br>

#### 1. SYN 단계

클라이언트는 서버에 클라이언트의 ISN(Initial Sequence Numbers)을 담아 SYN(Synchronization)을 보낸다. ISN은 새로운 TCP 연결의 첫 번째 패킷에 할당된 임의의 시퀀스 번호를 말하며 이는 장치마다 다를 수 있다.
<br></br>

#### 2. SYN + ACK 단계

서버는 클라이언트의 SYN을 수신하고 서버의 ISN을 보내며 승인번호로 클라이언트의 ISN + 1을 보낸다.
<br></br>

#### 3. ACK 단계

클라이언트는 서버의 ISN + 1한 값인 승인번호를 담아 ACK(Acknowledgement)를 서버에 보낸다.\
<br></br>

이렇게 '3-way handsahke'  과정 이후 신뢰성이 구축되고 데이터 전송을 시작한다. TCP는 이 과정이 있기 때문에 신뢰성이 있는 계층이라고 하며 UDP는 이 과정이 없기 때문에 신뢰성이 없는 계층이라고 한다.
<br></br>
<br></br>

## TCP 연결 해제 과정

TCP가 연결을 해체할 때는 4-way handshake 과정을 거친다.

![image](https://github.com/ehdbs0903/Computer-Science/assets/82309982/2aaaa4d1-c4e0-4d9b-af9c-1db5c535572c)
<br></br>

#### 1번

먼저 클라이언트가 연결을 닫으려고 할 때 FIN으로 설정된 세그먼트를 보낸다. 그리고 클라이언트는 FIN_WAIT_1 상태로 들어가고 서버의 응답을 기다린다.
<br></br>

#### 2번

서버는 클라이언트로 ACK라는 승인 세그먼트를 보낸다. 그리고 CLOSE_WAIT 상태에 들어간다. 클라이언트가 세그먼트를 받으면 FIN_WAIT_2 상태에 들어간다.
<br></br>

#### 3번

서버는 ACK를 보내고 일정 시간 이후에 클라이언트에 FIN이라는 세그먼트를 보낸다.
<br></br>
 
#### 4번

클라이언트는 TIME_WAIT 상태가 되고 다시 서버로 ACK를 보내서 서버는 CLOSED 상태가 된다. 이후 클라이언트는 어느 정도의 시간을 대기한 후 연결이 닫히고 클라리언트와 서버의 모든 자원의 연결이 해제된다.
<br></br>

이 과정에서 중요한 것은 TIME_WAIT이다. TIME_WAIT이 있는 이유는 두 가지가 있다.
<br></br>
#### 1. 지연 패킷이 발생할 경우를 대비하기 위해서

패킷이 늦게 도달하고 이를 처리하지 못한다면 데이터 무결성 문제가 발생한다.
<br></br>

#### 2. 두 장치가 연결이 닫혔는지 확인하기 위해서

만약 LAST_ACK 상태에서 닫히게 되면 다시 새로운 연결을 하려고 할 때 장치는 줄곧 LAST_ACK로 되어 있기 때문에 접속 오류가 나게 된다.
 
