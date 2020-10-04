---
title: "[Mybatis] 대량의 데이터 다중 insert 하기"
excerpt: mybatis에서 다중insert를 해야하는 경우
categories:
- StudyNote
tags:
- Mybatis
- 다중insert
- 데이터 저장
toc: true
toc_sticky: true
toc_label: 목차
---

# mybatis에서 다중insert를 해야하는 경우

참고 : [https://kutar37.tistory.com/entry/mybatis-다중-insert](https://kutar37.tistory.com/entry/mybatis-%EB%8B%A4%EC%A4%91-insert)

## 상황

양이 거대한 데이터를 디비에 저장할 때 → 일반적인 방법으로 마이바티스에 insert 했더니 하루죄~~~ㅇ일 인서트를 하고있다...

⇒ list 형태의 객체를 이용해서 insert를 해보자! 

## 1. 단일 insert mapper를 구현하고 insert mapper를 List를 이용해 반복해서 insert 한다

1) DTO 클래스를 만들어 각각을 ArrayList에 add 로 담고, Map 객체에 map.put("list", list);로 담는다

2) List형태의 객체를 반복해서 단일 insert 처리한다.

```java
public class UserMapper {
     
@Autowired 
private SqlSession mapper;
     
    public void insetUser(Map<string, object=""> map) {
        List<userdto> list = (ArrayList<userdto>)map.get("list");
        for(UserDto dto : list) {
            mapper.insert("user.insert", dto);
        }
    }
}
```

## 2. foreach를 이용한 다중 insert

```java
public class UserMapper {
     
    @Autowired private SqlSession mapper;
     
    public void insetUser(Map<string, object> map) {
        mapper.insert("user.insert", map);
    }
}
```

```java
<insert id="insert" parametertype="java.util.Map">
        insert into user(username, age)
        values
        <foreach collection="list" item="item" separator=" , ">
            (#{item.username}, #{item.age})
        </foreach>
 </insert>
```

- <foreach> 태그
    - collection : 파라미터 타입으로 넘어온 map 안에 list (map에 key값)
    - item : collection을 사용할 변수명
    - seperator : 반복 문자열을 구분할 문자

[참고 : [Mybatis/MariaDB]foreach 구문을 이용해서 Insert 대량 삽입하기](https://vivi-world.tistory.com/13)
