# Sails on Heroku
### 간편 메모웹 만들기

2014.07.29 / [@rkjun](http://twitter.com/rkjun)



## 오늘 이야기하는 것
- Heroku - PAAS
- Sails - Node framework

Note:
오늘 이야기하지 않는 것
- os x 사용법



## Heroku
- "her-OH-koo" 허로쿠, 헤로쿠
- 클라우드 어플리케이션 플랫폼 (웹호스팅 + addons)
- 2007~
- Hero (영웅) + Haiku (일본의 단시 하이쿠)  
  : Haiku는 Ruby 언어 창시자 Yukihiro Matsumoto(Matz)에 대한 감사


## Heroku
develop ---> git commit ---> git push ---> deploy



## Heroku 지원 언어
- Ruby (Rails)
- Java (Spring, Play)
- Python (Django)
- Node.js
- PHP
- Clojure
- Scala



## Heroku Toolbelt Download
- https://toolbelt.heroku.com/
![heroku toolbelt](http://i.imgur.com/ZGSPIRK.png)
- Heroku client CLI tool + Foreman + Git


## Heroku Toolbelt
- Heroku client CLI tool  
  (for creating and **managing** Heroku apps)
- Foreman  
  (an easy option for running your apps **locally**)
- Git  
  (revision control and **pushing** to Heroku)


## OS X brew install
```SHELL
$ brew install heroku-toolbelt
```
<small>heroku-toolbelt requires an installation of Ruby 1.9 or greater.</small>



## Heroku Login
- heroku dashboard
![Heroku Login](http://i.imgur.com/vvHM0lw.png)


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



## Create a new app
![create_a_new_app](http://i.imgur.com/9SkRxgH.png)


## Created an app 
- App URL
- Git URL
- ```git clone GIT_URL -o heroku``` (-o remote repo name을 origin 대신 heroku 로)
![created_app](http://i.imgur.com/W9XYAV4.png)


## Create a new app CLI
```SHELL
$ heroku create
Creating polar-brushlands-6730... done, stack is cedar
http://polar-brushlands-6730.herokuapp.com/ | git@heroku.com:polar-brushlands-6730.git
```


## Create a new app CLI - specify a name
```SHELL
$ heroku apps:create rkjun-test
Creating rkjun-test... done, stack is cedar
http://rkjun-test.herokuapp.com/ | git@heroku.com:rkjun-test.git
```


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


## Delete App
- WEB  
heroku dashboard-app-settings-Delete App
- CLI
```SHELL
$ heroku destroy rkjun-test --confirm rkjun-test
```


## Deploying code
- 배포하기
```SHELL
$ git push heroku master
```
- 내 브랜치명이 다른 경우에는, 브랜치 지정
```SHELL
$ git push heroku your_branch:master
```


## heroku 제약사항
- 한 SSH 키의 시간당 75 Git 요청만 허용함.



## Heroku 사용하기(처음)
1. (nodejs) 코딩
2. npm dependency 정의
3. Procfile 정의 (최초 1번)
4. ```foreman start``` *for Local Test*
6. git init . (최초 1번)
7. git add . && commit
8. ```heroku create``` (최초 1번)
9. 8. git push heroku master *for deploy*


## Heroku 사용하기(반복)
1. 코딩/테스트
2. git add . && commit
3. git push heroku master *for deploy*



## Deploy after.


Let’s ensure we have one dyno running the web process type:

$ heroku ps:scale web=1


## dyno?


## heroku 얼마임?


## addons

## sails ?

## sails 사용법



## simple memo web app



# 결론
## 부숴도 좋은 장난감을 만들자
- toy
## git 을 배우자
- git link


## 고맙습니다
Thank you.

