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

#### user `without` OOP

:exclamation: 문제점 : ​username/password가 global namespace에 작성되어 이 모듈로는 한사람의 정보만 담을 수 있다.

​				 여러 사람이 로그인을 한다면 같은 모듈을 여러개 만들어야 한다.

```python
# 사용자 정보
username = '정아린'
password = 'dkfls'

# 비밀번호를 바꾸는 기능
def change_password(old_password, new_password):
    global password
    if old_password == password:
        password = new_password
        print('비밀번호가 변경되었습니다.')
    else:
        print('비밀번호가 일치하지 않습니다.')
```

#### user `with` OOP

```python
class User:
    username = ''
    password = ''
    
    # 인스턴스에서 사용한 메서드(인스턴스 메서드)
    # 메서드의 첫번째 매개변수 : self
    def change_password(self, old_password, new_password):
        if old_password == self.password:
            self.password = new_password
            print('비밀번호가 변경되었습니다.')
        else:
            print('비밀번호가 일치하지 않습니다.')
```

```python
user1 = User()                            # 인스턴스 생성
user1.name = '정아린'
user1.password = 'dkfls'
# user1.change_password('dkfls','dkfls@')
User.change_password(user1, 'dkfls', 'dkfls@')
# 비밀번호가 변경되었습니다.

user2 = User()                            # 인스턴스 생성
user2.name= '강찬엽'
user2.password = 'cksduq1!'
# user2.change_password('cksduq1!','cksduq2@')
User.change_password(user2,'cksduq1!','cksduq2@')
print(user2.password)
# 비밀번호가 변경되었습니다.
# cksduq2@
```



#### Python 출력에서 `str` 과 `repr`

- `str` : 객체를 print() 할 때, 보이는 값
- `repr` : 객체 자체가 보여주는 값
- 둘 다 원하는 방식으로 수정 가능

```python
class User:
    username = ''
    password = ''
            
    def __str__(self):
        return 'print 안에 넣으면 이렇게 나오고'
    
    
    def __repr__(self):
        return '그냥 객체만 놔두면 이게 나오지요'
```

```python
user = User()

print(user)
# print 안에 넣으면 이렇게 나오고

user
# 그냥 객체만 놔두면 이게 나오지요
```





### :star2:용어 정리

```python
class Person:						# 클래스 정의(선언, 클래스 객체 생성)
    name = 'unknown'				# 클래스 변수(data attribute:멤버 변수)
    def greeting(self):				# 멤버 메서드 / 인스턴스 메서드
        return f'{self.name}'
```

```python
tim = Person()						# 인스턴스 객체 생성
tim.name							# 클래스 변수 호출
tim.greeting()						# 인스턴스 메서드 호출

# 이름으로 해놓으니깐 조금 헷갈릴 수 있으니깐
person1 = Person()
person1.name
person1.greeting()
```



#### 인스턴스와 객체

- 인스턴스 = 객체 (usually)
- 객체만 지칭할 땐, 그냥 객체
- 클래스와 연관 지을 땐, 인스턴스

```python
a = int(10)
b = int(20)

# a, b 는 객체
# a, b 는 int 클래스의 인스턴스

# a 가 int의 인스턴스인지 알아보는 방법
isinstance(a, int)
type(a)
```



## 실습 1

### MyList 만들기

```python
class MyList:
    data = []
    
    def append(self, n):
        self.data += [n]
    
    def count(self):
        return len(self.data)
    
    def __repr__(self):
        return f'내 리스트 안에는 {self.data}가 들어있다.'
```



## 클래스 변수와 인스턴스 변수

```python
class Dog:
    kind = 'tori'					# 클래스 변수 (모든 인스턴스가 공유)
    
    def __init__(self, name):		# 인스턴스 메서드
        self.name = name			# 인스턴스 변수 (각각의 인스턴스의 고유 변수)
```



### self : 인스턴스 객체 자기자신

- C++ or Java에서 this 키워드와 동일
- :star2: 무조건 메서드에서 `self`를 첫번째 인자로 설정 :star2:
- 메서드는 인스턴스 객체가 함수의 첫번째 인자로 전달되도록 되어있다.



### 클래스-인스턴스간의 이름공간(namespace)

- 클래스를 정의하면, 클래스 객체가 생성 and 이름공간이 생성된다.
- 인스턴스를 만들면 인스턴스 객체가 생성 and 이름공간이 생성된다.
- 인스턴스의 attribute가 변경되면, 변경된 데이터를 인스텐스 객체 이름공간에 저장
- 인스턴스에서 특정 attribute에 접근하면 `인스턴스 -> 클래스` 순으로 탐색

![image-20200329165213998](OOP.assets/image-20200329165213998.png)



### 클래스의 생성 & 소멸

- `__init__()`
  - 초기화
  - 인스턴스 객체가 만들어진 다음에 호출되는 함수
  - 인스턴스에서 사용할 초기 값들을 초기화 하고 초기화된 새 인스턴스를 얻음
- `__del__()`
  - 소멸자, 파괴자
  - 인스턴스 객체가 소면되기 직전에 호출되는 함수

> 위의 형식처럼 언더스코어가 있는 메서드는 특별한 일을 하기 위해 만들어진 메서드이기 때문에 `스페셜 메서드` 또는 `매직 메서드`라고 한다.   ex) `__something__`

```python
class Person():
    
    def __init__(self):
        print('야호!')
        
    def __del__(self):
        print('bye...')
```

```python
p1 = Person()
# 야호 출력
del p1
# bye... 출력
```

---

![image-20200329170734779](OOP.assets/image-20200329170734779.png)

## 실습 2

```python
class Stack:
    def __init__(self):
        self.data = []
    
    def empty(self):
        if len(self.data) == 0:
            return True
        else:
            return False
    
    def top(self):
        if len(self.data) == 0:
            return None
        else:
            return self.data[-1]
        
    def pop(self):
        if len(self.data) == 0:
            return None
        else:
            self.data -= self.data[-1]
    
    def push(self, n):
        self.data += [n]
        
    def __repr__(self):
        return ' '.join(map(str,self.data))
```

---

```python
class circle:
    pi = 3.14
    
    def __init__(self, r, x=0, y=0):
        self.r = r
        self.x = x
        self.y = y
    
    def area(self):
        return (self.pi)*(self.r)**2
    
    def circumference(self):
        return 2*self.pi*self.r
    
    def center(self):
        return self.x,self.y
    
    def move(self, x, y):
        self.x = x
        self.y = y
        return self.x,self.y
```

![image-20200329173752415](OOP.assets/image-20200329173752415.png)

---



# 08_OOP_advanced

