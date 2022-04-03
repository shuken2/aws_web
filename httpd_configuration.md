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


**부팅 시 자동 시작되도록설정**
```
sudo chkconfig httpd on
chkconfig --list httpd 
또는
systemctl list-unit-files|grep -i httpd
```

**Web 80 포트 접속용 Security Group설정**
* 유형 : HTTP
* 프로토콜 : TCP
* 포트범위 : 80
* 소스 : 사용자지정

-- Apache httpd는 Apache document root 디렉토리에 보관된 파일을 처리함
/var/www/html
기본적으로 루트에서 소유함.


*ec2-user 계정에서 이 디렉터리의 파일을 조작할 수 있게 하려면 디렉터리의 소유권과 권한을 변경해야 함.
*ec2-user를 apache그룹에 추가하여 apache그룹에 /var/www 디렉터리의 소유권을 부여하고 쓰기 권한을 할당.


**파일 권한설정**
1) 사용자(ec2-user)를 apache 그룹에 추가
```
[ec2-user ~]$ sudo usermod -a -G apache ec2-user
```
2) 로그아웃 후 다시 로그인,  새그룹 선택하고 멤버쉽 확인.
```
exit
이후 재 로그인
[ec2-user ~]$ groups
ec2-user wheel apache
[ec2-user ~]$ sudo chown -R ec2-user:apache /var/www
```
3) 그룹 쓰기 권한을 추가하여 나중에 하위 디렉터리에 대한 그룹ID 설정하려면 /var/www 와 그 하위 디렉터리의 디렉터리 권한을 변경
```
[ec2-user ~]$ sudo chmod 2775 /var/www
[ec2-user ~]$ find /var/www -type d -exec sudo chmod 2775 {} \;
```
4) 그룹 쓰기 권한을 추가하려면 /var/www 및 그 하위 디렉터리의 파일 권한을 반복하여 변경.
```
[ec2-user ~]$ find /var/www -type f -exec sudo chmod 0664 {} \;
```
---
## 2. index.html 설정
```
[ec2-user ~]$ cd /var/www/
[ec2-user ~]$ vi index.html
<html>
<head>
    <meta charset='utf-8'>
    <meta http-equiv='X-UA-Compatible' content='IE=edge'>
    <title>Welcome aws test page</title>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <link rel='stylesheet' type='text/css' media='screen' href='main.css'>
    <script src='main.js'></script>
</head>
<body>
    <h1> Welcome to the AWS world!! </h1>
    <div id="get-html-from-other-s3"></div>
  </body>
</html>
```

이후 httpd 서비스 재시작
```
sudo service httpd restart
```

웹브라우저에서 접속
```
http://인스턴스퍼블릭IPv4주소/index.html
```

--







## 아래는 MarkDown 구문 샘플 ##
---

설치 완료되면 방화벽 설정
```
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```
---

> 인용문 입니다
>> 인용문 안 인용문
>>> 인용문 안 인용문 안 인용문

<u> 밑줄 </u>

<mark>형광팬</mark>

**볼드체**
