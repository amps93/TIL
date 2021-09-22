# URL 분리

config/urls.py 파일 에는 **앱이 아닌 프로젝트 성격의 파일**이므로 이곳에는 프로넥트 성격의 URL 매핑만 추가되어야 함

```python
# config/urls.py

from django.contrib import admin
from django.urls import path, include #inculde 추가
# from pybo import views 삭제

urlpatterns = [
    path('admin/', admin.site.urls),
    #path('pybo/', include('pybo.urls')), 아래로 수정
    path('pybo/', include('pybo.urls')),
]
```

* path('pybo/', include('pybo.urls')) : `pybo/`로 시작되는 페이지를 요청하면 이제 `pybo/urls.py`파일의 매핑 정보를 읽어서 처리하라는 의미
* 이제 pybo 앱의 URL을 추가할때 `config/urls.py` 파일이 아닌 `pybo/urls.py` 파일만 수정하면 됨



## pybo/urls.py 생성

1. pybo디렉토리 밑에 urls.py 생성

2. 아래와 같이 입력

   ```python
   from django.urls import path
   from . import views
   
   urlpatterns = [
       path('', views.index)
   ]
   ```

3. 