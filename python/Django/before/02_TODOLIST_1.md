# TODO-LIST

## 1. 프로젝트 구성하기

* 터미널에서 `django-admin startproject 프로젝트명` 입력
* manage.py가 있는 폴더에서 `python manage.py startapp my_to_do_app` 입력
* `ToDOList > setting.py`의 내용 변경

```python
#line 33
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'my_to_do_app' #해당 내용 추가
]
```

* `ToDoList > urls.py`의 내용 변경

```python
from django.contrib import admin
from django.urls import path
from django.urls.conf import include # 추가

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('my_to_do_app.urls')) #추가
]

```

* `my_to_do_app`폴더에 `urls.py`생성

```python
#my_to_do_app > urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('',views.index)
]
```

* `my_to_do_app > views.py`의 내용 변경

```python
#my_to_do_app > views.py
from django.shortcuts import render #추가
from django.http import HttpResponse

# Create your views here.
#추가
def index(request):
    return render(request, 'my_to_do_app/index.html')
```

### templates

* HTML파일을 템플릿으로 사용하려고 할때, 장고는 해당 앱에서 templates라는 폴더를 탐색 > 동일한 앱의 이름으로 된 폴더를 찾아 그 내부에 있는 html파일을 불러와 사용 > 따라서 html파일을 사용할때는 항상 이와 같이 app 내부에 templates라는 폴더와 templates라는 폴더 내부에 app 이름과 동일한 폴더가 존재하고, 그안에 html을 넣어야함

* `my_to_do_app` 폴더 밑에 `templates/my_to_do_app` 폴더 생성
* `templates/my_to_do_app` 밑에 `index.html` 생성

```html
<--index.html/-->
<html lang="ko">
<head>
    <meta charset="UTF-8">

    <!-- Boot strap -->
    <!-- 합쳐지고 최소화된 최신 CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">
    <!-- 부가적인 테마 -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap-theme.min.css">
    <!-- 합쳐지고 최소화된 최신 자바스크립트 -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/js/bootstrap.min.js"></script>

    <style>
        .content{
            height: 75%;
        }
        .messageDiv{
            margin-top: 20px;
            margin-bottom: 50px;
        }
        .toDoDiv{

        }
        .custom-btn{
            font-size: 10px;
        }
        .panel-footer{
            height:10%;
            color:gray;
        }
    </style>

    <title>To-Do</title>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="page-header">
                <h1>To-do List <small>with Django</small></h1>
            </div>
        </div>
        <div class="content">
            <div class="messageDiv">
                <form action="" method="POST">{% csrf_token %}
                    <div class="input-group">
                        <input id="todoContent" name="todoContent" type="text" class="form-control" placeholder="메모할 내용을 적어주세요">
                        <span class="input-group-btn">
                            <button class="btn btn-default" type="submit">메모하기!</button>
                        </span>
                    </div>
                </form>
            </div>

            <div class="toDoDiv">
                <ul class="list-group">

                    <form action="" method="GET">
                        <div class="input-group" name='todo1'>
                            <li class="list-group-item">메모한 내용은 여기에 기록될 거에요</li>
                            <input type="hidden" id="todoNum" name="todoNum" value="1"></input>
                            <span class="input-group-addon">
                                <button type="submit" class="custom-btn btn btn-danger">완료</button>
                            </span>
                        </div>
                    </form>

                </ul>
            </div>
        </div>
        <div class="panel-footer">
            실전예제로 배우는 Django. Project1-TodoList
        </div>
    </div>
</body>
</html>
```

* `my_to_do_app > views.py` 수정

```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def index(request):
    return render(request, 'my_to_do_app/index.html') #수정
```



