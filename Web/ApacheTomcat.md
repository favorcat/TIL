# Apache Tomcat
### macOS에서의 Apache Tomcat을 사용하기
1. [Tomcat 설치방법](#Tomcat을-설치하는-2가지-방법)
2. Tomcat 실행 및 종료 방법
    * [다운로드로 설치한 Tomcat](#다운로드로-설치한-Tomcat-실행-및-종료하는-방법)
    * [Homebrew로 설치한 Tomcat](#Hombrew로-설치한-Tomcat-실행-및-종료하는-방법)
4. [페이지 꾸미는 방법](#localhost8080의-페이지-꾸미는-방법)

### Tomcat을 설치하는 2가지 방법
1. [원하는 버전의 tar.gz 파일을 다운받아 설치](#원하는-버전을-다운받아-설치하는-방법)
2. [Homebrew를 이용한 설치](#Hombrew를-이용한-설치)

---
### 원하는 버전을 다운받아 설치하는 방법
[Apache Tomcat 다운로드](http://tomcat.apache.org/)
1. Apache Tomcat 사이트에서 원하는 버전의 tar.gz 파일을 다운받는다.
2. 다운받은 파일을 압축해제하여 해제한 폴더를 데스크탑 폴더로 옮긴다.
3. 터미널을 실행시켜 아래의 명령어를 차례로 입력한다.
```
sudo mkdir -p /usr/local 
sudo mv ~/Desktop/<압축해제한 폴더명> /usr/local 
sudo rm -f ~/Library/Tomcat 
sudo ln -s /usr/local/<압축해제한 폴더명> /Library/Tomcat  
sudo chown -R <맥북 user id> /Library/Tomcat  
sudo chmod +x /Library/Tomcat/bin/*.sh 
```
#### 다운로드로 설치한 Tomcat 실행 및 종료하는 방법
1. 해당 명령어를 실행한다.
```
sudo /Library/Tomcat/bin/startup.sh
```
2. 브라우저에 *http://localhost:8080* 를 입력해서 Tomcat의 사진이 나오면 제대로 실행된 것이다.
3. Tomcat 서버를 종료하려면 아래의 명령어를 입력한다.
```
sudo /Library/Tomcat/bin/shutdown.sh
```   



---
### Hombrew를 이용한 설치

1. 터미널을 실행시켜 아래의 명령어를 차례로 입력한다.
2. brew를 업데이트한다.
```
Brew update
```
3. brew에서 tomcat을 찾는다
```
Brew search tomcat
```
4. list에 tomcat이 가장 최근버전이니 tomcat을 설치한다.
```
Brew install tomcat
```
5. tomcat이 설치된 것을 확인한다.
```
Brew list
```

#### Hombrew로 설치한 Tomcat 실행 및 종료하는 방법
1. Tomcat이 설치된 경로는 */usr/local/Cellar/* 폴더에 있다.
2. 해당 경로에서 ls로 목록을 보면 ‘Tomcat’ 폴더가 있으며, 그 폴더에 들어가면 Tomcat의 버전명으로 된 폴더가 존재한다.
3. Tomcat을 실행하기 위해서는 해당 디렉터리로 이동한다.
```
cd /usr/local/Cellar/tomcat/버전명/bin
```
4. 디렉토리에 이동한 후에 실행을 위한 명령어를 입력한다.
```
./catalina start
```
5. 성공적으로 실행이 된 것을 확인하기 위해서는 *http://localhost:8080* 를 입력해서 Tomcat의 페이지가 나오면 성공이다.
6. 종료를 원할 때에는 아래의 명령어를 입력한다.
```
./catalina stop
```   



---
### localhost:8080의 페이지 꾸미는 방법
```
/usr/local/Cellar/tomcat/버전명/libexec/webapps/ROOT
```
해당 폴더로 가면 localhost:8080으로 페이지를 띄웠을 때 나오는 소스들이 존재한다.   
페이지를 꾸미고 싶다면 코드파일을 해당 폴더에 저장하여 사용하면 된다.
