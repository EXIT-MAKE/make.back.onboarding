# 🧑‍💻 MAKE ONBOARDING for BACKEND

메이크 백엔드 신규 입사자 교육을 위한 레포지토리입니다.

## 🗃 우리 서비스는?

```
    
    +---- Front-end ----+    +--------+                                        +-- Auto Scaling Group (Blue)--+         +------+
    |     +-------+     |    |  Fire  |                                        |   +-- EC2 --+   +-- EC2 --+  |         |  S3  +<---+
    |     |  APP  +     +<-->+  Base  |                                   +--->+   | Docker  |   | Docker  |  +<---+    +---+--+    |
    |     +-------+     |    |  Auth  |  +---------+    +-------------+   |    |   +---------+   +---------+  |    |        |       |
    |     +------+      |    +--------+  |  Route  |    | Application |   |    +------------------------------+    |   +----+---+   |
    |     | MAKE |      |     +--------->+    53   +--->+    Load     +---+                                        +<--+  Code  |   |
    |     +------+      |     |  MAKE    |  (DNS)  |    |  Balancer   |   |    +-- Auto Scaling Group(Green)--+    |   | Deploy +<--+
    |    +---------+    |     |          +---------+    +-------------+   |    |   +-- EC2 --+   +-- EC2 --+  |    |   +--------+   |
    |    |  Block  |    |     |                                           +--->+   | Docker  |   | Docker  |  +<---+        Deploy! |
    |    |  Editor |    +---->+                                                |   +---------+   +---------+  |   +--make.functions-++ 
    |    |  (WEB)  |    |     |  Sales                                         +-------------------+----------+   |    Git Actions   +
    |    +---------+    |     |    +---------+                                                     ^              +------------------+
    |   +-----------+   |     |    |   API   |     +--------+     +--- RDS1 ---+        +--- RDS2 -+-+
    |   | Education |   |     +--->+ Gateway +<--->+ Lambda +<--->+ PostgreSQL |        | PostgreSQL |
    |   +-----------+   |          +---------+     +---+----+     +------------+        +------------+
    |     +-------+     |                      Deploy! |
    |     | Admin |     |                          +---+- sales.functions --+
    |     +-------+     |                          |       Git Actions      |
    +-------------------+                          +------------------------+
    
```

```
💡 본 미션을 진행하기전 IAM 계정을 발급받았는지 확인해주세요.
```

## ⚽️ MAKE Mission 1

###  _간단한 서버를 올려보자_

본사의 서비스는 AWS의 클라우드 인프라를 활용하여 구축하고 있습니다. </br>
MAKE의 서버아키텍처를 직접 만들어볼까요? </br>

#### 📝 요구사항

- 서버는 Nestjs를 사용하여 구성되며, EC2에 배포할 것
- [닉네임].make-api.co 의 형태로 서브도메인을 구성할 것
- SSL 인증을 적용하고, 80번 포트로의 입력을 443으로 리다이렉션 할 것
- 연재중...

#### 🗝 미션 클리어를 위한 선수지식

- NestJs (TypeScript)
- EC2
- Route53 (DNS)
- AWS Certificate Manager
- Elastic Load Balancing (ALB)

## 🏀️ MAKE Mission 2

### _CI/CD, 오토스케일링을 위한 환경을 구성해보자_

본사의 서비스는 무중단 배포 자동화와, CPU 사용량에 따른 오토스케일링이 적용되어 있습니다.  </br>
원활환 서비스 제공을 위한 환경조성이 목적인데요. 직접 이 환경을 구성해봅시다. </br>

#### 📝 요구사항

- Mission 1 에서 구성한 작업환경에 이어서 구축해야합니다.
- GitHub에서 제공하는 GitActions를 이용합니다.
- CPU 사용량이 70프로 이상 유지될 경우 오토스케일링을 시작합니다.
- 연재중...

#### 🗝 미션 클리어를 위한 선수지식

- Target groups
- EC2 AMI, 시작 템플릿
- Auto Scaling
- CodeDeploy

## ⚾ MAKE Mission 3

### _docker를 적용한 환경을 구성해보자_

#### 📝 요구사항

#### 🗝 미션 클리어를 위한 선수지식

## 🏐 MAKE Mission 4

### _Nestjs로 딴딴한 백엔드 구현하기_

#### 📝 요구사항

#### 🗝 미션 클리어를 위한 선수지식

## 🎱️ Bonus Mission

### 1. _Lambda에 API 서버를 올려보자_

#### 📝 요구사항

```
CEO Monday는 개발팀의 고충을 알기 위해 직접 웹사이트를 만들었지만, 사람들이 방문하는지 알 수 없었습니다. 
그래서 자신의 사이트에 누군가가 접속을 하면 DB에 기록되는 API가 필요하다고 생각하고 이를 신입 개발자에게 맡기기로 합니다.
```

1. nodejs 기반의 serverless framework 템플릿을 구성하고 기본 환경을 배포합니다.
   1. 텝플릿은 aws node js 템플릿을 사용하며, ts로 변경하여 사용해도 됩니다.
   2. 서비스 명은 back-onboarding-[닉네임]으로 지정합니다.
   3. 레포지토리를 따로 마련하여 'develop', 'master' 브랜치를 구성하고, gitflow를 준수합니다.
   4. 오프라인에서 해당 서비스를 실행해보고 정상동작이 될 경우 deploy 합니다.
2. `/connect GET` 요청이 들어올 경우 Request 정보를 저장하는 API를 구축합니다.
   1. 템플릿 초기 설정시 만들어진 핸들러를 참고하여 해당 API를 구축해봅니다.
   2. AWS 콘솔은 VPC, Subnet, EIP 등의 생성을 위해서만 사용하고, 서버리스에 관한 세부 설정은 코드에서 처리하도록 합니다.
   3. 환경 변수는 `.env`, `.env.dev`, `.env.prod` 로 분할하여 구성하며, 절대 레포지토리에 업로드 하지 않습니다.
   4. DB는 sales DB의 onboarding-[닉네임]을 사용합니다.
   4. DB 스키마의 형태는 자유롭게 설정합니다.
3. GitActions 를 이용하여 CD를 구축합니다.
   1. `.env`파일을 CD 스크립트로 구성합니다.
   2. 환경 변수들은 secrets를 이용하여 저장합니다.
   3. develop 은 dev 스테이지에 master 는 prod 스테이지에 올라가도록 합니다.

### 2. _Lambda에 스케줄러를 올려보자_

```
"오늘 하실건가요?" "뭘요?" 오늘도 Jack은 '금알못(금요일을 알차게 보내는 건 못참지)'을 기억하지 못했습니다. 
이쁨을 받고 싶었던 신입개발자는 저번 미션을 기반으로 '금알못'알림이를 만들려고 합니다.
금알못은 매주 금요일 오후 7시에 시작하는 사내 모임입니다. 슬랙으로 10분전에 알림을 주도록 해봅시다.
```

#### 📝 요구사항

1. 매주 금요일 KST 오후 6시 50분에 슬랙에 알림이 가는 스케쥴러를 구현합니다.
   1. AWS 콘솔은 배포가 되었는지 확인하는 용도로 사용하고, 세부 설정은 코드상에서 해결하도록 합니다.
   2. 슬랙 알림의 형태는 자유롭게 설정합니다.
2. 기존에 진행했던 레포지토리에 이어서 핸들러를 구현합니다.
   1. 같은 레포에 구성하되 환경변수는 핸들러에 따라 구분하여 배포하도록 설정합니다.

#### 🗝 미션 클리어를 위한 선수지식

- serverless Framework
- AWS Lambda