## Django App 생성

- django는 여러 개의 APP을 가진 하나의 프로젝트로 구성된다.

  - 커뮤니티를 만든다.
    - 회원과 관련된 APP : `accounts`
    - 게시글과 관련된 APP : `posts`

  ```bash
  $ python manage.py startapp app이름
  ```

  (아래의 내용에는 `pages`라는 APP이름을 사용할 것.)

  

- APP 생성 후 반드시 `settings.py`의 `INSTALLED_APP`에 등록한다.

  ```python
  INSTALLED_APPS = [
      ...
      'pages',
  ]
  ```



### 기본 흐름

#### 1. urls.py

```python
# django_intro/urls.py
from pages import views

urlpatterns = [
    path('lotto/', views.lotto),
]
```

- **from** app명 **import** views
- **path**('file명/', views.file명)



#### 2. views.py

```python
# pages/views.py
import random

def lotto(request):
    pick = random.sample(range(1, 46), 6)
    context = {
        'pick': pick
    }
    return render(request, 'lotto.html', context)
```

- 함수를 정의할 때, 항상 첫번째 인자는 `request`로 작성해둔다.
  - 내부적으로 요청을 처리할 때, 함수 호출 시 요청 정보가 담긴 객체를 넣어준다.(**ex. context**)
- `render`함수를 통해 return한다.
  - return render(`request`, 템플릿 파일(`html`), dictionary, 템플릿에서 활용을 하려고 하는 값 )



#### 3. template 파일 생성

- 반환할 `html file`은 항상 **templates** 폴더 안에 생성한다.

```html
<!-- pages/templates/lotto.html -->
<p>{{ pick }} </p>
```

- context 딕셔너리의 **key 값**을 적으면 출력된다.



## URL 설정

### Variable routing

> url의 특정 위치의 값을 변수로 활용

#### 1. urls.py

```python
# django_intro/urls.py
path('hi/<str:name>/', views.hi),
path('add/<int:a>/<int:b>/', views.add),
```

#### 2. views.py

```python
# pages/views.py
def hi(request, name):
    context = {
        'name': name
    }
    return render(request, 'hi.html', context)
```

#### 3. template

```html
<!-- pages/templates/hi.html-->
<h1>
    안녕, {{name}}
</h1>
```



## Template

### DTL

> 템플릿파일(html)은 django template language를 통해 구성된다.

#### 기본문법

1. 출력 `{{ }}`

   ```html
   {{ menu }}
   {{ menu.0 }}
   ```

2. 문법 `{% %}`

   ```html
   {% for menu in menupan %}
   
   {% endfor %}
   ```

3. 주석 `{# #}`

   ```html
   {# 주석입니다. #}
   ```

#### 반복문

```html
{% for reply in replies %}
	<li>{{ reply }}</li>
{% endfor %}
```

* `{{ forloop.counter }}`
* `{{ forloop.counter0 }}`
* `{% empty %}`



#### 조건문

```html
{% if user == 'admin' %}
	<p>관리자 입니다.</p>
{% else %}
	<p>권한이 없습니다.</p>
{% endif %}
```



#### built-in tag, filter

```html
{{ content|length }}
{{ content|truncatechars:10 }}
```



### Template 확장

```html
 <!-- pages/templates/base.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Django 기초 - pages</title>
    {% block css %}
    {% endblock %}
</head>
<body>
    <h1>Django 기초 문법 학습</h1>
    {% block body %}
    {% endblock %}
</body>
</html>
```

```html
{% extends 'base.html' %}

{% block css %}
<style>
    h1 {
        color: blue;
    }
</style>
{% endblock %}

{% block body %}
	<h1>페이지</h1>
{% endblock %}
```



### Template 설정

```python
# django_intro/settings.py Line#55
TEMPLATES = [
    {
        # DTL 엔진을 활용. jinja2 등으로 변경 가능함.
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # APP 내에 있는 폴더가 아닌 추가적으로 템플릿으로 활용하고 싶은 경로.
        'DIRS': [
            os.path.join(BASE_DIR, 'django_intro', 'templates')
        ],
        # APP_DIRS: True 인경우, 등록된 app(INSTALLED_APPS)의 디렉토리에 있는 templates 폴더를 템플릿 폴더로 활용하겠다.
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

* `DIRS` 리스트에 경로 정의는 폴더 구조를 통해 확인하자.

  ```
  00_django_intro/ <- BASE_DIR
  	django_intro/
  		templates/
  ```



## Multiple app을 위한 설정

> 앞으로는 항상 app을 생성하면 다음과 같은 폴더 구조를 가진다.

```
app1/
	templates/
		app1/
			index.html
			a.thml
    urls.py
    views.py
    ...

app2/
	templates/
		app2/
			index.html
			b.thml
    urls.py
    views.py
    ...
```

### 1. url 설정 분리

> 각각의 app 별로 url을 관리한다.

* 프로젝트 폴더 urls.py 정의

  ```python
  # django_intro/urls.py
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('pages/', include('pages.urls')),
      path('boards/', include('boards.urls')),
  ]
  ```

* 각 프로젝트별 urls.py  정의

  ```python
  from django.urls import path
  from . import views
  
  urlpatterns = [
      # /boards/
      path('', views.index),
      # /boards/new/
      path('new/', views.new),
      # /boards/complete/
      path('complete/', views.complete),
  ]
  ```

### 2.  templates 폴더 구조

* template 파일을 반환하기 위해서 django는 아래의 폴더들을 탐색한다.
  * `DIRS` 에 정의된 경로의 하위 디렉토리
  * `INSTALLED_APPS` 디렉토리의 `templates` 폴더의 하위 디렉토리 탐색
* 이 과정에서 중복된 파일이 있는 경우, 예상치 못한 결과가 나타날 수 있다.
* 따라서, 앞으로 다음과 같은 구조를 유지한다.

```
app1/
	templates/
		app1/
app2/
	templates/
		app2/
```



## Form을 통한 요청 처리

### 개요

1. 사용자들로부터 값을 받아서 (`boards/new/`)
2. 이를 단순 출력하는 페이지 구성 (`boards/complete/`)

### 1. 사용자에게 form 양식 제공

1. url 지정

   ```python
   # boards/urls.py
   path('new/', views.new),
   ```

2. view 함수 생성

   ```python
   # boards/views.py
   def new(request):
       return render(request, 'boards/new.html')
   ```

3. template

   ```html
   <!-- boards/templates/boards/new.html -->
   <form action="/boards/complete/">
       제목 : <input type="text" name="title">
   </form>
   ```

   * form 태그에는 `action` 속성을 정의한다.
     * 사용자로부터 내용을 받아서 처리하는 url
   * input 태그에는 `name` 속성을 통해 사용자가 입력한 내용을 담을 변수 이름을 지정한다.
   * url 예시 :  `/boards/complete/?title=제목제목`

### 2. 사용자 요청 처리

1. urls.py 정의

   ```python
   # boards/urls.py
   path('complete/', views.complete)
   ```

2. views.py

   ```python
   # boards/views.py
   def complete(request):
       title = request.GET.get('title')
       context = {
   		'title': title
       }
       return render(request, 'boards/complete.html', context)
   ```

   * `request` 에는 요청과 관련된 정보들이 담긴 객체가 저장되어 있다.

3. template

   ```html
   <!-- boards/templates/boards/complete.html -->
   {{ title }}
   ```

### 3. form 태그의 method 속성: GET과 POST 속성값

### GET

- 전송할 수 있는 정보의 길이가 제한된다.

- URL에 정보가 담겨서 전송된다.

- 요청을 전송할 때 필요한 데이터를 Body에 담지 않고, 쿼리스트링을 통해 전송합니다. URL의 끝에 `?`와 함께 이름과 값으로 쌍을 이루는 요청 파라미터를 쿼리스트링이라고 부릅니다. 만약, 요청 파라미터가 여러 개이면 `&`로 연결합니다. 쿼리스트링을 사용하게 되면 URL에 조회 조건을 표시하기 때문에 특정 페이지를 링크하거나 북마크할 수 있습니다.

  쿼리스트링을 포함한 URL의 샘플은 아래와 같습니다. 여기서 요청 파라미터명은 name1, name2이고, 각각의 파라미터는 value1, value2라는 값으로 서버에 요청을 보내게 됩니다.

  **www.example-url.com/resources?name1=value1&name2=value2**

### POST

- 전송할 수 있는 데이터의 길이 제한이 없다. (대용량 데이터를 전송할 수 있다.)
- URL상에 전달한 전보가 표시되지 않는다. **따라서 URL name이 추가 되어야 한다!**
- 토큰이 필요하다. **{% csrf_token %}**

