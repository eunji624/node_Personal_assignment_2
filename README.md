# node_Personal_assignment_2

내일배움캠프 Node.js 숙련주차 개인과제

http://mallish.store/api/

# 환경변수

- .env 파일에 어떤 환경변수가 추가되어야 하는지 작성합니다.

  - DB_PWD
  - DB_USER_NAME
  - DB_HOST
  - DB_NAME
  - PORT
  - SECRET_KEY

- 그 밖의 사용한 환경변수를 나열해 주세요.

  - DB_ENGINE

# API 명세서 URL

- 구글 Docs 공유 URL 추가

https://docs.google.com/spreadsheets/d/1ujCVNFIhgsDy3UfyvX24Keni2-DMAPjIksdsO53khlA/edit#gid=0

# ERD URL

- ERD Cloud URL 추가

  https://www.erdcloud.com/d/sMPmb43rHDNeFv68G

# 더 고민해 보기

1. **암호화 방식**

- 비밀번호를 DB에 저장할 때 Hash를 이용했는데, Hash는 `단방향 암호화`와 `양방향 암호화` 중 어떤 암호화 방식에 해당할까요?

  > 단방향 암호화에 해당합니다. 복호화를 할 수 없기 때문입니다.

- 비밀번호를 그냥 저장하지 않고 Hash 한 값을 저장 했을 때의 좋은 점은 무엇인가요?
  > 정보가 탈취되어 데이터베이스에 누군가 접근했다고 하더라도, 단방향 암호화 Hash의 경우 비밀번호를 알 수 없습니다.

2. **인증 방식**

- JWT(Json Web Token)을 이용해 인증 기능을 했는데, 만약 Access Token이 노출되었을 경우 발생할 수 있는 문제점은 무엇일까요?

  > 토큰이 노출되었다는 사실을 인지하고도, 토큰을 만료시킬 수 없습니다.
  > 해당 토큰이 만료될때까지 기다려야 합니다. 따라서 피해가 커질 수 있습니다.

- 해당 문제점을 보완하기 위한 방법으로는 어떤 것이 있을까요?

  > Refresh Token을 이용해서 Access Token을 발급해 주는 것 입니다.<br/>
  > 좀더 자세히 말하자면, Access Token의 만료기간을 짧게 두고, 해당 만료기간이 끝나게 되면, Refresh Token을 이용해서 새로운 Access Token을 발급 받습니다. 새로 받은 Access Token을 이용해 유저는 다시 로그인 하지 않고도 서비스를 이용할 수 있게 됩니다.

3. **인증과 인가**

- 인증과 인가가 무엇인지 각각 설명해 주세요.

  > 인증은 로그인 과정, 인가는 유저의 모든 요청마다 접근 권한이 있는지 판단하는 과정입니다.

- 과제에서 구현한 Middleware는 인증에 해당하나요? 인가에 해당하나요? 그 이유도 알려주세요.

  > 인가에 해당합니다.<br/>
  > 로그인을 통해 토큰을 발급하는 과정이 "인증",<br/>
  > 인증 미들웨어를 통해 유저의 접근 권한을 확인하는 과정이 "인가"이기 때문입니다.<br/>

4. **Http Status Code**

- 과제를 진행하면서 `사용한 Http Status Code`를 모두 나열하고, 각각이 `의미하는 것`과 `어떤 상황에 사용`했는지 작성해 주세요.

  > 200 : 성공적인 요청 처리 _ 요청을 성공적으로 처리한 경우 사용했습니다.<br/>
  > 201 : 성공적인 생성 _ 요청을 성공척으로 처리하여 새로운 리소스가 생성된 경우 사용했습니다.(회원가입, 상품 작성)<br/>
  > 400 : 유저가 요청한 구문이 이상할때 _ 입력 데이터가 형식에 맞지 않을 경우 사용했습니다.<br/>
  > 401 : 유저가 접근하려 하는 것에 권한이 없을 때 \*\* 이미 로그인 한 사용자가 로그인 하려 할때 사용했습니다.<br/>
  > 404 : 유저가 접근하려 하는 것이 없을 때 _ 삭제한 게시글을 접근하려 할때 사용했습니다.<br/>
  > 409 : 서버가 요청을 수행하는 도중 충돌이 발생할 때 \_ 유저가 입력한 이메일이나 닉네임 값이 이미 서버에 존재할 때 사용했습니다.

5. **리팩토링**

- MongoDB, Mongoose를 이용해 구현되었던 코드를 MySQL, Sequelize로 변경하면서, 많은 코드 변경이 있었나요? 주로 어떤 코드에서 변경이 있었나요?

  > 데이터베이스에 접근하는 메소드가 약간씩 달라 db crud 부분과, 처음 셋팅하는 부분에서 변경이 있었습니다.

- 만약 이렇게 DB를 변경하는 경우가 또 발생했을 때, 코드 변경을 보다 쉽게 하려면 어떻게 코드를 작성하면 좋을 지 생각나는 방식이 있나요? 있다면 작성해 주세요.
  > .

6. **서버 장애 복구**

- 현재는 PM2를 이용해 Express 서버의 구동이 종료 되었을 때에 Express 서버를 재실행 시켜 장애를 복구하고 있습니다. 만약 단순히 Express 서버가 종료 된 것이 아니라, AWS EC2 인스턴스(VM, 서버 컴퓨터)가 재시작 된다면, Express 서버는 재실행되지 않을 겁니다. AWS EC2 인스턴스가 재시작 된 후에도 자동으로 Express 서버를 실행할 수 있게 하려면 어떤 조치를 취해야 할까요?
  (Hint: PM2에서 제공하는 기능 중 하나입니다.)

  > startup 기능을 이용해 해결할 수 있습니다.

7. **개발 환경**

- nodemon은 어떤 역할을 하는 패키지이며, 사용했을 때 어떤 점이 달라졌나요?

  > 파일을 수정후 저장만 하면, 서버를 자동으로 재시작 해주는 역할을 합니다.<br/>
  > 사용함으로 인해서 번거로운 작업이 많이 줄어들고 효율적인 작업을 할 수 있었습니다.<br/>

- npm을 이용해서 패키지를 설치하는 방법은 크게 일반, 글로벌(`--global, -g`), 개발용(`--save-dev, -D`)으로 3가지가 있습니다. 각각의 차이점을 설명하고, nodemon은 어떤 옵션으로 설치해야 될까요?

  > 개발용(`--save-dev, -D`)은 실제 배포에는 필요가 없으나, 개발할때에는 필요한 라이브러리를 설치하는 경우에 사용합니다.<br/>
  > 예를들어 sequelize-cli나 nodemon 같은 경우가 그렇습니다.<br/>

  > 글로벌(`--global, -g`)은 해당 라이브러리를 전역으로 설치하고 싶은 경우 사용합니다.<br/>
  > 시스템의 node_modules에 설치되며, 프로젝트에서는 사용할 수 있지만, package.json 파일에는 표기되지 않습니다.<br/>

  > 일반으로 설치하게 되면 package.json 파일의 dependencies 에 해당 라이브러리 이름이 추가됩니다.<br/>
  > 배포시 사용할 라이브러리들은 모두 dependencies에 담아둡니다.<br/>

  > nodemon의 경우 배포에는 필요가 없으니 개발용으로 -D 옵션을 이용하면 됩니다.<br/>
