---
layout: post
title: Chpater 1. DB Modeling
color: rgb(000, 204, 255)
tags: [Django]
---

## Django 의 개발방식 (MTV 패턴)
<p align="center"><img src="https://user-images.githubusercontent.com/67581495/107123479-286b8f00-68e1-11eb-9a7d-467459727b9e.png"></p>
- M(Model): 데이터베이스에 저장되는 데이터에 대해 정의
- T(Template): 사용자(user)에게 보여지는 부분을 정의
- V(View): 실질적으로 프로그램 로직이 동작하여 템플릿에 전달되는 부분을 정의
<p align="center"><img src="https://user-images.githubusercontent.com/67581495/107123497-39b49b80-68e1-11eb-954a-96dd80176b28.png"></p>
웹 클라이언트가 서버에 Request를 보내면 URLConf 모듈을 통해 URL의 PATTERN을 분석하여 view와 매핑 시켜준다. C.R.U.D가 필요하다면 Model을 통해 DB에 접근한다. 그 후 View가 Template을 통해 클라이언트에게 보낼 html 파일을 랜더링 한다.

---
## 모델링 설계하는 방법
1) 어떤 필드가 필요한지 생각한다.
2) 각 필드는 어떤 타입이어야 하는지 생각한다.
Ex1) 주문(Order) 모델링
- 주문번호 
- 고객-고객 번호 
- 총 금액
- 주문 상태
Ex2) 포스트(Post) 모델링
- 글 번호 `pk`
- 유저-글쓴이번호 `relation-pk`
- 글 내용 `TextField`
- 글 쓴 날짜 `DateTimeField`
- 글 수정한 날짜 `DateTimeField`
