# static

지금까지 질문 목록 화면과 질문 상세 화면을 만들어 보았다. 하지만 좀 더 그럴싸한 화면을 만들기 위해서는 화면에 디자인을 적용해야 한다. 디자인을 적용하기 위해서는 스타일시트(stylesheet, CSS파일)를 사용해야 한다.



## 스태틱 디렉토리

스타일시트 파일은 장고의 스태틱 디렉터리에 저장해야 한다. 스태틱 디렉터리도 템플릿 디렉터리와 마찬가지로 `config/settings.py` 파일에 등록해야 한다.

```python
# config/setting.py

(... 생략 ...)

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]

(... 생략 ...)
```

이 후 static 폴더를 생성(mysite/static)



style.css 파일을 다음과 같이 작성

```css
# mysite/static/style.css

textarea {
    width:100%;
}

input[type=submit] {
    margin-top:10px;
}
```



## 템플릿에 스타일 적용

```html
<!--teplates/pybo/question_detail.html -->

{% load static %}
<link rel="stylesheet" type="text/css" href="{% static 'style.css' %}">
<h1>{{ question.subject }}</h1>
(... 생략 ...)
```

