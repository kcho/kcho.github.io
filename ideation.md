

라디오+인터넷
--------------------
### 개요
- mp3 + 인터넷
- 광고 안나오는 라디오를 구현해 보자
- 방송 편송표와 같이 라이도 편성표도 표시
- 방금그곡api 리스트 목록으로 플레이 리스트 표시
- 모양은 아이리버 mp3 같이 생겼음

투명핸드폰
------------

### 개요
- 후방 카메라 영상을 핸드폰 화면에 보여주여 투명한 효과를 낸다.
- 화면뷰를 통해 뒤면이 보이게 해줌.
- 투명한것 처럼 보이게 뷰 조절, 크기 조절이 관건.
- 핸드폰마다 후방 카메라 위치가 다르고, 카메라 스펙이 다른게 문제.
- 많이 쓰는 핸드폰 모델을 기준으로 만들어 보자.
- 확산되는 앱

확산되는 앱
------------

### 개요
많이 설치되는 앱을 만들어 보자

### 확산
확산 전략 잘 퍼지는것.
- 한 번 경험후 다시 찾아야 한다.
- 재미 손에 붙어야 한다.
- 전파 할 수 있는 이미지, 영상이여야한다.
- 추천시스템.. 영상, 예술, 재미, 코믹,
- 날라주다. 전달시스템. rss
- 쉽게 볼 수 있어야..  목록&뷰 형식

### 어떻게
- 어찌 찾을 것인가. 사람들의 반응을 감지.
- 초기 확산의 기운을 감지 한다. like 버튼
- 관리 대상의 폭을 넓이다. 인터넷 한글 게시물 전체..
- 기미를 감지 하다.


방금 그 라디오
-----------------

### 개요
- 방금 그 곡을 라디오로 플레이 한다.
- 라디오로 노래만 들을 수 있다.
- 업데이트시 라이디 체널 자동 변경, 갱신/멈춤
- 방금 그 곡 사용  [다음방금그곡]( http://m.music.daum.net/onair/timeline)
- api 있으면 좋고 없으면, update call parsing http://m.music.daum.net/onair/timeline
- POST http://m.music.daum.net/onair/songlist.json?type=top&searchChannelType=popular&startTime=20140605100621&channelIds= HTTP/1.1
- [response json](onair.txt)

### 설명

### 제안
- 주파수를 받아서 제어 가능한 라디오 필요 (핸드폰이나. 라이오이거나 )
- 핸드폰은 라이오app 은 밴더 종속이랑 공통 app 만들기가 힘들어 보인다.

### 방금 그 곡 api 업데이트
- 한 곳에서만 해도 되겠다.
- 서버하나 두고, api 파씽해서 라이오 채널만 out 으로 내려주는 api 생성
- 채널을 받아서 라디로 플레이는 하는 app 필요.