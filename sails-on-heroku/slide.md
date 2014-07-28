# Sails on Heroku
### Heroku 와 Sails 살펴보기

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
- git 사용법 (필요한 부분만.. 최소)
- nodejs 사용법 (필요한 부분만.. 최소)
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
7. git add . && git commit
8. ```heroku create``` (최초 1번)
9. git push heroku master *for deploy*
- - -
## Heroku 사용하기(반복)
1. 코딩/테스트
2. git add . && git commit
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
- 확장하기 (2X Dyno - 1024MB/2x CPU시간당 $0.10)
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
- 기본 CRUD 는 백엔드 코드 불필요
   - Automatically generated JSON API  
   - Automatic route bindings
- +Grunt (Java의 mvn/ant, Ruby의 rake)
_ _ _
## Models
- Waterline
   - https://www.npmjs.org/package/waterline
   - ORM (Object Relational Mapping)
   - for mysql, mongo, postgres, redis..
_ _ _
## Controllers
- Contorller's method
   - http://localhost:1337/:controller/:method
- REST
   - get /:controller/:id?
   - post /:controller
   - put /:controller/:id
   - delete /:controller/:id
- Shortcut CRUD
   - /:controller/find/:id?
   - /:controller/create
   - /:controller/update/:id
   - /:controller/destroy/:id
_ _ _
## Views
- ejs
```HTML
<div>
  <h1>My first view</h1>

  <h2>My corndog collection:</h2>
  <ul>
    <% _.each(corndogs, function (corndog) { %>
    <li><%= corndog.name %></li>
    <% }) %>
  </ul>
</div>
```
- config/views.js
```javascript
  // ejs, jade, handlebars...
  engine: 'ejs',
```
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
## Sails on Heroku
간단한 메모웹앱 만들어보기
_ _ _
## Application 생성하기
- simple-memo-webapp 생성하기
```SHELL
$ sails new simple-memo-webapp
info: Created a new Sails app `simple-memo-webapp`!
```
```SHELL
$ cd simple-memo-webapp && tree
├── api
│   ├── controllers
│   ├── models
├── assets
├── config
│   └── ...
├── node_modules (ejs, grunt, sails, sails-disk..)
├── tasks
└── views (ejs)
```
- 기본 경로 및 기본 파일은 자동으로 생성됨.
- api : backend api (models, controllers)
- assets : client
- views
_ _ _
## API 생성하기
- Model and Controller 생성하기  

```SHELL
$ sails generate api Memo

info: Created a new model ("Memo") at api/models/Memo.js!
info: Created a new controller ("Memo") at api/controllers/MemoController.js!

info: REST API generated @ http://localhost:1337/Memo
info: and will be available the next time you run `sails lift`.
```
_ _ _
## Model 수정
- memo 항목과 writer 추가
```javascript
module.exports = {
    attributes: {
      // memo 항목
      memo: {
        type: 'string'
      },
      // writerName 은 필수
      writerName: {
        type: 'string',
        required: true
      }
    }
};
```
_ _ _
## View 생성하기
- 자동 바인딩을 위해서 views/ 동일한 이름으로 생성   
- views/layout.ejs 속으로···.

```SHELL
$ cd views && mkdir Memo

// 파일생성
$ echo Hello World >> index.ejs
```
_ _ _
## bootstrap, jquery 가져오기
- CSS, JS 다운로드
```SHELL
$ cd assets/styles
$ curl -O http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.css
$ curl -O http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.css
...
$ cd assets/js
$ curl -O http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.js
$ cd assets/js/dependencies
$ curl -O http://code.jquery.com/jquery-2.1.1.js
```
- sails lift 시, 자동 include (by grunt)
- sails lift --prod 모드에서 minify (by grunt)
_ _ _
## 메모 작성기능 추가 (ejs)
- /views/Memo/index.ejs 수정하기
- writerName 필드와 memo 필드를 추가.

```HTML
...
<input type="text" class="form-control col-md-2" id="writerName" name="writerName" placeholder="작성자명">
...
<input type="text" class="form-control" id="memo" name="memo" placeholder="메모남기기..">
```
_ _ _
## 메모 작성기능 추가 (js)
- assets/js/memo.js 추가하기
- submit 시 POST 로 전달 

```javascript
$(document).ready(function() {

  var $form = $("#form");

  $form.submit(function(e) {
    e.preventDefault();

    var reqData = $form.serialize();
    $.ajax({
      type: "POST",
      url: "/memo",
      data: reqData
    }).done(function( resultJson ) {
    });

  });
});
```
_ _ _
## 메모 조회 (ejs)
- memos 를 받아서 각각 필드 조회  
```HTML
      <ul id="list">
        <% _.each(memos, function (memo) { %>
        <li><%= memo.writerName %> : <%= memo.memo %> : <%= memo.updatedAt %></li>
        <% }) %>     
      </ul>
```
_ _ _
## 메모 조회 (controller)
- find method override (defualt json)
```javascript
  find: function(req, res) {

    Memo.find()
    .limit(100)
    .sort('updatedAt')
    .exec(function(err, memos) {
      return res.view('Memo/index', {memos:memos});
    });
  }
```
_ _ _
## 메모 삭제하기 (index.ejs)
- html (ejs)
```HTML
<input type="text" id="targetId">
<button id="removeBtn" class="btn btn-primary">remove</button>
```
_ _ _
## 메모 삭제하기 (js)
- via socket.io

```javascript
$(document).ready(function() { 
...
io.socket.get('/Memo');  // subscribe.

  // publishDestroy
  $("#removeBtn").click(function(e) {
    io.socket.delete('/Memo', {
        id: parseInt($('#targetId').val()),
      }, function (response) {
        console.log('removed');
    });
  });

  io.socket.on('memo',function(obj){
    if (obj.verb == 'destroyed') {
      $("#li_"+obj.id).append('<strong> was removed!</strong>');
        console.log(obj.id + ' was removed.');
    }
  });
```
_ _ _
## 메모 삭제하기 (Controller)
- destroy override

```javascript
  find: function (req, res) {
  ...
      Memo.subscribe(req.socket, memos);

      if (req.isSocket) {
        return res.json({memos:memos});
      }
  ...

  destroy: function (req, res) {
    var id = req.param('id');

    Memo.destroy({'id':id}).exec(function destroy(err){
      Memo.publishDestroy( id );
    });

    return res.json({targetId: id});
  }
```
- - -
## etc
- - -
## sails 그외
- CORS (Cross-Origin Resource Sharing) 
- Policies
- File Uploads
- Internationalization
- Security (CSRF...)

- - -
## sails 를 heroku 에..
- git repository 초기화 & 커밋.
```SHELL
$ git init .
$ git add .
$ git commit -m 'simple-app'
... ...
$ heroku apps:create rkjun-test-sails
$ git push heroku master
```
- - -
## sails 를 heroku 에..
```SHELL
$ heroku ps:scale web=1
$ heroku ps
=== web (1X): `npm start`
web.1: up 2014/07/28 16:33:41 (~ 18s ago)
```

- Procfile 생성하기 (heroku push까지..)

```SHELL
$ echo web: sails lift --prod >> Procfile
$ git add . && git commit -m "heroku procfile"
$ git push heroku master
... heroku deploy...
```
- - - 
## Data Storage 변경
- default - localDiskDb (sails-disk) .tmp/localDiskDb.db
- sails-mongo 설치하기
```SHELL
$ npm install sails-mongo --save (for sails 0.9.x)
$ npm install sails-mongo@0.10.x --save
```
- sails v0.10.0
   - config/connections.js
   - config/models.js
- sails v0.9.x
   - config/adapters.js
_ _ _
## heroku addon 추가 
- credit card 필요.
- heroku addon add mongoHQ
```SHELL
$ heroku addons:add mongohq
...
$ heroku config | grep MONGOHQ_URL
MONGOHQ_URL : mongodb://heroku:...
```
_ _ _
## db 정보 추가
- config/connections.js

```javascript
  mongoHQ: {
    adapter: 'sails-mongo',
    // host: 'localhost',
    // port: 27017,
    // user: 'username',
    // password: 'password',
    // database: 'your_mongo_db_name_here'
    url: process.env.MONGOHQ_URL
  },
```
- config/models.js

```javascript
  connection: 'mongoHQ'
```
- - -
## 결론
- heroku 무료 
   - 원하지 않게, 실수로 유료서비스 사용하지 않게 주의
- sails - 지금도 개발중.
   - 어느 정도 안정화
   - 버전별 차이는 있음
      - 마이그레이션이 필요함.
- sails 를 보니 ruby on rails 에 흥미가 생김.
- - -
## 참고
* [Heroku Dev Center](https://devcenter.heroku.com/)
* [Sailsjs](http://sailsjs.org/)
- - -
## 끝
<small>- 30시간의 삽질을 30분에....</small>   
<small>- github [@rkjun](http://github.com/rkjun), twitter [@rkjun](http://twitter.com/rkjun)</small>   
