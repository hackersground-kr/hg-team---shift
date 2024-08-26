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

App Service에서 ‘만들기’ > ‘웹 앱 만들기’를 클릭한다.
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
![image](https://github.com/user-attachments/assets/9115206b-987d-46aa-bc48-c0f099f8b7a2)
위에 빨간박스로 네모친 곳을 눌러서 bash(맥이라서 bash고, windows유저는 powerShell로하면된다.) 로 들어간다. 
<img src="https://github.com/user-attachments/assets/fe8e8062-ee3b-463d-a79c-fcc336b23db8" alt="description" width="300"/>
만약 위 화면이 뜬다면 (Hackers Ground)를 선택하고, ‘스토리지 계정이 필요하지 않음’을 선택. ‘기존 프라이빗 가상 네트워크 사용’ 이거는 체크할 필요없다.
```
az webapp deployment user set --user-name (username) --password (password)
```
를 넣는다. ((username),(password)에 자신의 에저 username[사용자 이메일],password를 넣어라)

이제부터 깃허브에 백엔드 코드를 등록하고 git actions을 활용하여 paas 서버를 구축해볼 것이다.
먼저, 코드를 올릴 깃허브 레포지토리를 파주겠다.

![image](https://github.com/user-attachments/assets/68d83fde-1c2b-473d-b3f0-831f4184dc24)
레포지토리를 하나 생성한다.

(Add a README file의 체크는 하지 않는다.)

그렇다면, 올릴 코드가 필요하다.
아래 링크를 클릭하면 백엔드 코드 압축 파일이 있다. 다운받는다.
https://drive.google.com/file/d/14xv_sbteeGJNQH65f8lIpEANZdpCeQqc/view?usp=sharing

터미널로 방금 다운받은 나의 백엔드 코드파일에 접근할 것이다.

일단, 다운로드 받은 파일의 압축을 푼다.

터미널(윈도우는 cmd)을 연다.

![image](https://github.com/user-attachments/assets/94b69ff9-1613-4f17-b908-bbd7d1b698ed)
```
ls // 현재위치의 폴더.파일 리스트 보기
cd Downloads // Downloads(다운로드) 폴더위치로 이동한다.
```
![image](https://github.com/user-attachments/assets/dffdccc5-c5bf-4575-87f3-0a9ad76e6903)

여기서
```
cd moiso // moiso 백엔드 코드 폴더로 현재 위치 변경
```
![image](https://github.com/user-attachments/assets/594a86d0-a54c-4cf1-a5d8-42a7deeed6f2)
화면처럼 현재 위치가 정해졌다면.
```
git init
git remote -v // 현재 로컬 레포가 연결된 원격 레포 확인 , 아무것도 나오지 않으면 연결 가능
// git remote remove origin // 만약, 레포가 존재한다면
git remote add origin <방금 만든 레포의 링크>

// 코드 올리기
git add .
git commit -m '커밋메세지'
git push origin main
```
(깃허브 설치하는법)
윈도우
1. Git 다운로드 페이지에 접속합니다.
2.Windows용 Git 설치 파일을 다운로드합니다.
3.설치 파일을 실행한 후, 기본 설정을 그대로 두고 "다음"을 계속 클릭합니다.
4.설치가 완료되면 Git Bash 또는 명령 프롬프트에서 Git을 사용할 수 있습니다.
맥OS
```
brew install git
```
위 코드를 순서대로 쳐라.

마지막으로 App Service에서 설정 > 구성으로 가준다.

‘시작 명령’을
```
java -jar /home/site/wwwroot/*.jar --server.port=80
```
로 설정해준다. 저장을 누르고, 업데이트까지 기다린다.

이제 코드파일과 Azure App Service까지 준비가 되었다.

배포 > 배포센터 > 설정 으로 간다.

![image](https://github.com/user-attachments/assets/57f6350a-ccbd-48a9-8f50-c5151b07d006)
소스 : Github

다음으로 로그인에서 들어가 로그인을 통해 본인의 username을 설정합니다.

개인레포지토리 이므로 조직에서 hackersground-kr 대신 username을 선택해준다.
방금 만든 리포지토리를 선택한다.

분기는 main으로 설정.

![image](https://github.com/user-attachments/assets/1d1c0f1b-d824-4921-be9b-4547f49aa8ee)
구독에서 Hackers Ground를 설정하고 ID는 (새로 만들기) 로 둔다.

이후 위에 있는 ‘저장’ 버튼을 누른다. 

배포가 성공적으로 진행되기 전까지 기다린다.

![image](https://github.com/user-attachments/assets/ffdbe3de-8f39-41bd-9788-5a98acf690b5)

가 뜨면 깃허브로 가본다. 

grade.yml 파일이 .github/workflows/main_(app service이름).yml 이렇게 생성이 되었을 것이다.

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
위 코드를 파일에 복붙하자. 그러나, 띄어쓰기가 중요하기 때문에 해당 링크의 코드를 복사하는 것도 방법이다.
https://github.com/heunseoRyu/MOISO_BACKEND/blob/main/.github/workflows/main_moiso-server.yml

![image](https://github.com/user-attachments/assets/467e2350-b49b-400b-b601-92d6342119af)

이렇게 둘다 체크가 뜨면 성공이다.

![image](https://github.com/user-attachments/assets/c4c630bb-d884-4bef-a49e-0d4fc53c4595)

배포되었는지 확인
![image](https://github.com/user-attachments/assets/348d8769-c7b2-4888-ba67-8a1da80fe038)
이 도메인을 사용할거다.

![image](https://github.com/user-attachments/assets/3bf7b555-a078-4ac0-a5bd-c9e33bf53dfe)
웹브라우저에서 검색해도 응답을 볼 수 있다!

웹도 함께 배포됩니다.
아래 경로로 검색해보시면 들어가집니다.
https://moiso-server-hzeae2hhbchmexcc.eastus-01.azurewebsites.net/web/upload-article
https://moiso-server-hzeae2hhbchmexcc.eastus-01.azurewebsites.net/web/sign-in

만약에 내가 배포한 도메인으로 접속해보고 싶으면
moiso-server-hzeae2hhbchmexcc.eastus-01.azurewebsites.net 부분을 자신의 도메인으로 바꿔주세요!

## 시작하기

> **여러분의 제품/서비스를 Microsoft 애저 클라우드에 배포하기 위한 절차를 구체적으로 나열해 주세요.**
