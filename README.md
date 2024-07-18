# spring-gift-enhancement

## step 1

### 기능 요구 사항

* 상품 정보에 카테고리를 추가하기
* 상품과 카테고리 모델 간의 관계를 고려하여 설계하고 구현하기

---

* **카테고리는 1차 카테고리만 있으며** 2차 카테고리는 고려하지 않는다.
* 카테고리는 수정할 수 있다.
* 관리자 화면에서 상품을 추가할 때 카테고리를 지정할 수 있다.
* 카테고리의 예시는 아래와 같다.
    * 교환권, 상품권, 뷰티, 패션, 식품, 리빙/도서, 레저/스포츠, 아티스트/캐릭터, 유아동/반려, 디지털/가전, 카카오프렌즈, 트렌드 선물, 백화점

#### Request

```
GET /api/categories HTTP/1.1
```

#### Response

```
HTTP/1.1 200
Content-Type: application/json

[
{
"id": 91,
"name": "교환권",
"color": "#6c95d1",
"imageUrl": "https://gift-s.kakaocdn.net/dn/gift/images/m640/dimm_theme.png",
"description": ""
}
]
```

### 프로그래밍 요구 사항

구현한 기능에 대해 **적절한 테스트 전략**을 생각하고 작성한다.
---

- [x] category의 CRUD 구현
- [x] category - product의 oneToMany 관계 매핑
- [x] category가 삭제될 때 -> product의 category가 [DefaultCategory]로 변함
- [x] category가 삭제될 때 product의 category 테스트 &uarr;
- [x] product의 category가 변경될 때 -> 이전 category에 접근해서 product 삭제 & 새 category에 해당 product add
- [x] product의 category가 변경될 때 테스트 &uarr;

---

## step 2

### 기능 요구 사항

* 상품 정보에 옵션 추가하기
* 상품과 옵션 모델 간의 관계를 고려하여 설계하기

* 상품에는 항상 하나 이상의 옵션이 있어야 한다.
* 옵션 이름은 공백을 포함하여 최대 50자까지 입력할 수 있다.
* 특수 문자 : ( ), [ ], +, -, &, /, _ 만 가능
    * 그 외 특수 문자 사용 불가
* 옵션 수량은 최소 1개 이상 1억 개 미만이다.
* 동일한 상품 내의 옵션 이름은 중복될 수 없다.

#### Request

```
GET /api/products/1/options HTTP/1.1
```

#### Response

```
HTTP/1.1 200
Content-Type: application/json

[
  {
    "id": 464946561,
    "name": "01. [Best] 시어버터 핸드 & 시어 스틱 립 밤",
    "quantity": 969
  }
]
```

- [x] option CRUD 구현
- [x] product - option ManyToMany
- [x] product에 항상 하나 이상의 옵션이 있어야
- [x] product에 중복된 이름의 옵션 존재 x
- [x] 테스트 작성
    - [x] mock 객체로 테스팅 해보기 (MockBean)