## Django ORM

> 기본적인 데이터베이스 조작을 CRUD(Create, Read, Update, Delete) operation 이라고 한다.

### 0. django shell

>  python interactive interpreter를 django 프로젝트에 맞게 쓸 수 있는 기능

```bash
$ python manage.py shell
```

* 추가적인 패키지 설치를 통해 편하게 활용할 수 있다.

  ```bash
  $ pip install django-extensions ipython
  ```

  * `django-extensions` 는 django 개발에 있어서 유용한 기능들을 기본적으로 제공한다.
    * https://github.com/django-extensions/django-extensions
  * `ipython` 은 인터렉티브 쉘을 조금 더 편하게 활용하기 위해서 설치.

* 설치 이후에, `settings.py` 에 다음의 내용을 추가한다. (콤마 유의)

  ```python
  # django_crud/settings.py
  INSTALLED_APPS = [
      ...
      'django_extensions',
      'articles',
  ]
  ```

* 그리고 이제부터는 아래의 명령어를 사용한다.

  ```bash
  $ python manage.py shell_plus
  ```

* 쉘 종료 명령어는 `ctrl+d` 이다.

### 1. 생성

```python
article = Article()
article.title = '제목'
article.content = '내용'
article.save()
```

### 2. 조회

* 전체 데이터 조회

  ```python
  Article.objects.all()
  >> <QuerySet [<Article: Article object (1)>]>
  ```

* 단일 데이터 조회

  > 단일 데이터 조회는 고유한 값인 id를 통해 가능하다.

  ```bash
  Article.objects.get(id=1)
  >> <Article: Article object (1)>
  ```

### 3. 수정

```python
a1 = Article.objects.get(id=1)
a1.title = '제목 수정'
a1.save()
```

* 수정이 되었는지  확인하기 위해서 데이터 조회를 다시 해보자.

### 4. 삭제

```python
a1 = Article.objects.get(id=1)
a1.delete()
>> (1, {'articles.Article': 1})
```



## Admin 페이지 활용

### admin 등록

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article
admin.site.register(Article)
```



### 1. 관리자 계정 생성

```bash
$ python manage.py createsuperuser
사용자 이름 (leave blank to use 'ubuntu'): admin1
이메일 주소:
Password:
Password (again):
Superuser created successfully.
```

### 2. admin 등록

> admin 페이지를 활용하기 위해서는 app 별로 있는 admin.py에 정의 되어야 한다.

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article
admin.site.register(Article)
```

### 3. 확인

* `/admin/` url로 접속하여, 관리자 계정으로 로그인


