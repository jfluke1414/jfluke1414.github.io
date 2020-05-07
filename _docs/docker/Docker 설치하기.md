---
title: (Docker) Docker 설치하기
category: Docker
order: 1
---

이제 Docker를 설치해보겠습니다. Docker는 소스를 컴파일해서 설치하려면 준비해야 할 것이 많습니다. 따라서 이 장에서는 자동 설치 스크립트와 각 리눅스 배포판의 패키지로 설치하는 방법을 설명하겠습니다. 소스를 컴파일해서 설치하는 방법은 부록을 참조하기 바랍니다.

리눅스
리눅스에 Docker를 설치하는 방법은 두 가지가 있습니다. Docker에서 제공하는 자동 설치 스크립트를 이용하는 방법과 리눅스 배포판의 패키징 시스템을 이용하여 직접 설치하는 방법이 있습니다.

자동 설치 스크립트
Docker는 리눅스 배포판 종류를 자동으로 인식하여 Docker 패키지를 설치해주는 스크립트를 제공합니다.
$ sudo wget -qO- https://get.docker.com/ | sh
get.docker.com 스크립트로 Docker를 설치하면 hello-world 이미지도 자동으로 설치됩니다. hello-world 이미지는 사용하지 않을 것이므로 모두 삭제합니다.
$ sudo docker rm `sudo docker ps -aq`
$ sudo docker rmi hello-world

우분투
자동 설치 스크립트를 사용하지 않고 우분투에서 패키지로 직접 설치하는 방법입니다. 버전은 14.04 LTS 64비트 기준입니다.
$ sudo apt-get update
$ sudo apt-get install docker.io
$ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
/usr/bin/docker.io 실행 파일을 /usr/local/bin/docker로 링크해서 사용합니다.

RedHat Enterprise Linux, CentOS
자동 설치 스크립트를 사용하지 않고 레드햇 엔터프라이즈 리눅스(RHEL)와 CentOS에서 패키지로 직접 설치하는 방법입니다. RHEL과 CentOS 6 패키지 저장소에는 docker-io가 없으므로 EPEL(Fedora Extra Packages For Enterprise Linux) 저장소를 사용할 수 있도록 설정합니다.
CentOS 6
$ sudo yum install http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
$ sudo yum install docker-io
AWS EC2에 설치되는 Amazon Linux(RHEL 기반)는 EPEL 저장소를 바로 사용할 수 있으므로 epel-release-6-8.noarch.rpm을 설치하지 않아도 됩니다.
CentOS 7에서는 docker 패키지를 설치하면 됩니다.
CentOS 7
$ sudo yum install docker
Docker 서비스 실행하기
$ sudo service docker start
부팅했을 때 자동으로 실행하기
$ sudo chkconfig docker on

최신 바이너리 사용하기
배포판 버전이 오래되었거나, CentOS 같이 버전업이 보수적인 배포판은 Docker 패키지 버전이 낮은 경우가 많습니다. 이번에는 배포판별 패키지가 아닌 빌드된 바이너리를 직접 사용하는 방법입니다.
이미 패키지로 설치했을 때는 다음과 같이 명령을 실행합니다.
$ sudo service docker stop
$ sudo wget https://get.docker.com/builds/Linux/x86_64/docker-latest \
    -O $(type -P docker)
$ sudo service docker start
새로 설치할 때는 다음과 같이 명령을 실행합니다.
$ wget https://get.docker.com/builds/Linux/x86_64/docker-latest
$ chmod +x docker-latest
$ sudo mv docker-latest /usr/local/bin/docker
$ sudo /usr/local/bin/docker -d
URL을 docker-latest로 지정하면 가장 최신 버전을 받고, docker-1.3.0처럼 지정하면 특정 버전을 받을 수 있습니다.
