# 07_OOP_basic

### OOP(Object-Oriented Programing) : 객체 지향 프로그래밍

#### :page_facing_up: 기본 구성요소

#### - 클래스(Class)

- 객체를 표현하는 문법
- `속성(attribute)`와 `행위(behavior)`를 정의한 것
- 객체지향 프로그램의 기본적인 사용자 정의 데이터 형(user define data type)

#### - 인스턴스(instance)

- class의 인스턴스/객체 : 실제 메모리상에 할당된 것
- 고유의 속성(attribute)을 가지고, class에 정의된 행위(behavior)를 수행할 수 있다.
- 객체의 behavior은 class에 정의된 behavior에 대한 method(정의)를 공유하면서 메모리를 경제적으로 사용

#### - 속성(attribute)

- class/instance가 가지고 있는 값

#### - 메서드(Method)

- class/instance가 할 수 있는 행위(behavior)/(함수)



## 객체의 속성(attribute)과 메서드(method)

#### 예시

- class/type - `str`

  instance - `''`  `hello`  `'123'`

  attribute -

  methods - `.capitalize()`  `.join()`  `.split()`

- class/type - `list`

  instance - `[]`  `['a', 'b']` 

  attribute -

  methods - `.append()`  `.reverse()`  `.sort()`

- class/type - `dict`

  instance - `{}`  `{key : value}` 

  attribute -

  methods - `.keys()`  `.values()`  `.items()`

- class/type - `int`

  instance - `0`  `1`  `2`

  attribute - `.real`  `.imag`

  methods - 

---

- 객체가 할 수 있는 모든 것(모든 속성과 메서드) 

  - `dir`

    ![image-20200329124121305](OOP.assets/image-20200329124121305.png)

## 클래스 및 인스턴스

### :star:클래스 정의하기

- 선언과 동시에 클래스 객체가 생성된다.
- 선언된 공간은 `지역 스코프(local scope)`로 사용된다.
- 정의된 attribute 중 변수는 멤버 변수(클래스 변수)로 불린다.
- 정의된 함수`def`는 `method(메서드)`로 불린다.

```python
class ClassName:
    attribute
    methods
```

### 인스턴스 생성하기

- 인스턴스 객체는 `ClassName()`을 호출함으로써 생성된다.

- 인스턴스 객체와 클래스 객체는 서로 다른 이름 공간을 가지고 있다.

- `instance(인스턴스) -> class(클래스) -> global(전역)` 순으로 탐색한다.

- 클래스는 특정 개념을 표현하는 껍데기고 실제 사용하려면 인스턴스를 생성해야 한다.

  ```python
  # 인스턴스 = 클래스()
  puppy = Dog()
  ```

