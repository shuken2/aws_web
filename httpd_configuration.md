#Install httpd (on AWS amazon linux 'Free Tier')
---
## 1. httpd 설치
```
sudo yum update -y
sudo yum install -y httpd
```

주요 디렉토리 설명
* conf : 주요 설정파일 httpd.conf ,  MIME 형식 지정위한 magic 파일 있는곳
* conf.d : Apache의 주요 설정을 분리해서 저장하는 곳. httpd.conf 설정 내용을 분리하여 이곳에 저장하면, httpd.conf 파일에서 불러와서 사용하게 됨. httpd.conf 파일 맨 마지막에 'IncludeOptional conf.d/*.conf' 구문이 있음
* logs : 로그파일 저장되는 디렉토리
* modules : Apache Module 설치 디렉토리
* 

**부팅 시 자동 시작되도록설정**
```
sudo chkconfig httpd on
chkconfig --list httpd
```

**Web 80 포트 접속용 Security Group설정**
* 유형 : HTTP
* 프로토콜 : TCP
* 포트범위 : 80
* 소스 : 사용자지정

-- Apache httpd는 Apache document root 디렉토리에 보관된 파일을 처리함
/var/www/html
기본적으로 루트에서 소유함.


설치 완료되면 방화벽 설정
```
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```




> 인용문 입니다
>> 인용문 안 인용문
>>> 인용문 안 인용문 안 인용문

<u> 밑줄 </u>

<mark>형광팬</mark>

**볼드체**
