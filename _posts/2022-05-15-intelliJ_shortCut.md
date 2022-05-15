---
title: "내가 보려고 정리하는 intelliJ 단축키 모음 (Mac OS)"
excerpt: "외울때까지 당분간은 계속 찾아보겠지,,,"
categories:
  - Tip
tags:
  - IntelliJ
  - 단축키
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# header:
  # teaser: /assets/images/2022-04-03/after.png
---
## 창 열기
- 액션 팁 보기 : Alt + Enter
- preferences 창 열기 : cmd + ,
- project structure 창 열기 : cmd + ;
- 좌측 패키지창 열기 : cmd + 1
  - cmd  + 숫자 로 다양한 창 열고 닫을 수 있음

### 툴팁
- 파라미터 정보 출력 : cmd + P
- 메소드 구현 부분을 창으로 띄워서 확인 : option + space 

## 검색
- 전체 검색 : shift + shift (연타)
  - 전체 파일 내 검색 : cmd + shift + F
- 최근에 작업한 파일 보기 : cmd + e
- 메소드, 변수 사용된 곳 찾기 : option + F7

## 이동
- 메소드 사용된 곳으로 이동 (option + F7의 빠른 찾기) : cmd + B
- 메소드 구현체로 이동 : cmd + option + B

### 탭 이동
- cmd + shift + [ (왼쪽 탭으로 이동)
- cmd + shift + [ (오른쪽 탭으로 이동)
- 탭 위치 옮기기 : TabMover 플러그인 설치
  - cmd + option + shift  + 방향키

### 커서 이동
- 히스토리 이동
  - 이전 커서로 이동 : cmd + [ 
  - 이후 커서로 이동 : cmd + ]

- 에러난 곳으로 바로 커서 이동 : F2
- 블록 시작점으로 커서 이동 : option + cmd + [
- 블록 끝으로 커서 이동 : option + cmd + ]
- 라인 이동 : cmd + L

## 변경
- 정렬 : option + cmd + L
- 대/소문자 변환 : cmd + shift + U
  - 플러그인 CamelCase 사용시 option + shift + U 로 카멜케이스, 스네이크, 케밥 등 다양하게 변환
   <figure>
    <img src='{{ "/assets/images/2022-05-15/plugin_camelCase.png" | relative_url }}' />
    </figure>
- 검색 후 일괄변경
  - 한 파일 내 : cmd + R
  - 여러 파일에서 : cmd + shift + R
- 클래스명, 함수명 변경 : shift + F6

## 선택
- 원하는 곳 다중 커서 : option + Shift + 마우스 좌클릭
- 방향키로 다중 커서 : option 연타 후 위/아래 방향키 
- 선택 영역 확장/축소 : options + 위/아래 방향키

## 리팩토링
- 테스트코드 자동 생성 : cmd + shift + T
- 변수 추출 : cmd + option + V
- 메소드 추출 : cmd + option + M
- ; 붙여서 자동완성 : cmd + shift + Enter

