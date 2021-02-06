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


Ex) 포스트(Post) 모델링


- 글 번호 `pk`
- 유저-글쓴이번호 `relation-pk`
- 글 내용 `TextField`
- 글 쓴 날짜 `DateTimeField`
- 글 수정한 날짜 `DateTimeField`

## Primary Key(기본키, pk)
- [PK](https://docs.djangoproject.com/en/3.1/topics/db/models/)는 테이블에 저장된 각각의 데이터를 구분하는 키
- 데이터베이스(DB) 테이블에 각 행의 식별 기준인 기본키가 필요하다.
- Django 에는 기본키로 id가 디폴트로 지정된다. 
```python
id = models.AutoField(primary_key=True)
```
`만약 따로 pk를 설정하고 싶다면 필드에 primary_key=True 를 넣어주면 된다. 이 경우에 id는 자동으로 생성되지 않는다.`

## Foreignkey
```python
class Order(models.Model):
    total_price = models.IntergerField(verbose_name="총 가격")
    product_name = models.Foreignkey(Product, on_delete=models.CASCADE)
```
- 각 테이블 간에 연결하기 위해서 특정 테이블에서 필드 중 다른 테이블에서 참조되는 키를 외래키라고 한다.

## Django Field types


| Field Type | Explain |
|:---:|:---|
| `CharField` | 작은 문자열 또는 큰 문자열을 위한 문자열 필드 |
| `TextField` | 큰 문자열 필드 |
| `IntegerField` | 정수 필드 |
| `FloatField` | 실수 필드 |
| `BooleanField` | True/False 필드 |
| `DateTimeField` | 날짜와 시간을 가지는 필드 |
| `FileField` | 파일 업로드 필드 |
| `EmailField` | EmailValidator를 사용해서 값이 유효한 email인지 체크하는 CharField |
| `ImageField` | 이미지 파일인지 유효성 체크해주며, FileField의 파생 클래스 |
| `DecimalField` | 소숫점을 갖는 필드 |
| `AutoField` | 1부터 시작해서 1씩 증가하기 때문에 IntegerFiled라고 봐도 무방함. AutoField로 pk 필드가 자동으로 추가된다. |
| `DateField` | 날짜의 필드 타입 |



```python
class DateField(auto_now=False, auto_now_add=False, **options)
```
DateTimeField와 DateField 는 매개변수 argument로 auto_now와 auto_now_add를 갖는다. 


- auto_now_add: 데이터가 **처음** 생성되어 저장할 때
- auto_now: 데이터가 저장될 때 **(Update)**
