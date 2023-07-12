## 소개

MongoDB 데이터 백업은 Tencent Cloud COS(Cloud Object Storage)가 [SCF(Serverless Cloud Function](https://intl.cloud.tencent.com/document/product/583)를 기반으로 사용자에게 제공하는 데이터베이스 백업 기능입니다. MongoDB CDB 파일을 COS에 장기적으로 저장하여 데이터 손실 및 손상을 방지합니다. 사용자가 지정 버킷에서 백업 함수 규칙을 설정하면 SCF는 정기적으로 MongoDB 백업 파일을 스캔하여 버킷에 파일을 저장합니다.

##  주의 사항

- MongoDB 데이터 백업 함수는 Tencent Cloud MongoDB 데이터베이스 백업 파일을 백업합니다. 기존에 MongoDB 데이터베이스 백업을 활성화하지 않은 경우 백업 함수를 실행할 수 없습니다. Tencent Cloud MongoDB 데이터베이스 백업에 대한 자세한 내용은 [TencentDB for MongDB 백업](https://intl.cloud.tencent.com/document/product/240/7108)을 참고하십시오.
- COS 콘솔에서 버킷에 MongoDB 데이터 백업 규칙을 추가한 적이 있는 경우 [SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)에서 기존에 생성한 MongoDB 데이터 백업 함수를 볼 수 있습니다. 이 함수를 삭제하지 **마십시오.** 삭제할 경우 규칙이 적용되지 않을 수 있습니다.
- 광저우, 상하이, 베이징, 청두, 중국홍콩, 싱가포르, 뭄바이, 토론토, 실리콘밸리 등 SCF를 런칭한 리전은 CDB 백업을 지원합니다. 지원 리전에 대한 자세한 내용은 [SCF 제품 문서](https://intl.cloud.tencent.com/document/product/583)를 참고하십시오.

## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 [애플리케이션 통합]을 클릭하여 [MongoDB 데이터 백업]을 찾습니다.
3. [백업 규칙 설정]을 클릭하여 규칙 설정 페이지로 이동합니다.
4. [함수 추가]를 클릭합니다.
>!
> SCF 서비스가 활성화되지 않은 경우 [SCF 콘솔](https://console.cloud.tencent.com/scf)에서 SCF 서비스를 활성화하고 안내에 따라 서비스 라이선스를 완료하십시오.
5. 팝업 창에서 다음과 같이 정보를 설정합니다.
![](https://main.qcloudimg.com/raw/f4591a75200593b0ee91cc27ccb589f6.png)
 - **함수 이름**: 함수의 고유 식별자로, 생성 후에는 수정할 수 없습니다. [SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)에서 해당 함수를 조회할 수 있습니다.
 - **연결 버킷**: MongoDB 백업 파일을 저장할 버킷입니다.
 - **트리거 주기**: MongoDB 데이터 백업 함수는 주기적인 트리거를 통해 백업 저장 작업을 트리거하며, 트리거 주기는 매일, 매주 및 사용자 정의 주기를 지원합니다.
 - **Cron 표현식**: 트리거 주기를 사용자 정의로 설정한 경우 Cron으로 구체적인 트리거 주기 규칙을 지정할 수 있습니다. Cron은 현재 베이징 시간인 UTC+8 중국 표준 시간(China Standard Time)을 기준으로 실행합니다. 정책 설정에 관한 상세 내용은 [Cron 관련 문서](https://intl.cloud.tencent.com/document/product/583/9708)를 참고하십시오.
 - **데이터베이스 인스턴스**: 현재 버킷이 속한 리전의 MongoDB 데이터베이스 인스턴스 리스트입니다.
 - **전송 경로**: 백업 파일의 전송 경로 접두사로, 입력하지 않은 경우 기본적으로 버킷의 루트 경로에 저장됩니다.
 - **SCF 라이선스**: MongoDB 데이터 백업은 MongoDB에서 백업에서 데이터베이스 인스턴스 및 백업 파일을 읽을 수 있는 권한을 SCF에 부여하여 백업 파일을 지정 버킷에 저장합니다. 따라서 해당 라이선스를 추가해야 합니다.
6. 설정을 추가한 후 [확인]을 클릭하면 추가된 함수를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/74eab5ca9a722e20fac6e1ca040ed8d3.png)
새로 생성한 함수에 다음과 같은 작업을 진행할 수 있습니다.
 - [로그 조회]를 클릭해 MongoDB 데이터 백업 기록을 조회합니다. 백업 시 오류가 보고된 경우 [로그 조회]를 클릭하고 SCF 콘솔에 리디렉션하여 로그 오류 상세 내용을 조회할 수 있습니다.
 - [편집]을 클릭하여 MongoDB 데이터 백업 규칙을 수정합니다.
 - [삭제]를 클릭하여 사용하지 않는 MongoDB 백업 규칙을 삭제합니다.

