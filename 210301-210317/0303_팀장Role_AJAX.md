20210303\_TIL
==============
웹개발 미니프로젝트 3화_와이어프레임, API 설계
----------------------------------------

-   한 사람이 코드의 중심을 잡고 가져가야 한다. static, templates 폴더를 생성한 후에 필요한 페이지 수를 계산해 HTML 파일들을 생성한다. 그리고 이를 app.py에 연동시켜 놓는 작업까지 해서 깃헙에 첫 commit을 만드는 것까지가 맨 처음 업무다.  

-   중간중간 gitHub branch들을 관리하면서 최종적으로는 파일 병합 업무까지의 책임이 있다. 첫 프로젝트부터 팀장이 되어 해당 업무들을 하고 있다. 경영전략 컨설팅 프로젝트를 할 때에도 한 사람이 Project Manager가 되어 전체 로직들을 도맡아 관리하게 되는데, 개발 프로젝트도 비슷하게 진행되는 듯하다. Project Manager 경험이 몇 번 있어서 팀장 업무 적응이 크게 어렵지는 않았다.  

-   프로젝트 완성일이 촉박해 원래 계획했던 서비스에서 SpecOut을 했다. 우선, 가장 까다로운 크롤링 작업 후 데이터 GPS 변환을 제거하였다. 대신, 사용자들이 직접 데이터를 기입할 수 있고 이를 보여주는 방식으로 변경하였다. 데이터를 긁어오는 것에서 직접 기입하는 방식으로 SpecOut이 진행되었다.  

-   SpecOut 한 후의 주요 기능들은 다음과 같다. 1) 로그인, 2) 웹서비스 상 지도 구현, 3) 사용자가 기입한 데이터를 데이터베이스에 저장한 후 이를 보여주는 것. 나는 이 중 2)번과 3)번을 맡아 진행하였다. 로그인이 아무래도 새로 배우는 template을 이용한 기능인지라, 로그인 부분에 다른 팀원들의 workload를 많이 할당하였다.  

-   2) 웹서비스 상 지도 구현은 네이버 OPEN API를 활용하는 방법으로 지도를 불러와 웹사이트에 구현하였다. 과정에서 key 값을 받아 코드에 적용하는 법 등을 익혔다.  

-   3) 사용자가 기입한 데이터를 데이터 베이스에 저장하고 보여주는 것은 AJAX와 requests의 insert, find 기능을 이용해 구현하였다.  

---


### 1\. 팀장 업무

첫째, 우선 기본 폴더와 파일들을 만든다.  

둘째, 클라이언트와 서버 통신을 확인한다.  

```python
@app.route("/")
def home():
    return render_template("01_main.html")
```
localhost:5000을 주소창에 입력해 01\_main.html 파일이 잘 나타나는지 확인한다.  

html 파일이 여러개라면 각 파일들마다 /@@@ 형태로 url을 지정하고, html 페이지를 할당한 뒤 localhost:5000/@@@이 잘 작동하는지 확인한다.  

셋째, 페이지 전환이 일어나는 부분들을 확인한 후 페이지 전환 기능을 넣는다.  

```python
<div class ="banner">
    <a href ="/login" class="login">로그인</a>
```

페이지 전환 버튼을 미리 만들어 놓고 href를 사용해 페이지 전환 기능을 넣은 후 각 페이지별 전환이 잘 되는지 확인한다. 기본 뼈대가 완성되었다! 팀원들이 각 페이지 안의 기능에만 집중할 수 있도록 중간지대(?)에 위치한 기능들을 미리 구현하는 방식이다.  

---


### 2\. 네이버 지도 API 사용

[NAVER Maps API v3](https://navermaps.github.io/maps.js.ncp/docs/)

네이버 지도 API 기술문서이다. 공식문서를 꼼꼼히 읽는 버릇을 들이고 있다.  

우선, 네이버 클라우드 플랫폼에 회원가입 한 뒤 지도 API 이용 신청이 필요하다.  

인증아이디를 발급받고 안내에 따라 html template을 사용하면 된다.  

이 부분에 대해서는 나중에 따로 자세히 포스팅 할 예정이다.  

---


### 3\. AJAX, requests

원래는 Selenium을 이용해 웹사이트를 스크래핑 하고 Geocoding을 이용해 스크래핑 된 데이터를 GPS 값으로 변환해 지도에 띄울 생각이었다. 다만, 셀레니움 조작이 미숙하여 고난이도의 크롬브라우저 조작을 통한 스크래핑을 시간안에 완성시키지 못할 것이라 판단하였다.  

따라서 정해진 시간까지 최대한 셀레니움으로 시도를 해 보되, 구현되지 않으면 데이터를 받아오는 대신 사용자들이 직접 기입할 수 있는 방향으로 스펙아웃을 하기로 결정했다. 첫 프로젝트이고, 따라서 프로토타입이라 생각하고 욕심을 버리고 완성에 초점을 맞춰야 한다고 판단했기 때문이다.  

```javaScript
        function postArticle() {
            let usertitle = $('#post-usertitle').val()
            let user = $('#post-user').val()
            let url = $('#post-url').val()
            let comment = $('#post-comment').val()

            $.ajax({
                type: "POST",
                url: "/memo",
                data: { usertitle_give: usertitle, user_give: user, url_give: url, comment_give: comment },
                success: function (response) { // 성공하면
                    alert(response["msg"]);
                    window.location.reload()
                }
            })
        }
```

우선, 사용자들이 직접입력한 정보를 서버에 보내는 자바스크립트 코드이다. post-url과 post-comment라는 id를 가진 입력창에 입력된 변수를 각각 url과 comment 변수로 받는다.  

지정된 url과 comment 변수들이 각각 url\_give와 comment\_give로 POST 되어짐을 알 수 있다. POST는 클라이언트에서 서버로 '보내는 것'이라 이해하였다.  

```python
## API 역할을 하는 부분
@app.route("/memo", methods=["POST"])
def saving():
    usertitle_receive = request.form["usertitle_give"]
    user_receive = request.form["user_give"]
    url_receive = request.form["url_give"]
    comment_receive = request.form["comment_give"]

    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36"
    }
    data = requests.get(url_receive, headers=headers)

    soup = BeautifulSoup(data.text, "html.parser")

    image = soup.select_one('meta[property="og:image"]')["content"]
    title = soup.select_one('meta[property="og:title"]')["content"]
    desc = soup.select_one('meta[property="og:description"]')["content"]

    doc = {
        "usertitle": usertitle_receive,
        "user": user_receive,
        "image": image,
        "title": title,
        "url": url_receive,
        "desc": desc,
        "comment": comment_receive,
    }
    db.articles.insert_one(doc)

    return jsonify({"msg": "저장이 완료되었습니다."})
```

클라이언트에서 보낸 입력값을 서버에 저장하는 파이썬 코드이다. 자바스크립트에서 url\_give와 comment\_give로 변수를 설정해 보낸 값들이 url\_receive, comment\_receive형태로 변환되어 받아짐을 확인할 수 있다.  

이를 doc 형태로 담아서 insert 해주면 MongoDB에 저장이 된다. 이로써 사용자가 전달한 데이터는 서버에 저장이 된다.  

```python
## HTML을 주는 부분
@app.route("/memo", methods=["GET"])
def listing():
    articles = list(db.articles.find({}, {"_id": False}))
    return jsonify({"all_articles": articles})
```

이제 저장한 데이터를 클라이언트가 요청하면 보낼 수 있게 '찾아서' 리스트 형태로 만들어두어야 한다. 위의 코드는 서버에 저장된 정보 중 필요한 정보를 검색해 클라이언트에게 보내는 파이썬 코드이다. GET은 클라이언트가 서버에서 '받는 것'이라 이해하였다. 처음엔 GET과 POST가 헷갈리는데, 둘 다 클라이언트 입장이라고 정의해두면 덜 헷갈린다.  

find를 사용해 조건에 맞는 데이터를 찾고 "all\_articles"라는 이름으로 준비해두었다.  

```javaScript
        function showArticles() {
            $.ajax({
                type: "GET",
                url: "/memo",
                data: {},
                success: function (response) {
                    let articles = response['all_articles']
                    for (let i = 0; i < articles.length; i++) {
                        let usertitle = articles[i]['usertitle']
                        let title = articles[i]['title']
                        let user = articles[i]['user']
                        let image = articles[i]['image']
                        let url = articles[i]['url']
                        let desc = articles[i]['desc']
                        let comment = articles[i]['comment']
                        temp_html = `
                        <div class="card">
                            ...
                            </div>`

                        $('#cards-box').append(temp_html)
                    }
                }
            })
        }
```

위의 코드는 서버가 검색해서 보내준 데이터를 브라우저에서 볼 수 있게 해주는 자바스크립트 코드다.  

서버가 "all\_articles"라는 이름으로 보내준 리스트에서 반복문을 돌려 값들을 변환한다. 이렇게 변환된 여러 값들을 append 라는 api로 붙여주면 끝이다.  