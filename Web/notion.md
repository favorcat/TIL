# 노션 공개 페이지에 도메인 연결하기

### 1. 노션 페이지 공유 활성화
1. 외부에 공유하고 싶은 노션 페이지를 `웹에서 공유` 활성화 한다.

### 2. Cloudflare에 도메인 추가
1. Cloudflare에 `Add a site`를 클릭해 자신의 도메인을 추가한다.
2. 요금제는 `Free`를 선택한다.
3. DNS records 입력 창에 다음과 같이 입력해준다.
    ```
    Type(형식) : CNAME
    Name(이름) : 서브 도메인명 (ex. nt)
    Target(대상) : notion.so
    ```
    하지만 나는 서브 도메인이 아닌 메인으로 쓰고싶기에 메인 도메인으로 설정했다.

### 3. 네임서버 변경
1. DNS 관리자 페이지 하단에 Clouldflare nameservers에 나와있는 네임서버를 확인한다.
2. 구입한 도메인(호스팅) 사이트로 가서 네임서버를 변경해준다.

### 4. Web Workers 세팅
1. CloudFlare의 Web Workers를 이용한다.
2. Worker 아이콘 클릭시, 보이는 `Manage Workers(Workers 관리)` 버튼을 클릭한다.
3. Workers 관리 페이지에서 `Create a Worker(Worker 생성)` 버튼을 클릭해 새로운 Workers를 생성한다.
4. Workers 이름을 `'notion-worker'`로 변경한다.
5. 스크립트 편집창에 아래 코드를 복사해서 붙여넣는다.
    
    ```script
    const MY_DOMAIN = "도메인 URL"
    const START_PAGE = "노션 공개 페이지 URL"
    addEventListener('fetch', event => {
        event.respondWith(fetchAndApply(event.request))
    })
    const corsHeaders = {
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "GET, HEAD, POST,PUT, OPTIONS",
        "Access-Control-Allow-Headers": "Content-Type",
    }
    function handleOptions(request) {
        if (request.headers.get("Origin") !== null &&
            request.headers.get("Access-Control-Request-Method") !== null &&
            request.headers.get("Access-Control-Request-Headers") !== null) {
            // Handle CORS pre-flight request.
            return new Response(null, {
                headers: corsHeaders
            })
        } else {
            // Handle standard OPTIONS request.
            return new Response(null, {
                headers: {
                    "Allow": "GET, HEAD, POST, PUT, OPTIONS",
                }
            })
        }
    }
    async function fetchAndApply(request) {
        if (request.method === "OPTIONS") {
            return handleOptions(request)
        }
        let url = new URL(request.url)
        let response
        if (url.pathname.startsWith("/app") && url.pathname.endsWith("js")) {
            response = await fetch(`https://www.notion.so${url.pathname}`)
            let body = await response.text()
            try {
                response = new Response(body.replace(/www.notion.so/g, MY_DOMAIN).replace(/notion.so/g, MY_DOMAIN), response)
                // response = new Response(response.body, response)
                response.headers.set('Content-Type', "application/x-javascript")
                console.log("get rewrite app.js")
            } catch (err) {
                console.log(err)
            }
        } else if ((url.pathname.startsWith("/api"))) {
            response = await fetch(`https://www.notion.so${url.pathname}`, {
                body: request.body, // must match 'Content-Type' header
                headers: {
                    'content-type': 'application/json;charset=UTF-8',
                    'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36'
                },
                method: "POST", // *GET, POST, PUT, DELETE, etc.
            })
            response = new Response(response.body, response)
            response.headers.set('Access-Control-Allow-Origin', "*")
        } else if (url.pathname === `/`) {
                let pageUrlList = START_PAGE.split("/")
            let redrictUrl = `https://${MY_DOMAIN}/${pageUrlList[pageUrlList.length-1]}`
            return Response.redirect(redrictUrl, 301)
        } else {
            response = await fetch(`https://www.notion.so${url.pathname}${url.search}`, {
                body: request.body, // must match 'Content-Type' header
                headers: request.headers,
                method: request.method, // *GET, POST, PUT, DELETE, etc.
            })
        }
        return response
    }
    ```
6. 위의 스크립트의 1행과 2행을 다음과 같이 수정한다.
서브도메인으로 하였을 경우, `nt.favorcat.dev`로 하면 된다.
    ```
    const MY_DOMAIN = "favorcat.dev"
    const START_PAGE = "https://www.notion.so/favorcat/Eunyeong-Ko-4c8974e378654f66a9ee19d8003bd62c"
    ```
7. 스크립트 코드 추가 및 수정을 완료한 후 `Save and Deploy(저장 및 배포)` 버튼을 클릭해 저장한다.
8. Clouldflare의 사이트 관리 메인 페이지에서 `Workers` 버튼 클릭 후 나오는 페이지로 이동한다.
9. Workers 페이지에 `Add Route(경로 추가)` 버튼 클릭해 Route(경로)와 Worker 항목을 아래와 같이 입력한다.
    ```
    Route : 도메인/* (ex. favorcat.dev/* , nt.favorcat.dev/*)
    Worker : Worker에서 저장했던 notion-worker 선택
    ```
