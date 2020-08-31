---
title: "[Git] 필요없는 변경 사항을 stage에서 없애기"
excerpt: 캐시를 제거해서 .gitignore로 관리하기
categories:
- Git
tags:
- gitignore
- cache
- untracking
- stagingArea
---

## 파일 상태를 Unstaged로 변경하기

- 상황 : 변경사항이 있을 때마다 필요없는 파일들도 Staging Area에 올라왔다. gitignore 파일이 있었지만 내용을 추가하지 않은 채 계속 커밋&푸쉬가 진행되어 왔다.
- 핵심
    1. 앞으로도 특정 파일의 변경사항을 언트랙킹하려면 .gitignore 파일에 추가하면 된다.
    2. .gitignore에 파일을 추가하기 전에 stage에 올라간 파일들은 **캐시가 남아**있어 이그노어 파일이 적용되지 않는다. (ignore 처리된 파일이 계속 changes에 뜬다)
- 해결 : 캐시를 제거한다

## 캐시 제거하기

```bash
git rm -r --cached .
git add .
git commit -m "cache clear"
```

여기 [블로그](https://niceman.tistory.com/114)에서 도움을 받았다.

깃 레포지토리의 가장 상위 폴더로 이동 후 

1. 현재 레포의 캐시 내용을 전부 삭제
2. .gitignore에 넣은 파일 목록들을 제외하고 다른 모든 파일을 다시 트래킹하도록 add All
3. 커밋

## gitignore 파일 생성

```bash
vi .gitignore
```

- 에디터를 켜서 gitignore 파일을 열고 i나 a 또는 o를 누르고 '입력모드'로 들어간다

> Jekyll 블로그용 gitignore 파일 내용

```bash
## MacOS
*.DS_Store
.bundle
.sass-cache
node_modules
package.json

## Jekyll stuff
/_site/
_site/
.sass-cache/
.jekyll-metadata
.jekyll
Gemfile
Gemfile.lock
https://gmlwjd9405.github.io/2017/10/06/Jekyll-github.io-blog-3.html
```

- 붙여넣고 esc로 '명령모드'로 돌아온 뒤 :wq 를 입력하여 저장 및 종료한다.
- ignore파일 내용 [출처](https://gmlwjd9405.github.io/2017/10/06/Jekyll-github.io-blog-3.html)
- 깃이그노어 파일 자동 생성기 : [gitignore.io](https://www.toptal.com/developers/gitignore)
