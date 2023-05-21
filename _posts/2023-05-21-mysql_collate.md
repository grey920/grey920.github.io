---
title: "바닐라 아이스크림 알러지가 있는 자동차를 만난 썰 (feat.MySQL)"
excerpt: "충격 실화. 엔지니어라면 한번쯤 만나는 그 바닐라 아이스크림 알러지가 있는 자동차를 만난 썰 푼다"
categories:
    - Server
tags:
  - MySQL
  - collation
  - MySQL 대소문자 구분
  - 글또
toc: true
toc_sticky: true
toc_label: "바닐라 아이스크림 알러지가 있는 자동차를 만난 썰"
toc_icon: "edit"
# classes: wide
header:
  teaser: 'https://www.motorgraph.com/news/photo/202204/29791_94109_5738.jpg' #/assets/images/2022-01-02/Untitled.png
---

## 바닐라 아이스크림 알러지가 있는 자동차
<img alt="image" src="https://www.motorgraph.com/news/photo/202204/29791_94109_5738.jpg">
여러분은 '바닐라 아이스크림 알러지가 있는 자동차' 이야기를 아시나요? 

GM사의 폰티악 부서에 고객불만 사항이 하나 접수되었습니다. 다른 종류의 아이스크림에는 문제가 없었지만 유독 바닐라 아이스크림을 사기만 하면 차에 돌아왔을때 시동이 걸리지 않는다는 내용이었습니다. <br>
점검하러 나간 엔지니어는 모든 종류의 데이터를 종합하여 결국 해당 가게의 **상품 배치 형태** 때문임을 밝혀내었습니다. 바닐라 아이스크림은 가장 인기있는 품목이었기에 상대적으로 계산하고 차로 돌아오기까지 다른 맛들에 비해 시간이 적게 걸렸습니다. 이로인해 바닐라 향을 살 때에는 엔진이 아직 너무 뜨거워 베이퍼락이 해소되지 못한 상태였기에 시동이 잘 걸리지 않았던 것입니다. <br>

엔지니어 썰중에서 제가 가장 좋아하는 이야기인데요. 이게.. 실제로 나타났습니다(?!)
오늘은 제가 만난 바닐라 아이스크림 알러지가 있는 자동차 이야기를 해볼까 합니다.


## 문제상황
언제부터인가 개발중인 프로젝트에서 테스트를 하다보면 이력을 쌓는 이벤트에서 10번에 한 번 정도 간헐적으로 `Duplicate Key`  에러가 발생하기 시작했습니다. 메뉴탭을 이동하면 메뉴 이력을 쌓고, 게시판을 보거나 수정하는 경우에도 게시판 조회이력과 수정이력을 쌓고 있어서 '이력을 쌓는 과정에서 로직상 두 번 도는게 있나..' 하는 의심을 했습니다. 하지만 디버깅을 해보고 로직을 샅샅히 봐도 insert문을 두 번 도는 로직은 없었습니다.
계속 테스트를 하다보니 이력 로직이 아닌 일반 insert 로직에서도 아주 **간헐적으로** Duplicate Key 에러가 발생했습니다. 이 때부터 이력 로직이 아니라 insert 자체에 뭔가 문제가 있구나, 하는 생각이 들었습니다.

일단 상황을 정리해보면, <br>
1) insert 하는 상황 중 **간헐적**으로 발생한다. <br>
2) id값은 내부에서 시간을 기반으로 만드는 UUID같은 유일한 값으로 중복될 확률이 거의 없다. ( 코어 시스템이라 여러 프로젝트에서 사용했지만 한 번도 중복된 적이 없다. ) <br>
3) 화면에서 API는 한 번만 호출한다. <br>
4) 로직 내에는 두 번 도는 상황이 없다. <br>

한 리퀘스트 내에서 두 번 돌지 않고, 화면에서도 리퀘스트를 단 한번만 호출하는데 DB에서 Duplicate key 에러가 발생한다라... 


## 로그를 열자 실마리가 열렸다
먼저 컨트롤러로 들어오는 엔트리 포인트를 확인해보기 위해 로그를 확인해보았습니다. 
그리고 Duplicate Key 에러가 발생한 ID를 검색해보았는데

음..? id값이 대문자인 값도 파일에 같이 있네..?
<img alt="image" src="https://github.com/grey920/obsidian_tech-note/assets/58028215/11d568ad-941a-4962-a96c-a8e69f274206">
<img alt="image" src="https://github.com/grey920/obsidian_tech-note/assets/58028215/1ff5a960-5876-43b2-8c7c-5120e2dbb0b5">

정상적으로 동작한 리퀘스트의 로그를 확인해보니 해당 ID 하나만 파일에 존재합니다. 
<img alt="image" src="https://github.com/grey920/obsidian_tech-note/assets/58028215/44f9e194-1341-4fef-ae32-448d9e9388ea">

이쯤되니 불안합니다.. 대소문자가 다르면 다른 ID인건데,, 설마??

데이터의 대소문자 구분을 안해...??


## 모든건 MySQL 때무니야
일단 라고 외쳐봅니다. 

현재 프로젝트의 DB 스펙은 MySQL 8.0.31을 사용하고 있습니다. 
MySQL 8은 기본 캐릭터 셋이 latin-1에서 **utf8mb4**로 변경되었습니다. 그리고 이에 맞게 `collation`도 latin1_swedish_ci에서 **utf8mb4_0900_ai_ci**로 변경되었습니다.( [참고](https://www.lesstif.com/dbms/mysql-8-character-set-collation-91947077.html) )

### 콜레이션이요..? 'utf8mb4_0900_ai_ci'은 뭔데 이렇게 길죠 ?????
`Collation` 은 character 간의 **정렬**을 의미하며, 크게 2가지로 나뉩니다.
1. binary collation
	- 문자를 인코딩된 바이너리 스트림 값으로 문자를 비교합니다.
	- a와 A는 코드가 다르기 때문에 다른 문자로 인식됩니다. 즉, **대소문자를 구별할 수 있습니다.**
2. case-insensitive collation
	- 대소문자를 같은 문자로 다룹니다.
	- 이후에 인코딩으로 비교합니다. 
	- **general_ci**, **unicode_ci**


`utf8mb4_0900_ai_ci`은 나눠서 살펴보면 다음과 같습니다.
- utf8mb4 : 각 character가 최대 4byte UTF8 인코딩을 지원한다 (*이모지* 처리 가능)
- 0900 : Unicode 의 collation algorithm 9.0.0 을 지원 (가장 최신의 유니코드 표준).
- ai : accent insensitivity. 그래서 다음 문자들은같은 문자로 취급함(e, è, é, ê and ë)
- ci : **case insensitivity.** 그래서 p 와 P 를 같은 순서로 취급합니다


사용중인 mySQL 8에서는 기본적으로 데이터의 대소문자를 구분하지 않고 있었다는 겁니다..(!!!)
믿을 수 없어서(?) 확인해보도록 합니다.


### 적용된 collation 확인하기
#### collation, character set 확인하기
```sql
SHOW VARIABLES WHERE VARIABLE_NAME LIKE '%coll%' OR VARIABLE_NAME LIKE '%char%' OR VARIABLE_NAME='init_connect';
```
<img width="560" alt="image" src="https://github.com/grey920/obsidian_tech-note/assets/58028215/30e6b1ca-3b05-4f11-a17d-688c0e18d5e0">


#### 테이블의 컬럼 collation 확인하기
```
mysql> SHOW FULL COLUMNS FROM 테이블명;
```
<img alt="image" src="https://github.com/grey920/obsidian_tech-note/assets/58028215/d985e41e-82bd-45a7-a4da-f85bc0fa9de1">

이 놈이,, 맞군



## MySql 대소문자 구분 설정

테이블 생성시 해당 컬럼에 collate를 걸어줍니다.
```sql
create table tb_user
(user_oid varchar(11) binary not null auto_increment primary key,
user_id varchar(255),
name varchar(255) 
) engine=innodb;

OR

create table tb_collation_test
(user_oid varchar(11)  character set utf8mb4 collate utf8mb4_bin not null auto_increment primary key,
user_id varchar(255),
name varchar(255) 
) engine=innodb;
```

그러나 저처럼 이미 테이블과 값이 존재하는 경우 필요한 컬럼만 변경합니다.
```sql
alter table tb_user change user_oid user_oid varchar(11) binary not null
```



## 근데 왜 간헐적으로 발생했을까?
해당 프로젝트의 id는 시간을 기준으로 0~9A~Za~z 를 조합하여 ID를 생성하고 있습니다.

<img width="322" alt="image" src="https://github.com/grey920/obsidian_tech-note/assets/58028215/806894fe-3d90-40fd-800e-cb1cb8fa3c77">

메뉴 이력이나 게시판 조회 이력처럼 빈번하게 insert가 일어나는 경우 위에서 보는 것처럼 순서대로 id가 채번되다가 가장 마지막 영어 대문자가 26번째 후 소문자로 바뀌는 타이밍에서 같은 이력 테이블에 oid로 들어가게 되었고, DB에서는 대소문자를 구분하지 못해 같은 id로 인식하여 `Duplicate Key` 에러가 발생한 것입니다.


## 자나깨나 로그를 살펴보자
사실 처음부터 id로 로그를 살펴봤다면 좀 더 일찍 원인을 발견했을지도 모르겠다는 생각이 들었습니다..(머쓱) <br>
로그를 보기 전까지는 id는 완전 유니크한 값이라 db에서 절대 중복될 수가 없는데 어떻게 가능한 것인지에만 몰두해서 괜히 캐시나 트랜잭션같은 부분만 의심하고 있었는데,, ㅎㅎ<br>
어쨌든 이번 기회로 다시 한 번 정말 안풀리는 문제가 있을 땐,
1. 모든 기록, 특히 로그를 잘 살펴보자
2. 그리고 발상을 전환해보려 노력하자
이를 마음에 잘 새겨두어야 겠다는 생각을 하게 되었습니다..ㅎ 


## 출처(참고문헌)
- 적용된 collation 확인하기 : [ MySQL Character Set, Collation 확인](https://velog.io/@mooh2jj/MySQL-Character-Set-Collation-%ED%99%95%EC%9D%B8)