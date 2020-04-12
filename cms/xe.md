# XE

## XE 특강 메모

* 날짜 : 2020.04.12 
* 수업 목적 : 추후 HTML, CSS, JS를 이용하여 XE, 워드프레스, 카페24쇼핑몰, 그누보드 등을 이용하여 어떤식으로 상용화 사이트를 제작하며 프리랜서가 창업을 할 수 있는지에 대한 가이드라인 제시

### 1. 웹서버와 데이터베이스의 개념 소개 및 환경 세팅

![](../.gitbook/assets/image%20%285%29.png)

#### 웹서버와 데이터베이스

* 웹서버 : 창고 관리인
* DB : 정보가 들어가는 창고
  * DB종류
    * MySQL, MsSQL, ORACLE - 테이블 형식
    * MongoDB - JSON 형식, 데이터 수신에 반응함 \(소켓IO\) - ex. 채팅 기능에 구현

#### 환경 세팅

1. 비트나미 WAMP 다운로드\(Development버전이 아닌 것으로\)
   * WAMP : window + 아파치 + MySQL + PHP \(맥은 MAMP\)
2. 설치하는거 제일 아래있는거 빼고체크 해제

#### CMD로 직접 명령하기

데이터베이스 xe전용 테이블 설치 순서

1. CMD창열기
2. `cd C:\Bitnami\wampstack-7.2.29-2\mysql\bin` \(MySQL 실행폴더로 이동\)
3. \`mysql -uroot -p\[비밀번호\]
4. `create database [테이블 명];`
5. `show databases;`

**mySQL 명령어**

* `mysql -uroot -p비번` \(세미콜론없이 엔터\) :mysql 접속
* 데이터베이스 확인
  * `show databases;` \(s붙이는거, 세미콜론 필수\)
* 데이터베이스\(database\) 생성과 삭제
  * `create database <database명>`
  * `drop database <database명>`
* 테이블\(table\) 생성과 삭제
  * `create table <table명>`
  * `drop table <table명>`
* 데이타베이스 선택
  * `use csi2;`
* 테이블 생성하는 구문

  ```text
  create table members(
  num int not null auto_increment,
  id char(20),
  pass char(20),
  name char(12),
  mail varchar(80),
  primary key(num)
  );
  ```

* 필드값 추가
  * `alter table members add mail char(50);`
* 필드값 제거
  * `alter table members drop mail;`
* 필드값 수정
  * `alter table board change 바꿀필드명  바뀔필드명  자료형  not null;`
* 테이블 확인
  * `show tables;`
* 테이블의 구조
  * `desc 테이블 이름;`
* 테이블의 데이터를 꺼내서 확인하는거
  * `select * form 테이블 이름;`

#### 기타

* 실제 닷홈이나 cafe24에서는 마리아DB로 되어있음. \(MySQL이랑 같은거임\)
* CMD는 명령 프롬프트\(CLI\)

### 2. XE소개 및 설치

#### XE 소개

* 싼 건 : XE \(더 편하다\)
* 비싼건 : 워드프레스

기능은 차이가 없고, XE가 작업 난이도가 워드프레스의 1/3정도 워드프레스는 php 지식 필요.

* 자유게시판 기능, 로그인 기능

#### XE 설치

1. XE1 다운로드 \(ver1.11.5\)
   * \([https://xe1.xpressengine.com/index.php?mid=download&package\_id=18325662&detail=release](https://xe1.xpressengine.com/index.php?mid=download&package_id=18325662&detail=release)\)
2. 루트 폴더 안에 xe 넣기
3. 한국어 -&gt; 동의 -&gt; 설치 진행 -&gt; MySQLI -&gt; DB아이디, DB이름 : root -&gt; 다음 -&gt; 메일주소, 비밀번호, 닉네임, 아이디

### 3. XE의 구조 및 스킨 제작 방법 소개

1. 주소 : localhost/xe/admin
2. 고급 &gt; 설치된 모듈
   * 페이지, 게시판 즐겨찾기 등록

### 4. DB연동이 되는 게시판 페이지 만들기

#### 게시판 만들기

사이트 메뉴 편집 &gt; Welcome Page제외 모두 삭제

#### 페이지만드는 방법

### 5. 내가 만든 HTML, CSS, JS 작업물 XE에 얹기

1. 원하는 태그가들어간 파일 만들기 \(확장자는 .php\)
2. xe폴더 안쪽에 넣기
3. 외부페이지로 페이지 만들기
4. 만든 php폴더를 외부 문서 위치에 경로 입력

* index.html이 아니라 layout.html로 바꿔야 함.
* html, head, body태그 등 삭제
* 불러오는 소스는 load태그로 통일
* 로그인 연동 붙이기 : 고급 &gt; 설치된 위젯 &gt; 코드 생성
* 로그인필요한 태그에 붙여넣기 하고 저장
* layouts라는 폴더 안에 넣기
* gnb태그넣고, 관리자페이지. 사이트디자인 설정 &gt; 메뉴설정 \(conf폴더가 있어야 함\)

외부파일 호출

```markup
<load target="js/custom.js" />
```

GNB-XE 연동코드

```markup
<ul id="gnb">
<li loop="$main_menu->list=>$key1,$val1" class="on"|cond="$val1['selected']">
<a href="{$val1['href']}" target="_blank"|cond="$val1['open_window']=='Y'">{$val1['link']}</a>
<ul cond="$val1['list']">
<li loop="$val1['list']=>$key2,$val2" class="active"|cond="$val2['selected']">
<a href="{$val2['href']}" target="_blank"|cond="$val2['open_window']=='Y'">{$val2['link']}</a>
</li>
</ul>
</li>
</ul>
```

메인, 서브 분리코드

```markup
<!--@if($mid=='index')-->
    메인페이지에 출력될 코드
<!--@else-->
   서브페이지에 출력될 코드
<!--@end-->
```

