# Django

* https://docs.djangoproject.com/ko/3.2/intro/tutorial01/



## Conda env for Django

* conda deactivate

* conda create --name django python=3.8.3

* conda env list

* conda activate django

* pip install ipykernel

* python -m ipykernel install --user --name django --display-name "Python Django"

* conda install -c conda-forge jupyterlab



## project 만들기

* 프로젝트 디렉토리 이동
* django-admin startproject mysite
* startproject 생성
  * The outer `mysite/` root directory is a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
  * `manage.py`: Django 프로젝트와 다양한 방법으로 상호작용 하는 커맨드라인의 유틸리티 입니다. `manage.py` 에 대한 자세한 정보는 [django-admin and manage.py](https://docs.djangoproject.com/ko/3.2/ref/django-admin/) 에서 확인할 수 있습니다.
  * `mysite/` 디렉토리 내부에는 프로젝트를 위한 실제 Python 패키지들이 저장됩니다. 이 디렉토리 내의 이름을 이용하여, (`mysite.urls` 와 같은 식으로) 프로젝트의 어디서나 Python 패키지들을 임포트할 수 있습니다.
  * `mysite/__init__.py`: Python으로 하여금 이 디렉토리를 패키지처럼 다루라고 알려주는 용도의 단순한 빈 파일입니다. Python 초심자라면, Python 공식 홈페이지의 [패키지](https://docs.python.org/3/tutorial/modules.html#tut-packages)를 읽어보세요.
  * `mysite/settings.py`: 현재 Django 프로젝트의 환경 및 구성을 저장합니다. [Django settings](https://docs.djangoproject.com/ko/3.2/topics/settings/)에서 환경 설정이 어떻게 동작하는지 확인할 수 있습니다.
  * `mysite/urls.py`: 현재 Django project 의 URL 선언을 저장합니다. Django 로 작성된 사이트의 《목차》 라고 할 수 있습니다. [URL dispatcher](https://docs.djangoproject.com/ko/3.2/topics/http/urls/) 에서 URL 에 대한 자세한 내용을 읽어보세요.
  * `mysite/asgi.py`: An entry-point for ASGI-compatible web servers to serve your project. See [ASGI를 사용하여 배포하는 방법](https://docs.djangoproject.com/ko/3.2/howto/deployment/asgi/) for more details.
  * `mysite/wsgi.py`: 현재 프로젝트를 서비스하기 위한 WSGI 호환 웹 서버의 진입점입니다. [WSGI를 사용하여 배포하는 방법](https://docs.djangoproject.com/ko/3.2/howto/deployment/wsgi/)를 읽어보세요.



## 개발서버

* mysite 디렉토리로 이동
* python manage.py runserver
* 장고 개발서버 시작(http://127.0.0.1:8000/)
* **절대로** 개발 서버를 운영 환경에서 사용하지 마십시요. **개발 서버는 오직 개발 목적으로만** 사용하여야 합니다



## 설문조사 앱 만들기

```python
python manage.py startapp polls
```



## 첫번째 뷰 작성하기

* polls/views.py

```
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

* mysite/urls.py

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')), #해당 라인 추가
    path('admin/', admin.site.urls),
]
```



## 데이터베이스 연동

* mysite/setting.py

```python
#76번째 줄 아래로 수정
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'tip' ,
        'USER' : 'amps' ,
        'PASSWORD' : '123123',
        'HOST' : 'localhost' ,
        'PORT' : '3306'
    }
}
```

*  python manage.py migrate

