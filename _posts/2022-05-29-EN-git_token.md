---
title: "[에러노트] refusing to allow a Personal Access Token to create or update workflow 에러 해결"
excerpt: ""
categories:
- ErrorNote
tags:
- error
- Github
- token
toc: true
toc_sticky: true
toc_label: 목차
---

## 현상
<figure>
  <img src='{{ "/assets/images/2022-05-29/Untitled.png" | relative_url }}' width="600" />
</figure>


Github Action 강의를 듣고 이것저것 수정사항을 거친 후 push하려는데 에러가 발생함.

대충 보니 yml 파일에 액세스 토큰을 쓴 쪽에서 뭔가 문제가 있는 듯 하다.

## 원인

해당 토큰으로는 workflow를 생성하거나 수정할 수 없다는 메시지이므로 토큰의 scope를 workflow에서 사용할 수 있도록 변경해주어야 한다. 

## 해결

**[github.com/settings/tokens](https://github.com/settings/tokens)**

위의 링크로 들어가서 해당 토큰을 선택하고 Select scopes에서 workflow 체크박스를 선택한다. → Update token 버튼 클릭 후 다시 push하니 성공!
<figure>
  <img src='{{ "/assets/images/2022-05-29/Untitled%201.png" | relative_url }}' width="600" />
</figure>