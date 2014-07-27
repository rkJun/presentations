# Sails on Heroku
### 간편 메모웹 만들기

2014.07.29 / [@rkjun](http://twitter.com/rkjun)

Note:
시작시 image 필요한가
- 좀더 고민해보기
- - -
## 오늘 이야기하는 것
- Heroku - PAAS  
  <small>클라우드 플랫폼</small>
- Sails - Node framework  
  <small>ruby on rails 에서 영감을 얻은 Node framework</small>
_ _ _
## 오늘 이야기하지 않는 것
- git 사용법
- nodejs 사용법
- 지속적인 통합 (CI Tool) 적용하기  
등은 다루지 않음.
_ _ _
- PaaS(Platform as a Service)  
  SaaS의 개념을 개발 플랫폼에도 확장한 방식으로, ***개발을 위한 플랫폼 구축을 할 필요 없이 필요한 개발 요소들을 웹에서 쉽게 빌려쓸 수 있게 하는 모델*** - [위키백과](http://ko.wikipedia.org/wiki/PaaS)

- Sails.js  
  make it easy to build custom enterprise-grade Node.js apps. It is designed to mimic the MVC pattern of frameworks like Ruby on Rails, but with support for the requirements of modern apps: data-driven APIs with scalable, service-oriented architecture. It's especially good for building chat, realtime dashboards, or multiplayer games.
- - -
## Heroku
- "her-OH-koo" 허로쿠, 헤로쿠
- 클라우드 어플리케이션 플랫폼 (웹호스팅 + addons)
- 2007~
- Hero (영웅) + Haiku (일본의 단시 하이쿠)  
  : Haiku는 Ruby 언어 창시자 Yukihiro Matsumoto(Matz)에 대한 감사
_ _ _
## Heroku
develop ---> git commit ---> git push ---> deploy
- - -
## Heroku 지원 언어
- Ruby (Rails)
- Java (Spring, Play)
- Python (Django)
- Node.js
- PHP
- Clojure
- Scala
- - -
## Heroku Toolbelt Download
- https://toolbelt.heroku.com/
![heroku toolbelt](http://i.imgur.com/ZGSPIRK.png)
- Heroku client CLI tool + Foreman + Git
_ _ _
## Heroku Toolbelt
- Heroku client CLI tool  
  (for creating and **managing** Heroku apps)
- Foreman  
  (an easy option for running your apps **locally**)
- Git  
  (revision control and **pushing** to Heroku)
_ _ _
## OS X brew
```SHELL
$ brew install heroku-toolbelt
```
<small>heroku-toolbelt requires an installation of Ruby 1.9 or greater.</small>
- - -
## Heroku Login
- heroku dashboard
![Heroku Login](http://i.imgur.com/vvHM0lw.png)
_ _ _
## Heroku Login CLI
```SHELL
$ heroku login
Enter your Heroku credentials.
Email: adam@example.com
Password:
Could not find an existing public key.
Would you like to generate one? [Yn]
Generating new SSH public key.
Uploading ssh public key /Users/adam/.ssh/id_rsa.pub
```
- - -
## Create a new app
![create_a_new_app](http://i.imgur.com/9SkRxgH.png)
_ _ _
## Created an app 
- App URL
- Git URL
- ```git clone GIT_URL -o heroku``` (-o remote repo name을 origin 대신 heroku 로)
![created_app](http://i.imgur.com/W9XYAV4.png)
_ _ _
## Create a new app CLI
```SHELL
$ heroku create
Creating polar-brushlands-6730... done, stack is cedar
http://polar-brushlands-6730.herokuapp.com/ | git@heroku.com:polar-brushlands-6730.git
```
_ _ _
## Create a new app CLI - specify a name
```SHELL
$ heroku apps:create rkjun-test
Creating rkjun-test... done, stack is cedar
http://rkjun-test.herokuapp.com/ | git@heroku.com:rkjun-test.git
```
_ _ _
## Create a new app CLI in Git Repo Path
```SHELL
cd myapp
$ git init
Initialized empty Git repository in .git/
$ git add .
$ git commit -m "my first commit"
... ...
$ heroku create
Creating falling-wind-1624... done, stack is cedar
http://falling-wind-1624.herokuapp.com/ | git@heroku.com:falling-wind-1624.git
Git remote heroku added
... ...
$ git remote -v
heroku     git@heroku.com:falling-wind-1624.git (fetch)
heroku     git@heroku.com:falling-wind-1624.git (push)
```
or 
```SHELL
$ heroku git:remote -a falling-wind-1624
Git remote heroku added.
```
- - -
## Delete App
- WEB  
heroku dashboard-app-settings-Delete App
- CLI
```SHELL
$ heroku destroy rkjun-test --confirm rkjun-test
```
- - -
## Deploying code
- 배포하기
```SHELL
$ git push heroku master
```
- 내 브랜치명이 다른 경우에는, 브랜치 지정
```SHELL
$ git push heroku your_branch:master
```
- - -
## heroku 제약사항
- 한 SSH 키의 시간당 75 Git 요청만 허용함.
- - -
## Heroku 사용하기(처음)
1. (nodejs) 코딩
2. npm dependency 정의
3. Procfile 정의 (최초 1번)
4. ```foreman start``` *for Local Test*
6. git init . (최초 1번)
7. git add . && commit
8. ```heroku create``` (최초 1번)
9. git push heroku master *for deploy*
- - -
## Heroku 사용하기(반복)
1. 코딩/테스트
2. git add . && commit
3. git push heroku master *for deploy*
- - -
## After Deploy
- 1 dyno만 사용하기
```SHELL
$ heroku ps:scale web=1
```

- app 상태 체크 (dyno 갯수,실행명령어)
```SHELL
$ heroku ps
=== web (1X): `bin/hubot --adapter hipchat`
web.1: up 2014/07/22 18:28:05 (~ 17h ago)
```
- - -
## Visit your app
```SHELL
$ heroku open
```
- - -
## Dyno sleeping and scaling
- 확장하기 (2X Dyno - 1024MB/2x CPU 시간당 $.10)
```SHELL
$ heroku ps:scale web=2
```
- 잠자기 (idle)
```SHELL
$ heroku ps:scale web=0
```
_ _ _
## Dyno ?
- <small>_A dyno is a lightweight container running a single user-specified command.
Dynos are the containers in which your application components run._</small>
- app을 동작하기 위한 컨테이너  
- 사이즈 조절 가능 (1X, 2X, PX dynos)
_ _ _
## Dyno 가격
- 1X dynos: $0.05 / hour [512RAM, 1x CPU..]
- 2X dynos: $0.10 / hour [1024RAM, 2x CPU..]
- PX dynos: $0.80 / hour [6GB, 100%(8core)..]

- 1X dyno 기준 
  - 하루 _ $1.2 (약 1,200원)
  - 한달, 31일기준 - $37.2 (약 38,000원)
_ _ _
## 750 free dyno-hours per app
- app 당 매월 750시간 무료 dyno 제공
- 1X dyno 사용시 한달내내 무료 사용가능
- 2x dyno 사용시 375시간 (15.6일) 무료로 사용가능
- - -
## Automatic dyno restarts
- you create a new release by deploying new code
- changing your config vars
- changing your add-ons
- when you run heroku restart 
- ```$ watch heroku ps```
- - -
## Heroku 로그보기
- 로그보기
```SHELL
$ heroku logs
```
- tail 옵션 (-t, --tail)
```SHELL
$ heroku logs --tail
```
- - -
## one-off dyno로 명령어 실행
- 명령어 실행만을 위한 dyno 생성
```SHELL
$ heroku run 명령어
```
- top 명령 실행하기
```SHELL
$ heroku run top
```
- - -
## addons
- https://addons.heroku.com/
- DataStores  
<small>(Postgres, ClearDB MySQL, Redis, Memcached, MongoHQ...)</small>
- Mobile, Search, E-mail and SMS, Workers and Queueing, analytics, Caching, Monitoring, Media, Utilities ...
- add-ons 별로 별도의 가격정책이 있음

_ _ _
## addons - MongoHQ
* MongoHQ ?  
- https://www.mongohq.com  
- MongoDB as a Service  
- Storage 512MB 는 무료  
_ _ _
## addons -  +MongoHQ
- MongoHQ 추가하기
```SHELL
$ heroku addons:add mongohq
Adding mongohq on rkjun-app... done, v28 (free)
Use `heroku addons:docs mongohq` to view documentation.
```
- 설치후 MONGOHQ_URL 변수가 추가됨.
```SHELL
$ heroku config
MONGOHQ_URL:            mongodb://... ...
```

- MongoHQ 제거하기
```SHELL
$ heroku addons:remove mongohq --confirm your_app
Removing mongohq on your_app... done, v29 (free)
```
- - -
## Releases, Rollback
- Releases List
```SHELL
$  heroku releases
== demoapp Releases
v103 Deploy 582fc95  jon@heroku.com   2013/01/31 12:15:35
v102 Deploy 990d916  jon@heroku.com   2013/01/31 12:01:12
```
- Rollback
```SHELL
$ heroku releases:rollback v102
Rolling back demoapp... done, v102
$ heroku releases
== demoapp Releases
v104 Rollback to v102 jon@heroku.com   2013/01/31 14:11:33 (~15s ago)
v103 Deploy 582fc95   jon@heroku.com   2013/01/31 12:15:35
v102 Deploy 990d916   jon@heroku.com   2013/01/31 12:01:12
```
- - -
# Sails.js
- - -
## Sails.js
- JavaScript  
- Node.js  
  - event-driven, asynchronous architecture
- MVC Architecture  
- built on   
  - Express (for routing)
  - EJS (for templating)  
  - Socket.io (for cross-platform WebSockets...)
- http://sailsjs.org/
_ _ _
## Node.js
- Chrome's JavaScript runtime
- Build fast
- Event-driven
- Non-blocking I/O model
- http://nodejs.org/ 
_ _ _
## Node.js
- Node (node+npm) Install v0.10.29
  - Package Installer for Windows, OS X, Linux
    http://nodejs.org/download/
  - OS X (using Homebrew)
  ```SHELL
  $ brew install node
  ```
_ _ _
## NPM
- Node Packaged Modules
- a package manager for node
- https://www.npmjs.org/
_ _ _
## Express
- web application framework for node
- http://expressjs.com/

```javascript
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('hello world');
});

app.listen(3000);
```
_ _ _
## EJS
- <% Embedded JavaScript %>
- <%= JavaScript Template library %>
_ _ _
## Socket.io
- The Fastest And Most Reliable Real-time Engine
- Server
```javascript
io.on('connection', function(socket){
  console.log('a user connected');
  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});
```
- Client
```javascript
  var socket = io();
  $('form').submit(function(){
    socket.emit('chat message', $('#m').val());
    $('#m').val('');
    return false;
  });
  socket.on('chat message', function(msg){
    $('#messages').append($('<li>').text(msg));
  });
```
- - - 
## Sails.js
- REST Blueprints
- Automatically generated JSON API for manipulating models  
- 기본 CRUD 는 백엔드 코드 불필요

(You don't have to write any backend code to build simple CRUD apps)
- Automatic route bindings for your controller actions

- - -
## Sails.js
### sails 시작하기
_ _ _
## Sails.js
### Installation
- npm install sails global option
```SHELL
$ sudo npm -g install sails
```
_ _ _
## Sails.js
### Creating a New Sails Project
```SHELL
$ sails new testProject
info: Created a new Sails app `testProject`!
```
_ _ _
## Sails.js
### Now Lift the Server  
```SHELL
$ cd testProject
testProject $ sails lift
```
default home page
http://localhost:1337/
- - - 
## Sails.js
### sails 살펴보기
- - -
- 


- - -
## simple memo web app
npm install mongodb --save

- - -
## 번외) Jenkins on Heroku
## 번외) Wordpress on Heroku
- - -
## 결론
- 부숴도 좋은 장난감 만들기
- git 배우기
- - -
## 참고
* [Heroku Dev Center](https://devcenter.heroku.com/)
* [Sailsjs](http://sailsjs.org/)
- - -
## 고맙습니다
Thank you.

