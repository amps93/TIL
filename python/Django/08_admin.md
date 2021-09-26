# admin

## 슈퍼유저

* 관리자 화면에 접근할 수 있는 슈퍼유저 생성
* `python manage.py createsuperuser`

## 모델 관리

* Question 모델 등록

```python
# pybo/admin.py
from django.contrib import admin
from .models import Question #추가

admin.site.register(Question) #추가
```

## 모델 검색

* 관리자 화면에서 제목으로 질문 검색

```python
from django.contrib import admin
from .models import Question


class QuestionAdmin(admin.ModelAdmin): #추가
    search_fields = ['subject']


admin.site.register(Question, QuestionAdmin) #수정
```



