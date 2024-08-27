# `시프트` - `모이소`

해커그라운드 해커톤에 참여하는 `시프트` 팀의 `모이소`입니다.

## 참고 문서

> 아래 두 링크는 해커톤에서 앱을 개발하면서 참고할 만한 문서들입니다. 이 문서들에서 언급한 서비스 이외에도 더 많은 서비스들이 PaaS, SaaS, 서버리스 형태로 제공되니 참고하세요.

- [순한맛](./REFERENCES_BASIC.md)
- [매운맛](./REFERENCES_ADVANCED.md)

## 제품/서비스 소개

<!-- 아래 링크는 지우지 마세요 -->
[제품/서비스 소개 보기](TOPIC.md)
<!-- 위 링크는 지우지 마세요 -->

## 오픈 소스 라이센스

<!-- 아래 링크는 지우지 마세요 -->
[오픈소스 라이센스 보기](./LICENSE)
<!-- 위 링크는 지우지 마세요 -->

## 설치 방법

> **아래 제공하는 설치 방법을 통해 심사위원단이 여러분의 제품/서비스를 실제 Microsoft 애저 클라우드에 배포하고 설치할 수 있어야 합니다. 만약 아래 설치 방법대로 따라해서 배포 및 설치가 되지 않을 경우 본선에 진출할 수 없습니다.**

### Paas 서버 구축 및 웹 배포 방법

### 사전 준비 사항
Azure(Microsoft의 클라우드 서비스)의 대표 서비스인 PaaS의 정석, AppService(제품 이름입니다)로 PaaS서버를 구축하려고 했다.
<img width="1470" alt="스크린샷 2024-08-26 오후 7 50 22" src="https://github.com/user-attachments/assets/956953c0-12fa-4747-9881-6e5d13002cac">
먼저, https://portal.azure.com/ 에서 App Service 리소스를 생성할 것이다.
검색창에 App Service를 검색한다.

App Service에서 ‘만들기’ > ‘웹 앱’를 클릭한다.
(home에 원하는 리소스 서비스가 없을 경우에는 리소스 만들기를 눌러 원하는 리소스를 검색하여 찾을 수 있다.)

![image](https://github.com/user-attachments/assets/ab28ab4f-4350-4a0d-898f-115ffb191557)
![image](https://github.com/user-attachments/assets/24100634-c23d-48d5-a2e5-1a4555f6b5fa)
위와 같이 정보를 입력해준다.

중요한 것은 리소스그룹을 [Hackers Ground](https://portal.azure.com/#blade/HubsExtension/ResourceMenuBlade/id/%2Fsubscriptions%2Fbfa39d86-1058-4824-8074-e9d283d6c321) 로 설정하는 것이고, 

구독 : Hackers Ground

리소스 그룹 : (본인의 리소스 그룹 , 나는 **rg-team---shift** )

인스턴스 정보를 입력해준다. (내 기준으로 적어봤다.)

이름 : 원하는 이름으로 (본인은 moiso-server)

게시 : 코드 

런타임 스택 : Java 17 

Java 웹 서버 스택 : Java SE (Embedded Web Server)

운영체제 : Linux

지역 : Korea South

다음은, ‘검토+만들기’를 클릭 한다. 마지막으로 검토페이지에서 설정들을 확인한 후 ‘만들기’를 선택한다. (와이파이 이슈를 조심하자)

## Github와 Azure로 배포하기

**먼저 배포를 위한 자격 증명을 설정**한다.
'리소스로 이동'을 클릭한다.
![361386257-9115206b-987d-46aa-bc48-c0f099f8b7a2](https://github.com/user-attachments/assets/a9711782-b1f7-4320-bfb7-aa27ad92d170)
위에 빨간박스로 네모친 곳을 눌러서 bash(맥,윈도우 둘다 bash로하면된다.) 로 들어간다. 

<img src="https://github.com/user-attachments/assets/fe8e8062-ee3b-463d-a79c-fcc336b23db8" alt="description" width="300"/>

만약 위 화면이 뜬다면 (Hackers Ground)를 선택하고, ‘스토리지 계정이 필요하지 않음’을 선택. ‘기존 프라이빗 가상 네트워크 사용’ 이거는 체크할 필요없다.
```
az webapp deployment user set --user-name (username) --password (password)
```
를 넣는다. ((username),(password)에 자신의 에저 username[사용자 이메일],password를 넣어라)

![image](https://github.com/user-attachments/assets/9115206b-987d-46aa-bc48-c0f099f8b7a2)
위와 같이 뜨면 성공이다!

이제부터 깃허브에 백엔드 코드를 등록하고 git actions을 활용하여 paas 서버를 구축해볼 것이다.
먼저, 코드를 올릴 깃허브 레포지토리를 파주겠다.

서버를 배포할 코드가 올라간 레포지토리가 필요하다.
아래 링크를 클릭한다.
https://github.com/heunseoRyu/Moiso_test

<img width="1470" alt="스크린샷 2024-08-26 오후 10 40 53" src="https://github.com/user-attachments/assets/6a48aaeb-c4d2-437d-9ccb-424b928e31ce">
빨간색으로 표시한 곳을 클릭한다.
<img width="1470" alt="스크린샷 2024-08-26 오후 10 42 19" src="https://github.com/user-attachments/assets/b6550d67-85d3-49c0-a588-2244e208de7e">
'Choose an owner'를 자신의 프로필로 설정하고 레포지토리 이름을 설정하고 설명은 생략한다. 'Create fork'를 눌러준다.
그러면 moiso 레포지토리가 복제되어 나만의 레포지토리가 되었다.

마지막으로 에저로 돌아가 맨처음에 갔던 App Service에서 자신의 AppService를 클릭,
<img width="1470" alt="스크린샷 2024-08-26 오후 11 02 24" src="https://github.com/user-attachments/assets/e0bd0a9a-5b80-42e7-bda5-642ebe2069d3">

설정 > 구성으로 가준다.
<img width="1470" alt="스크린샷 2024-08-26 오후 11 03 08" src="https://github.com/user-attachments/assets/781c86dc-e211-4749-b0d9-4da1f71f866d">
![image](https://github.com/user-attachments/assets/c4c630bb-d884-4bef-a49e-0d4fc53c4595)

‘시작 명령’을
```
java -jar /home/site/wwwroot/*.jar --server.port=80
```
로 설정해준다. 저장을 누르고, 업데이트까지 기다린다.

이제 코드파일과 Azure App Service까지 준비가 되었다.

<img width="1470" alt="스크린샷 2024-08-26 오후 11 44 22" src="https://github.com/user-attachments/assets/a756420b-af81-42a1-9120-663e9b4bef2e">
배포 > 배포센터 > 설정 으로 간다.

![image](https://github.com/user-attachments/assets/57f6350a-ccbd-48a9-8f50-c5151b07d006)
소스 : Github

'다음으로 로그인'에서 파란글씨를 눌러 본인의 깃허브 username(깃허브아이디)을 설정합니다.

개인레포지토리 이므로 조직에서 hackersground-kr 대신 username을 선택해준다.
방금 만든 리포지토리를 선택한다.

분기는 main으로 설정.

![image](https://github.com/user-attachments/assets/1d1c0f1b-d824-4921-be9b-4547f49aa8ee)
구독에서 Hackers Ground를 설정하고 ID는 (새로 만들기) 로 둔다.

이후 위에 있는 ‘저장’ 버튼을 누른다. 

배포가 성공적으로 진행되기 전까지 기다린다.

![image](https://github.com/user-attachments/assets/ffdbe3de-8f39-41bd-9788-5a98acf690b5)

가 뜨면 깃허브로 가본다. 

yml 파일이 .github/workflows/main_(app service이름).yml 의 경로로 생성이 되었을 것이다.
사진으로 보면 아래와 같다. 
<img width="1470" alt="스크린샷 2024-08-26 오후 11 09 14" src="https://github.com/user-attachments/assets/4a80ff84-ec7c-4fa8-acec-7b100b754e4e">
빨간박스로 표시한 폴더를 누르면 main_(app service이름).yml 파일이 있을 것이다.
<img width="1470" alt="스크린샷 2024-08-26 오후 11 11 20" src="https://github.com/user-attachments/assets/cc726f5a-0339-4b85-9d93-100902656d38">
위에 빨간박스로 표시한 부분을 클릭해서 파일을 수정하는 페이지로 넘어간다.

그렇다면, 이제부터 이 파일을 조금 변경할 것이다.


```
name: Build and deploy JAR app to Azure Web App - moiso-server

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
     
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Java version
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'microsoft'

      - name: Build with Gradle
        run: ./gradlew bootJar

      - name: Upload artifact for deployment job
        uses: actions/upload-artifact@v4
        with:
          name: java-app
          path: build/libs/*.jar

	deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'Production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}
    permissions:
      id-token: write #This is required for requesting the JWT

    steps:
      - name: Download Artifact
        uses: actions/download-artifact@v4
        with:
          name: java-app

      - name: Login to Azure
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZUREAPPSERVICE_CLIENTID_BC9EAE9B21F84B8BA153374854069D0F }}
          tenant-id: ${{ secrets.AZUREAPPSERVICE_TENANTID_2A578BDF6BB546C595AA77734DDA2CFF }}
          subscription-id: ${{ secrets.AZUREAPPSERVICE_SUBSCRIPTIONID_CC15C906548443F5B44D168292F19DEC }}

      - name: Deploy to Azure Web App
        id: deploy-to-webapp
        uses: azure/webapps-deploy@v3
        with:
          app-name: 'moiso-server'
          slot-name: 'Production'
          package: '*.jar'
```
위 코드를 파일에 복붙하자. 그러나, 띄어쓰기가 중요하기 때문에 아래 링크의 코드를 복사하는 것도 방법이다.
https://github.com/heunseoRyu/MOISO_BACKEND/blob/main/.github/workflows/main_moiso-server.yml

🚨 
## 1. 다만, 조건이 있다.
위에 코드에서 secrets. 뒤에 있는 값들
```
	with:
          client-id: ${{ secrets.AZUREAPPSERVICE_CLIENTID_BC9EAE9B21F84B8BA153374854069D0F }}
          tenant-id: ${{ secrets.AZUREAPPSERVICE_TENANTID_2A578BDF6BB546C595AA77734DDA2CFF }}
          subscription-id: ${{ secrets.AZUREAPPSERVICE_SUBSCRIPTIONID_CC15C906548443F5B44D168292F19DEC }}
```
AZUREAPPSERVICE_CLIENTID_BC9EAE9B21F84B8BA153374854069D0F,AZUREAPPSERVICE_TENANTID_2A578BDF6BB546C595AA77734DDA2CFF,AZUREAPPSERVICE_SUBSCRIPTIONID_CC15C906548443F5B44D168292F19DEC 세개는 복붙을 할때 내 기존 코드에서 가져와야 한다.
(그게 어디있는데요?)
```
- name: Login to Azure
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.__clientidsecretname__ }}
          tenant-id: ${{ secrets.__tenantidsecretname__ }}
          subscription-id: ${{ secrets.__subscriptionidsecretname__ }}
```
  이 부분을 찾고 __clientidsecretname__,__tenantidsecretname__,__subscriptionidsecretname__는 메모장에 기록한 후
```
	with:
          client-id: ${{ secrets.AZUREAPPSERVICE_CLIENTID_BC9EAE9B21F84B8BA153374854069D0F }}
          tenant-id: ${{ secrets.AZUREAPPSERVICE_TENANTID_2A578BDF6BB546C595AA77734DDA2CFF }}
          subscription-id: ${{ secrets.AZUREAPPSERVICE_SUBSCRIPTIONID_CC15C906548443F5B44D168292F19DEC }}
```
내가 방금 제시한 코드의 AZUREAPPSERVICE_CLIENTID_BC9EAE9B21F84B8BA153374854069D0F,AZUREAPPSERVICE_TENANTID_2A578BDF6BB546C595AA77734DDA2CFF,AZUREAPPSERVICE_SUBSCRIPTIONID_CC15C906548443F5B44D168292F19DEC 세부분을 순서대로 방금 기록한 __clientidsecretname__,__tenantidsecretname__,__subscriptionidsecretname__로 대신하여 넣는다.

## 2. 다만, 조건이 있다.
```
- name: Deploy to Azure Web App
        id: deploy-to-webapp
        uses: azure/webapps-deploy@v3
        with:
          app-name: 'moiso-server'
          slot-name: 'Production'
          package: '*.jar'
```
복사한 코드의 app-name 부분을 ⭐️ 나의 App Service 이름 ⭐️으로 설정해주어야 한다.
<img width="1470" alt="스크린샷 2024-08-27 오전 12 20 36" src="https://github.com/user-attachments/assets/7099e550-ac16-4e73-a779-1641a3e525b5">


<img width="1470" alt="스크린샷 2024-08-26 오후 11 52 06" src="https://github.com/user-attachments/assets/6d61683b-2b04-4f34-8843-ef8d3b3b59d9">
수정 완료했으면 빨간 부분으로 표시한 'Commit changes...'를 누른다.

<img width="1470" alt="스크린샷 2024-08-26 오후 11 59 23" src="https://github.com/user-attachments/assets/28ff27fb-8ba4-49c0-b370-43b38297499f">
누르면 위와 같은 화면이 나온다. 위에 빨간색으로 표시한 Actions를 클릭한다.

<img width="1470" alt="스크린샷 2024-08-27 오전 12 01 00" src="https://github.com/user-attachments/assets/37851403-fb60-4bab-8082-df33193211ed">
가장 상단에 있는 기록을 누른다.

![image](https://github.com/user-attachments/assets/467e2350-b49b-400b-b601-92d6342119af)
상당시간 기다려야 한다. 이렇게 체크가 뜨면 성공이다. 


배포되었는지 확인
![image](https://github.com/user-attachments/assets/348d8769-c7b2-4888-ba67-8a1da80fe038)
이 도메인을 사용할거다.

![image](https://github.com/user-attachments/assets/3bf7b555-a078-4ac0-a5bd-c9e33bf53dfe)
웹브라우저에서 검색해도 응답을 볼 수 있다!

웹도 함께 배포됩니다.
아래 경로로 검색해보시면 들어가집니다.
https://moiso-server-hzeae2hhbchmexcc.eastus-01.azurewebsites.net

만약에 내가 배포한 도메인으로 접속해보고 싶으면
moiso-server-hzeae2hhbchmexcc.eastus-01.azurewebsites.net 부분을 자신의 도메인으로 바꿔주세요!

