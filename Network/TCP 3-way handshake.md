## TCP 3-way handshake

![image-20210127151420170](C:\Users\Hijin\AppData\Roaming\Typora\typora-user-images\image-20210127151420170.png)

### Three way handshake

1. 클라이언트는 TCP SYN 세그먼트를 서버에 보냄
   * 초기 클라이언트 순서번호 명시
   * 데이터 불포함
2. 서버는 SYN를 수신하고 SYNACK 세그먼트로 응답
   * 서버는 버퍼를 할당, 초기 순서번호 규정
3. 클라이언트는 SYNACK를 수신하고 ACK로 응답
   * 데이터를 포함할 수 있음



### Closing a connection

1. 클라이언트는 TCP FIN을 서버로 보냄
2. 서버는 FIN을 수신하고 ACK로 응답, FIN을 전송하고 연결 종료 상태 진입
3. 클라이언트는 FIN 수신하고 ACK로 응답
   * timed wait 후 종료 (client의 ACK가 손실될 수 있기 때문에, 바로 종료할 경우 server가 보내는 데이터를 수신할 수 없음)
4. 서버는 ACK 수신하고 연결 종료