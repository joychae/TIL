20210302\_TIL
==============
웹개발 미니프로젝트 2화_VScode, Git 세팅 및 사용
----------------------------------------

-   개발을 위한 가상환경세팅과 협업을 위한 깃허브 사용에 예상보다 시간이 많이 소요되었다. 계속 사용하다보니 같은 에러가 반복되는 경우가 많았다. 반복해서 사용하다보면 능숙해질것 같다.

-    PyCharm을 사용하고 있었는데, 현업에서 Visual Studio를 많이 사용하기도 하고 프로그램 자체가 가벼워서 개발 툴을 Visual Studio로 변경하게 되었다. Framework나 Library Setting이 PyCharm보다 시각적으로 구현되지 않았다는 점이 가장 큰 차이점이다. 때문에 불편하다 느낄 수도 있지만 익숙해지면 VIsual Studio가 더 편리한 것 같다.

-   Git bash를 사용해 깃을 Commit, Push, Pull을 하며 팀원들과 협업했다. 물론 그 과정에서 많은 에러가 발생하였다. 뜻하지 않게 Git의 Branch 개념을 학습하고 Rebase와 Merge까지 다뤄보게 되었다.
---


### **1. PyCharm에서 Visual Studio로의 전환**

>[Visual Studio Code 파이썬(Python) 가상개발환경(venv) 셋팅](https://mr-spock.tistory.com/19)

>[Flask로 웹 페이지 제작하기 - 1 기초적인 설정과 사용법, Visual Studio Code와 Flask 설치법](https://hobbylists.tistory.com/entry/Flask-Flask%EB%A1%9C-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%A0%9C%EC%9E%91%ED%95%98%EA%B8%B0-1-%EA%B8%B0%EC%B4%88%EC%A0%81%EC%9D%B8-%EC%84%A4%EC%A0%95%EA%B3%BC-%EC%82%AC%EC%9A%A9%EB%B2%95-Visual-Studio-Code%EC%99%80-Flask-%EC%84%A4%EC%B9%98%EB%B2%95-%EA%B0%9C%EC%9D%B8%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8)

-   PyCharm에서 Virtual Studio로 넘어오면서 Flask부터 세팅을 다시 해야 했다. 위의 두 블로그를 참고하여 진행하였는데 많은 도움이 되었다.  

-   Venv 설정 후 terminal에 pip install flask, pip install requests등 pip install ~~~ 의 형태로 직접 기입하여 라이브러리를 설치한다.  

-   라이브러리를 설치하다 보면 자주 발생하는 error 중 하나가 pip를 최신 버전으로 업그레이드 하지 않아서 생기는 문제이다. 에러 메세지를 읽고 pip upgrade 관련 문제가 발생한다면 다음 링크를 참조하자.    

>[Python 패키지 pip 업그레이드, upgrade 방법](https://webisfree.com/2017-08-10/python-%ED%8C%A8%ED%82%A4%EC%A7%80-pip-%EC%97%85%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9C-upgrade-%EB%B0%A9%EB%B2%95)

---

**20210306 수정**

VS code 가상환경 세팅  

Terminal은 Select Default Sell > Git bash 설정  
```
py - V  

py -m venv venv  

source venv/Scripts/activate  
```
하면 가상환경 세팅이랑 작동이 간편하게 끝난다.  

어떤 환경은 py 대신 python 써야 한다.  

내 컴퓨터는 python 안먹히고 py 로 사용해야 작동한다.  

이 글을 보시는 분들은 py 안되면 python으로 시도해보시길 바란다.

---


### **2. Git Commit, Push and Pull**

**1) 깃 커밋**
```
git add .

git commit -m ' 커밋명'
```
이렇게 치면 커밋 완료! Push 전에 Commit을 먼저 해야 한다

**2) 깃 Push**
```
git push origin '브랜치명'
```
입력한 브랜치로 깃이 업로드 된다. origin은 리모트 명이다. origin으로 대게 사용하기는 하지만, 리모트명이 다르다면 해당하는 리모트명을 작성해야 Push가 제대로 이루어진다.

**3) 깃 Pull**
```
git pull orgin '브랜치명'
```
해당하는 위치의 깃이 내 로컬파일에 다운로드 된다.

**4) Error**

- Push 관련 이슈
 
>   너무 다양한 에러 (혹은 마음처럼 동작안함)이 발생했다.  
>>1.  Push가 잘 되던 Local Clone이 다른 팀원 Push 후에 Push가 안되기도 하였다. 한참 삽질하다가 결국 git reset하고 처음부터 경로를 설정했다.  
>>2.  remote와 repository 경로를 잃어버려 한참 헤멨다. 같은 맥락에서 main branch에 업로드 하고 싶은데 master branch에만 계속 업로드가 되었다.  
>>3.  Branch라는 개념에서 파생되어 Merge, Rebase 기능들이 있는데 이 역시 잘 사용하지 않으면 에러 발생 가능성이 높다. Rebase 같은 경우 사용하면 내 Local Clone이 Rebase 상태에 머물러 있게 되는데, 이 때 Pull이 진행되지 않았다.   git rebase --abort 하면 Rebase 상태 강제종료가 가능하다.  
>>4.  Pull 해올 때 venv 파일까지 건드려지지 않도록 항상 조심하자. 다른 팀원의 venv 파일을 pull한 후 클라이언트와 서버가 연결되지 않아서 애먹었다. 결국 pull을 취소하고 이전 내 커밋으로 돌아가고나서야 작동이 되었다. 현재 프로젝트 깃 레포지토리에 venv 파일이 올라가 있는데 원래는 venv파일은 뺴고 업로드를 하는 건지 알아봐야겠다.  
>>5.  그래서 주말에 공부할 것들은 다음과 같다. 1) Git Commit, Pull, Push 개념 정리, 2) Git Remote, Branch 개념 정리, 3) Git Merge, Rebase 기능들 개념 정리, 4) 다른 사람들이 올려놓은 Repository 구경하기  