## 작업 시나리오

Discuz!는 전 세계에서 완성도 및 커버율이 가장 높은 포럼 웹 사이트 소프트웨어 시스템 중 하나로, 200여만 명의 웹 사이트 사용자를 보유하고 있으며, 귀하도 Discuz!를 통해 포럼을 구축할 수 있습니다. 본 문서는 Tencent Cloud CVM에서 Discuz! 포럼 구축 및 그에 필요한 LAMP(Linux + Apache + MariaDB + PHP)환경 구축에 대해 소개합니다.


Discuz! 포럼 수동 구축을 위해 자주 사용하는 커맨드인 [CentOS 환경에서 YUM을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2046) 등의 Linux 커맨드에 익숙해져야 하며, 설치된 소프트웨어의 사용 및 버전 호환성에 대한 이해도가 있어야 합니다.

## 소프트웨어 버전(예시)
본 문서 중 구축한 Discuz! 포럼 소프트웨어의 구성 버전 및 설명은 다음과 같습니다.
- Linux: Linux 운영 체제의 경우, 본 문서는 CentOS 7.5를 예시로 사용합니다.
- Apache: Web 서버의 경우, 본 문서는 Apache 2.4.15를 예시로 사용합니다.
- MariaDB: 데이터베이스의 경우, 본 문서는 MariaDB 5.5.60를 예시로 사용합니다.
- PHP: 스크립트 언어의 경우, 본 문서는 PHP 5.4.16을 예시로 사용합니다.
- Discuz!: 포럼 웹 사이트 소프트웨어의 경우, 본 문서는 Discuz! X3.2를 예시로 사용합니다.


## 작업 순서
### 1단계: CVM 로그인
- [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 기타 로그인 방식을 선택하실 수 있습니다.
- [원격 로그인 소프트웨어로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)



### 2단계: LAMP 환경 구축 

CentOS 시스템에 대해 Tencent Cloud는 CentOS와 동기화된 소프트웨어 설치 소스를 제공하고 있어, 포함되어 있는 소프트웨어 모두 현재로써 가장 안정적인 버전으로, 직접 Yum을 통해 빠르게 설치할 수 있습니다.

<span id="InstallNecessarySoftware"></span>
#### 설치 구성 필수 소프트웨어
1. 다음 명령어를 실행하여 필수 소프트웨어(Apache, MariaDB, PHP)를 설치합니다.
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server -y
```
2. 다음 명령어를 실행하여 서비스를 시작합니다.
```
systemctl start httpd
systemctl start mariadb
systemctl start php-fpm
```
3. <span id="step3"></span>root 사용자가 데이터베이스에 액세스할 수 있도록 다음 명령어를 실행하여 root 계정 비밀번호 및 기본 환경을 설정합니다.
>
>- MariaDB 에 처음 로그인 하기 전, 다음 명령어를 실행하여 사용자 비밀번호 및 기본 설정으로 이동합니다.
>- 처음 root 계정 비밀번호를 입력한 후 엔터 키(root 비밀번호 설정 시 인터페이스는 기본으로 나타나지 않음)를 누르고 다시 입력하여 확인합니다. 인터페이스 상의 알림을 통해 기본 설정을 완료합니다.
> 
```
mysql_secure_installation
```
4. 다음 명령어를 실행하여 MariaDB에 로그인하고 [3단계](#step3)에서 설정한 비밀번호를 입력한 후 "**Enter**"를 누릅니다.
```
mysql -u root -p
``` 
방금 설정한 비밀번호를 입력하여 MariaDB 에 로그인 되면 제대로 설정되었음을 뜻합니다. 아래 그림 참조.
![](https://main.qcloudimg.com/raw/e22b91cc30bf4155436ab398ee44502a.png)

5. 다음 명령어를 실행하여 MariaDB 데이터베이스를 종료합니다.
```
exit
```

#### 환경 설정 검증

환경 구축 성공 여부를 확인 및 보장하기 위해 아래의 작업을 통해 검증할 수 있습니다.
1. 다음 명령어를 실행하여 Apache의 기본 루트 디렉터리 `/var/www/html`에서 `test.php` 테스트 파일을 생성합니다.
```
vim /var/www/html/test.php
```
2. "**i**"를 눌러 편집 모드로 바꾸고 다음 콘텐츠를 작성합니다.
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3. "**Esc**"를 누르고 "**:wq**"를 입력하여 파일을 저장한 뒤 돌아갑니다.
4. 브라우저에서 해당 `test.php`파일에 액세스하고 환경 설정 성공 여부를 조회합니다.
```
http://CVM의 공인 IP/test.php 
```
다음 페이지가 나타나면 LAMP 환경 설정 성공을 의미합니다.
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)



<span id="InstallDiscuz"></span>
### 3단계: Discuz! 설치 및 설정  

#### Discuz! 다운로드 
다음 명령어를 실행하여 설치 패키지를 다운로드 합니다.
```
wget http://download.comsenz.com/DiscuzX/3.2/Discuz_X3.2_SC_UTF8.zip
```

#### 설치 준비 작업
1. 다음 명령어를 실행하여 설치 패키지를 압축 해제합니다.
```
unzip Discuz_X3.2_SC_UTF8.zip
```
2. 다음 명령어를 실행하여 압축 해제 한 "upload" 폴더 내의 모든 파일을 `/var/www/html/`로 복사합니다.
```
cp -r upload/* /var/www/html/
```
3. 다음 명령어를 실행하여 쓰기 권한을 기타 사용자에게 부여합니다.
```
chmod -R 777 /var/www/html
```

#### Discuz! 설치
1. Web 브라우저 주소창에 Discuz! 사이트의 IP 주소(즉 CVM 인스턴스의 공인 IP 주소)를 입력하면 Discuz! 설치 인터페이스를 바로 확인할 수 있습니다. <!--아래 그림 참조
![설치 1](https://mc.qcloudimg.com/static/img/ad97b179b5b4977d86ca09a78ef05a7d/image.png)-->
2. [동의]를 클릭하여 설치 환경 확인 페이지로 이동합니다. <!--아래 그림 참조
![설치2](https://mc.qcloudimg.com/static/img/c5a521673ed6f1a3528ba67ca5886ee4/image.png)-->
3. 현재 상태가 정상임을 확인한 후, [다음 단계]를 클릭하여 실행 환경 설정 페이지로 이동합니다. <!--아래 그림 참조
![설치 3](https://mc.qcloudimg.com/static/img/11a44bd86bfdfcd1fe3dcce6e8f200e6/image.png)-->
4. 새로 설치를 선택하고 [다음 단계]를 클릭하여 데이터베이스 생성 페이지로 이동합니다. <!--아래 그림 참조
![설치 4 수정](https://mc.qcloudimg.com/static/img/5d5184cfb34f98d791c243273b910065/image.png)-->
5. 페이지 알림에 따라 정보를 작성하여 Discuz!를 위한 1개의 데이터베이스를 생성합니다.
>
>- [필수 소프트웨어 설치](#InstallNecessarySoftware)에서 설정한 root 계정과 비밀번호를 이용해 데이터베이스에 연결하고 시스템 메일함, 관리자 계정, 비밀번호와 Email을 설정하세요.
>- 자신의 관리자 아이디와 비밀번호를 기억하세요.
>
6. [다음 단계]를 클릭하여 설치를 시작합니다.
6. 설치 완료 후 [귀하의 포럼이 설치 완료되었습니다. 이곳을 클릭하여 액세스하세요]를 클릭하면 바로 포럼에 액세스할 수 있습니다. <!--아래 그림 참조
![설치 5](https://mc.qcloudimg.com/static/img/41dab1ec86120a565bdd790238f271da/image.png)-->


## FAQ
CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참조하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [비밀번호 및 키](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참조할 수 있습니다.
- CVM 네트워크 문제는 [IP 주소](https://intl.cloud.tencent.com/document/product/213/17285), [포트 및 보안 그룹](https://intl.cloud.tencent.com/document/product/213/2502)을 참조할 수 있습니다.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/document/product/213/17351)를 참조할 수 있습니다.
 
