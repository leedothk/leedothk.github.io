---
layout: default
title: Flask uWSGI Nginx
parent: Python
nav_order: 1
---

# Flask uWSGI Nginx 머신 러닝 플랫폼 구축
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

파이썬은 자바와 같은 가상머신이 없기 때문에 로컬에서의 개발 결과물을 서버로 곧바로 배포할 수는 없다.  대신에 Pycharm IDE와 도커를 이용하여 개발과 포팅을 할 수 있는 환경을 구축하여 개발과 배포를 용이하게 한다.

<br>

**_파이참 IDE 개발 -> Git -> 로컬 도커 -> 도커 허브 -> 서버 도커_**

<br>

![](/just-the-docs/assets/images/python_ml_arch.png)

---

## Docker CentOS 8 설정

<br>

윈도우10에서는 Window용 도커를 사용할 수 있으므로 VirtualBox와 같은 가상머신툴을 사용할 필요가 없다.  단, 윈도우10 설정에서 Hyper-V를 사용으로 설정해야 한다.

```
PS C:\Users\LHK> docker run --privileged -d --name machine -h machine -p 222:22 -p 80:80 -p 5000:5000 -p 8000:8000 centos /sbin/init
```

<br>

윈도우용 도커를 설치하고 PowerShell 또는 커맨트창을 열어서 CentOS 이미지를 다운받고 실행한다.  만약에 로컬에 CentOS 이미지가 있으면 있는 이미지를 실행하고, 이미지가 없다면 도커 레파지토리에서 다운받아 실행한다.

백그라운드로 실행중인 `machine` 호스트에 접속한다.

```
PS C:\Users\LHK> docker exec -it machine bash
```

다운로드 받은 CentOS의 버전을 확인한다.

```
[mechanic@machine ~]$ cat /etc/centos-release
CentOS Linux release 8.2.2004 (Core)
```

최신의 패키지 레파지토리를 추가한다.

```
[mechanic@machine ~]$ yum install epel-release
```

참고로, CentOS8 부터 yum 대신에 dnf를 사용한다.  yum 또한 사용할 수 있으나 dnf의 alias일 뿐이고 어떤 패키지의 경우에는 dnf로만 설치가 가능하다.

패키지 저장소가 추가되었으면 필요한 것들을 하나씩 설치한다(sudo 생략한다).

```
[mechanic@machine ~]$ dnf install ncurses
[mechanic@machine ~]$ yum install nginx
[mechanic@machine ~]$ yum install python3
[mechanic@machine ~]$ yum install gcc  # uWSGI 설치시 필요
[mechanic@machine ~]$ dnf install python3-devel -y
```

nginx 시작하고 확인한다.

```
[mechanic@machine ~]$ systemctl start nginx
[mechanic@machine ~]$ systemctl enable nginx
```

localhost:80 으로 접속해서 Nginx 초기 페이지가 보이면 설치가 완료된 것이다.

ssh도 설치해서 외부의 텔넷 프로그램으로 접속이 가능하도록 한다.  포트가 겹치는 경우 적절히 포트 포워딩한다.

```
[mechanic@machine ~]$ dnf install openssh-server
```

이제 MobaXTerm과 같은 텔넷 프로그램으로 접속이 가능하다.

```
/home/mobaxterm > ssh mechanic@sparkc.tipsbdsys -p 222
```

한글을 사용할 수 있도록 홈 디렉터리의 설정파일 수정한다.

<div class="code-example" markdown="1">
```shell
.virc
set encoding=utf-8
set fileencodings=utf-8,cp949

.profile
export LANG=ko_KR.euckr
```
</div>

일단 여기까지 하고 도커 이미지를 태깅하고 저장하고 푸쉬한다.

```
PS C:\Users\LHK> docker commit machine centos8:flask-uwsgi-nginx
PS C:\Users\LHK> docker tag centos8:flask-uwsgi-nginx leedothk/centos8:flask-uwsgi-nginx
PS C:\Users\LHK> docker push leedothk/centos8:flask-uwsgi-nginx
```

---

## 파이선 가상환경 설정

<br>

파이선은 프로젝트별로 필요한 패키지 환경을 따로 구성할 수 있다.  물론 전역적으로 패키지를 설치하여 사용할 수도 있지만, 프로젝트별로 가상의 환경에서 패키지를 구성하는 것이 패키지간의 충돌을 예방하거나 패키지 관리에 유리하다.

먼저 ssh를 이용하여 접속하고 프로젝트의 홈 디렉터리로 이동한다.

```
[mechanic@machine ~]$ pip3 install virtualenv
[mechanic@machine ~]$ virtualenv venv
[mechanic@machine ~]$ source myprojectenv/bin/activate
(venv) [mechanic@machine ~]$
```

패키지가 활성화 되면 프롬프트앞에 `(가상환경명)`이 붙음으로써, 현재 어떤 가상환경이 적용되어 있는지 알 수 있다.  이 상태에서 패키지를 설치하게 되면 해당 프로젝트에만 사용가능하도록 패키지가 설치된다.  이제 uWSGI와 Flask를 설치한다.

```
(venv) [mechanic@machine ~]$ pip install uwsgi flask
```

플라스크는 파이선 기반의 마이크로웹 서비스 패키지로서, 별도의 구성없이 간단한 웹서비스를 제공할 수 있다.  이런 플라스크를 Nginx 웹서버와 연결시켜 주는 인터페이스가 uWSGI(uWeb Serive Gateway Interface).  Nginx로 들어온 요청을 wWSGI의 소켓을 통해 flask로 전달돠고 flask는 웹서비스에 있어서 어플리케이션 역할을 하게 된다(고전 아키텍쳐인 CGI와 유사).

아래 코드를 입력하여 설치한 플라스크가 정상적으로 실행되는지 확인한다.

<div class="code-example" markdown="1">
```python
flaskapp.py

from flask import Flask
application = Flask(__name__)

@application.route("/")
def hello():
    return "<h1 style='color:blue'>Hello There!</h1>"

if __name__ == "__main__":
    application.run(host='0.0.0.0')
```
</div>

```
(venv) [mechanic@machine ~]$ python flaskapp.py
```

플라스크를 실행하고 localhost:5000 으로 접속하여 확인한다.

이제 플라스크와 Nginx를 인터페이스 역할을 하는 uWSGI를 확인한다.

<div class="code-example" markdown="1">
```python
wsgi.py

from myproject import application

if __name__ == "__main__":
    application.run()
```
</div>

```
(venv) [mechanic@machine ~]$ uwsgi --socket 0.0.0.0:8000 --protocol=http -w wsgi
```

이후 구성은 uWSGI를 이용하여 Flask와 Nginx를 연동하는 것으로써, 가상환경을 사용하도록 설정하게 되므로 커맨드라인에서의 가상환경은 더이상 필요없다.

```
(venv) [mechanic@machine ~]$ deactivation
[mechanic@machine ~]$
```

---

## uWSGI 를 이용하여 Nginx 와 Flask 연결

<br>

`WSGI(Web Server Gateway Interface)`는 웹서버와 웹앱 사이의 인터페이스를 정의한 표준으로써, uWSGI 는 이 표준을 따르는 제품이름이다.  uWSGI는 소켓통신을 이용한다.  먼저 프로젝트 디렉터리에 프로젝트에서 사용할 인터페이스 환경을 설정한다.

<div class="code-example" markdown="1">
```python
mechanic.py

[uwsgi]
module = wsgi
master = true
processes = 5
socket = mechanic.sock
chmod-socket = 660
vacuum = true
die-on-term = true
```
</div>

uWSGI 서비스를 시스템에 등록하여, 서버가 재시작할 때 자동으로 실행되고 아울러 플라스크도 같이 실행되도록 한다

<div class="code-example" markdown="1">
```shell
/etc/systemd/system/mechanic.service

[Unit]
Description=uWSGI instance to serve mechanic
After=network.target
[Service]
User=user
Group=nginx
WorkingDirectory=/home/mechanic
Environment="PATH=/home/mechanic/venv/bin"
ExecStart=/home/mechanic/venv/bin/uwsgi --ini mechanic.ini
[Install]
WantedBy=multi-user.target
```
</div>

```
[mechanic@machine ~]$ systemctl start mechanic
[mechanic@machine ~]$ systemctl enable mechanic
```

이제 `mechanic`이라는 이름의 서버가 기동될 때마다 flask 와 uWSGI 가 자동으로 실행된다.  정상적으로 실행되면 프로젝트 디렉터리에 'mechanic.sock' 파일이 생성된다.

이제 Nginx로 들어오는 요청을 wWSGI로 넘기도록 설정한다.

<div class="code-example" markdown="1">
```shell
/etc/nginx/nginx.conf

...
server {
    listen 80;
    server_name server_domain_or_IP;

    location / {
        include uwsgi_params;
        uwsgi_pass unix:/home/mechanic/mechanic.sock;
    }
}
...
```
</div>

설정문법이 정상인지 확인한다.

```
[mechanic@machine ~]$ nginx -t
```

Nginx 를 사용하는 사용자가 프로젝트에 접근할 수 있도록 권한을 부여한다.

```
[mechanic@machine ~]$ usermod -a -G user nginx
[mechanic@machine ~]$ chmod 710 /home/user
```

Nginx 를 제기동한다.

```
[mechanic@machine ~]$ systemctl start nginx
[mechanic@machine ~]$ systemctl enable nginx
```

이제 Nginx 를 통해 들어온 요청은 uWSGI 를 거처 Flask 에 전달된다.  도커 이미지를 저장하고 push한다.

---

## 개발환경 구성과 배포에 대해...

<br>

파이선 프로젝트는 자바와 다르게 가상머신 기반의 프로그램이 아니기 때문에 로컬(PC)에서의 개발 결과물을 곧바로 서버로 포팅할 수는 없다.  또한 uWSGI는 fork 기반의 프로그램이기 때문에 쓰레드기반의 윈도우에서는 설치가 불가능하다.  따라서 일반적인 커맨드라인상에서의 가상환경을 이용한 개발은 불가능하나, JetBrain사의 PyCharm을 이용하면 PyCharm이 wsgi와 Nginx 역할을 해주기 때문에 로컬에서도 개발이 가능하고 중간에 git을 이용하면 서버로의 배포도 가능하다.  PyCharm은 무료인 Cummunity과 유료인 Professional 버전이 있는데 Community 버전으로도 개발이 가능하기 때문에 굳이 Professional 버전을 사용할 필요는 없다.

프로젝트를 생성할 때는 위의 과정을 반복하거나, 아니면 위의 과정을 Git으로 만든 후 clone하거나 한다.  자세한 과정은 생략한다.

프로젝트를 생성한 후 Interpreter를 설정한다.

```
File > Settings > Project Interpreter > Vitual Envirionment

Base Interpreter : pythonw.exe
```

참고로, 로컬에서 먼저 프로젝트를 생성하고 Git 에 올릴 때 `Git Share` 메뉴를 이용하면 알아서 init 을 해주기 때문에 편리하다.

경우에 따라서 파이참 터미널에서 pip를 이용하여 직접 설치해주어야 하는 패키지들이 있을 수 있다.

---

## 도커를 이용한 서비스 배포(sparkc.tipsbdsys)

<br>

로컬에서 개발이 끝난 프로그램을 이미지로 만들어서 도커 레파지터리로 push를 했다고 가정한다.

spakc.tipsbdsys 접속하고, 여기서 도커 이미지를 다운로드한다.

```
[root@sparkc ~]# docker run --privileged -d --name machine -h machine -p 222:22 -p 80:80 -p 5000:5000 -p 8000:8000 docker.io/leedothk/centos8:flask-uwsgi-nginx /sbin/init
```

_* sparkc.tipsbdsys 에서 ssh 를 이미 사용하고 있기 때문에 222 번 포트를 22로 포트 포워딩한다._

```
/home/mobaxterm > ssh mechanic@sparkc.tipsbdsys -p 222
```

sparkc.tipsbdsys 에서 ssh 를 이미 사용하고 있기 때문에 222 번 포트를 이용하여 이미지로 된 서버의 22로 포트로 접속한다.

http://sparkc.tipsbdsys/로 접속해본다.

