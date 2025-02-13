---
layout: 
title: "github 블로그 만들기"
---
# 웹 호스팅이란
내가 만든 페이지를 모든 사람이 보게 하려면 웹서버를 설치하고 외부로 전송할 수 있게 만들어야 한다.
하지만 쉽지 않기 때문에 그 역할을 대신해 주는게 웹 호스팅이다.

<br/>
<br/>

<img src= "https://user-images.githubusercontent.com/58356031/142229623-ca5d93dd-474a-431c-9552-c1f98ef16565.png" width="600">

###### 출처:생활코딩

내가 만든 index.html를 github의 호스팅을 이용한다. 파일 업로드를 하면 깃허브의 서버 컴퓨터가 활성화되며 모든 사람이 볼 수 있는 주소를 알려준다.

<br/>
<br/>

<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fejitoq%2FbtqCgnl0z4K%2FwCoVdf98LWXxaXOMZM1NX1%2Fimg.png" width="600">

###### 출처:생활코딩

내 사이트의 주소를 다른 사람들에게 알려주면 그 사람들은 그 주소로 깃허브 서버에 있는 웹서버에 접속해 index.html을 볼 수 있는 방법이다.

<br/>
<br/>

# 깃 허브 블로그 만들기
개인이 웹서버를 운영하기엔 너무나 많은 제약이 있다. 따라서 웹 호스팅을 대신해 주는 여러 방법이 있는데 그중 하나가 Github pages를 이용하는 것이다.

Github pages는 깃허브에서 제공하는 Static website로 Github repository에 리소스를 push 하는 것만으로도 간단한 웹사이트를 만들 수 있게 도와준다. 간단하게 만들어진 블로그에서 repository에 Markdown 문법을 이용하여 간단하게 포스팅을 할 수 있다.

Github pages는 단순히 사이트 생성을 담당하는 호스팅 플랫폼이기 때문에 마크다운 문법을 블로그화하기 위해서는 site generator 프레임워크가 필요하다.

static site generator 종류는 Jekyll, hexo, hugo 등이 있는데 본인은 자체 내부적으로도 작동되고 있다는 Jekyll 를 이용하기로 했고 Jekyll 테마 중 minimal-mistakes를 fork 받아서 블로그를 만들었다.
> static website 란? 미리 저장된 파일들이 그저 서버를 통해 제공되기만 하는 형태의 사이트를 말한다.

<br/>
<br/>

# Minimal-Mistakes 디렉터리 구조
Jekyll 구조를 기반으로 각 테마마다 조금씩 차이가 있다. 내가 사용하고 있는 Minimal-Mistakes의 디렉터리 구조를 알아봤다.

<br/>
<br/>

### 주요 파일 모음
- [_data 폴더](https://unnokid.github.io/first/#_data-%ED%8F%B4%EB%8D%94)
- [_includes 폴더](https://unnokid.github.io/first/#_includes-%ED%8F%B4%EB%8D%94)
- [_layouts 폴더](https://unnokid.github.io/first/#_layout-%ED%8F%B4%EB%8D%94)
- [_sass 폴더](https://unnokid.github.io/first/#_sass-%ED%8F%B4%EB%8D%94)
- [_assets 폴더](https://unnokid.github.io/first/#_assets-%ED%8F%B4%EB%8D%94)
- [_config.yml](https://unnokid.github.io/first/#_configyml)
- [index.html](https://unnokid.github.io/first/#indexhtml)


### _data 폴더
테마를 커스터마이징 하기 위한 데이터 파일들이 모여있는 폴더이다. 사이트에 사용할 데이터를 적절한 포맷으로 정리하여 보관하는 디렉터리이다.
이 디렉터리에 `.yml` `.yaml` `json` `csv` `tsv` 등 파일들을 둔다면 이 파일들을 자동적으로 읽어서 `site.data`로 사용 할 수 있다.

예로 `member.yml` 파일이 있다면 site.data.member로 입력하여 그 파일을 사용할 수 있다.
폴더 기본 하위로는 상단 메뉴바를 커스터마이징 할 수 있는 `navigation.yml` 와 각국 언어별로 어떤 텍스트로 표시되는지를 나열한 문서 `ui-text.yml`이 있다.

<br/>
<br/>

### _includes 폴더
많이 재사용 되는 html 파일들을 모아 둔 폴더이다. 예로 댓글, 카테고리, 태그, 비디오, head, 등등 블로그에 자주 쓰이거나 항상 보이는 공통된 컴포넌트들을 담은 코드들만 모아둔 폴더이다.

필요에 따라 Liquid 언어의 태그로 포스트나 레이아웃에 _includes 폴더 내의 코드를 쉽게 삽입하여 재사용 할 수 있다.


- analytic-providers

어떤 analytics  플랫폼을 사용할지 고르는 폴더로 보통은 구글 analytics 을 사용한다. custom.html에 설정을 다르게 하면 다른 analytics 사용으로 변경 가능
> 구글 애널리틱스는 웹사이트 방문자의 데이터를 수집해서 분석함으로써 온라인 비즈니스의 성과를 측정하고 개선하는 데 사용하는 웹로그분석 도구

- comments-providers

어떤 댓글 플랫폼을 사용할 것인지 결정하는 폴더로 마찬가지로 다른 댓글 플랫폼을 사용하고 싶다면 custom.html에 코드를 추가하면 된다.

- footer, head

폴더에 들어있는 custom.html 에 커스터마이징 내용을 적으면 된다.

- search

어떤 검색 엔진을 사용하는가를 지정 가능하다. 우선 _config.yml에 search:true값으로 변경해 주어야 한다.
디폴트 검색 엔진은 `Lunar` 이며 본인 입맛대로 검색 엔진을 만들 수 있다.

- nav_list

메뉴 상단 바 리스트를 만들 수 있다.

- video

비디오(유튜브) 등을 embeding 해준다.
예시로 %include video id = "xxxx xxxx" provider="youtube"% 이런 식으로 삽입 가능하다. ({}추가하면 됨)

<br/>
<br/>

### _layout 폴더
페이지마다 디자인과 직접적으로 연결된 전체적인 레이아웃으로 템플릿을 위한 코드들 한곳에 보관할 수 있게 해준다.
따라서 모든 페이지에 반복적으로 입력하지 않고 _inclde 폴더 안에 부분적인 html들이 존재해서 이를 불러오는 부분이 많다.

기본 레이아웃은 default.html 이 사용된다. 대부분 레이아웃 html들이 `layout: default` 값을 담고 있다.
따라서 포스트에 layout: archive만 해줘도 상속구조이기때문에 위에 레이아웃을 부르고 불러서 렌더링이 된다.

<br/>
<br/>

### _sass 폴더
minimal-mistakes.scss에 import 할 수 있는 scss 파일들을 모아 둔 폴더이다.
minimal-mistakes.scss는 최종적으로 _assets/css/main.scss에 import 된다. 하는 역할은 블로그와 컴포넌트들을 시각적으로 디자인하는 스타일 시트 파일들이다.

<br/>
<br/>

### _assets 폴더
main.scss가 들어가는 폴더와 이미지 파일, java script 파일들이 들어가 있다.

<br/>
<br/>

### _config.yml
블로그를 구성하기 위한 기본적인 설정값이다.

<br/>
<br/>

### index.html
블로그 처음 홈페이지이다.


