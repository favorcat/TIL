# Notion Mismatch between origin and baseUrl(dev) error 해결법

### 1. [fruitionsite](https://fruitionsite.com/) 접속
2. `Get Started` 부분의 `Step 2` 클릭한다.
3. `Your Domain` : favorcat.dev (연결한 도메인 주소)
4. `Notion URL for fruitionsite.com` : 노션 공유 링크
5. `COPY THE CODE` 클릭하여 복사해 준다.

### 2. CloudFlare 접속
1. CloudFlare의 Web Workers를 이용한다.
2. Worker 아이콘 클릭시, 보이는 `Manage Workers(Workers 관리)` 버튼을 클릭한다.
3. Workers 관리 페이지에서 생성했던 worker를 클릭한 후, 빠른 편집을 클릭한다.
4. 스크립트 편집창에 기존의 코드를 모두 지우고, 복사한 코드를 붙여넣기 하여 저장 및 배포를 한다.