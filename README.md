# TIL


mobilestyle="widthContent"|||_##]

**20210301\_TIL**

-   개발 프로젝트 실행 전 계획짜기에 필요한 요소들을 알 수 있었다.
-   필요 요소들은 1) 프로젝트명, 2) 와이어프레임, 3) 개발해야 하는 기능들을 리스트업, 4) 협업을 위한 깃헙 레포지토리 생성이다. 직접 진행하며 각각의 요소들에서 현재 부족한 점들을 알 수 있었다.
-   아래 팀과 함께 일한 결과물들과 함께 좀 더 구체적으로 기록해두었다.

#### **1) 프로젝트명**

-   프로젝트명: 모두의 산 (가제)
-   기능 소개: 미리 크롤링해 놓은 등산로 정보를 기반으로, 유저들이 각각의 산을 선택해 등산 후기를 남길 수 있는 등산 후기 공유 플랫폼

#### **2) 와이어프레임 구성**

-   간단한 화면 구성에 해당하는 작업이다. 웹 서비스가 가지고 있는 모든 페이지에 와이어 프레임이 각각 대응되도록 만들어야 한다. 와이어프레임 페이지 수 = html 파일 수로 구성했다.
-   이번 프로젝트는 한 개의 메인페이지, 한 개의 로그인 페이지, 두 개의 세부 서비스 페이지로 구성했다.
-   HTML <div>에 해당하는 요소들이 와이어 프레임 내 하나의 box로 그려지는 기준으로 box를 생성했다.
-   HTML TAG 안에 어떠한 text가 들어가야 하는지 대략적인 내용을 기입하였다.

[##_Image|kage@bDBOrf/btqYN02s3G6/WiijGd7W4ZkXSTDutIiRnk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="300" data-ke-mobilestyle="widthContent"|||_##]

[##_Image|kage@5WgSF/btqY2tCcL0e/evgkCVRNeKbKs1vY9bvGo0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="300" data-ke-mobilestyle="widthContent"|||_##]

#### **3) API 설계 - 개발해야 하는 기능 리스트업**

[##_Image|kage@cq4TWw/btqYW2FbjsY/N3wReEJfgKp3ubCVj4yp6k/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|첫 API 설계||_##]

-   화면이 전환되는 onclick 액션을 기준으로, 팀원별로 어떤 기능 개발을 맞을 지 나눠보았다. 개발 프로젝트 협업은 처음인지라 각자 개발할 부분들을 어떻게 나눌지 가장 감이 안 오는 부분이었다. 코드가 유기적으로 연결되어야 하는 부분들이 많기에, 최대한 연결되어있지 않는 기능들부터 잘라 역할을 분배해보았다.
-   구현 기능들을 어느 level 까지 쪼개서 작성해야 잘 작성된 API 설계인지 궁금해졌다. 따로 API 설계를 검색해서 공부할 예정이다.
-   request 부분과 response 부분 작성이 많이 미흡하다. 이 부분은 대게 어떤 형태로 작성되는지 알아보는 게 중요할 것 같다. (코드를 다 작성할 수는 없으니까!)
-   메인 페이지 설계와 공통변수 설정이 미흡하다. 협업 진행 시 처음부터 변수를 통일해 진행하는 게 효율적일 것 같은데, API 설계에 어떻게 잘 표현해야 할지 연구해봐야겠다.

#### **4) 협업을 위한 깃헙 레포지토리 생성**

-   프로젝트를 위해 유용한 협업툴인 깃헙 레포지토리를 생성했다.
-   아래는 이번 프로젝트를 위해 생성한 깃허브 레포지토리 url 링크이다.
-   [github.com/joychae/hh99\_Webproject\_w1.git](https://github.com/joychae/hh99_Webproject_w1.git)
