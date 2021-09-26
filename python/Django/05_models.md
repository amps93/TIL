# models.py

* 앱의 기능과 관련된 모델을 정의



질문과 답변에 해당되는 모델을 pybo/models.py에 정의

```python
# pybo/models.py

from django.db import models

# Create your models here.
class Question(models.Model):
    subject = models.CharField(max_length=200)
    content = models.TextField()
    create_date = models.DateTimeField()


class Answer(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    content = models.TextField()
    create_date = models.DateTimeField()
```

* Question 모델은 제목, 내용, 작성일시를 속성으로 갖음
* Answer 모델은 Question 모델을 속성으로 가져가야함
  * ForeignKey를 사용
  * on_delete=models.CASCADE : 이 답변과 연결된 질문이 삭제될 경우 답변도 함께 삭제
* 속성 타입 참고 : https://docs.djangoproject.com/en/3.0/ref/models/fields/#field-types



## 파이보 앱 등록

작성한 모델을 이용하여 테이블 생성



* pybo 앱을 config/setting.py 파일의 INSTALLED_APPS 항목에 추가

```python
# config/setting.py

(... 생략 ...)
INSTALLED_APPS = [
    'pybo.apps.PyboConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    (... 생략 ...)
]
(... 생략 ...)
```

INSTALLED_APPS에 추가한 `pybo.apps.PyboConfig` 클래스는 `pybo/apps.py` 파일에 있는 클래스이다. 이 파일은 pybo 앱 생성시 자동으로 만들어지는 파일로 따로 만들 필요가 없다. 이미 `pybo/apps.py` 파일 안에 다음과 같은 클래스가 구현되어 있을 것이다.

```python
# pybo/apps.py

from django.apps import AppConfig

class PyboConfig(AppConfig):  # 장고 버전에 따라 내용이 다를 수 있다.
    name = 'pybo'
```

* 파이보 앱을 INSTALLED_APPS 항목에 추가하지 않으면 데이터베이스 관련 작업을 할 수 없으니 빠뜨리지 않도록 주의