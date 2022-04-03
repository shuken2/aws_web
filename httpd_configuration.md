## Install httpd (on AWS amazon linux 'Free Tier')
```
sudo yum install httpd
```

주요 디렉토리 설명
* conf : 주요 설정파일 httpd.conf ,  MIME 형식 지정위한 magic 파일 있는곳
* conf.d : Apache의 주요 설정을 분리해서 저장하는 곳. httpd.conf 설정 내용을 분리하여 이곳에 저장하면, httpd.conf 파일에서 불러와서 사용하게 됨. httpd.conf 파일 맨 마지막에 'IncludeOptional conf.d/*.conf' 구문이 있음
* logs : 로그파일 저장되는 디렉토리
* modules : Apache Module 설치 디렉토리

설치 완료되면 방화벽 설정
```
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```
