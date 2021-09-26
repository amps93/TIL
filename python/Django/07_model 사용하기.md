# 모델 사용하기

* `python manage.py shell`



## Question 생성

```python
>>> from pybo.models import Question, Answer
>>> from django.utils import timezone
>>> q = Question(subject='pybo가 무엇인가요?', content='pybo에 대해서 알고 싶습니다.', create_date=timezone.now())
>>> q.save()
>>> q.id
1
>>> q = Question(subject='장고 모델 질문입니다.', content='id는 자동으로 생성되나요?', create_date=timezone.now())
>>> q.save()
>>> q.id
2
```



## Question 조회

```python
>>> Question.objects.all()
<QuerySet [<Question: Question object (1)>, <Question: Question object (2)>]>
```

Question 모델에 `__str__` 메서드를 추가하면 id 값 대신 제목을 표시할 수 있다.

```python
# pybo/models.py

(... 생략 ...)

class Question(models.Model):
    subject = models.CharField(max_length=200)
    content = models.TextField()
    create_date = models.DateTimeField()

    def __str__(self):
        return self.subject

(... 생략 ...)
```

모델이 변경되었으므로 장고 셸을 재시작해야 변경된 결과를 확인할 수 있다

```
(mysite) c:\projects\mysite>python manage.py shell
>>> from pybo.models import Question, Answer
>>> Question.objects.all()
<QuerySet [<Question: pybo가 무엇인가요?>, <Question: 장고 모델 질문입니다.>]>
>>>
```

* 모델에 메서드가 추가될 경우에는 makemigrations와 migrate를 수행할 필요가 없다. migrate 명령이 필요한 경우는 모델의 속성이 변경되었을때 뿐이다.



### filter와 get

```
##### filter를 사용하여 id 값이 1인 Quesiton 데이터를 조회
>>> Question.objects.filter(id=1)
<QuerySet [<Question: pybo가 무엇인가요?>]>
#####filter는 조건에 해당되는 데이터를 모두 리턴해 주기 때문에 다건을 의미하는 QuerySet이 리턴

#####id는 유일한 값이므로 filter 대신 get을 이용하여 조회할 수도 있다
>>> Question.objects.get(id=1)
<Question: pybo가 무엇인가요?>
#####get으로 조회할 경우 QuerySet이 아닌 Question 모델 객체가 리턴되었다. filter는 다건을 리턴하지만 get은 한건만 리턴하기 때문

#####조건에 맞지 않는 데이터 조회 시
>>> Question.objects.get(id=3)
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "C:\venvs\mysite\lib\site-packages\django\db\models\manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "C:\venvs\mysite\lib\site-packages\django\db\models\query.py", line 435, in get
    raise self.model.DoesNotExist(
pybo.models.Question.DoesNotExist: Question matching query does not exist.

#####subject에 "장고"라는 문자열이 포함된 데이터만 조회
>>> Question.objects.filter(subject__contains='장고')
<QuerySet [<Question: 장고 모델 질문입니다.>]>
```

* 참고 : https://docs.djangoproject.com/en/3.0/topics/db/queries/



## Question 수정

```
먼저 다음과 같이 id 값이 2인 데이터를 조회한다.

>>> q = Question.objects.get(id=2)
>>> q
<Question: 장고 모델 질문입니다.>
그리고 subject 속성을 다음과 같이 수정하자.

>>> q.subject = 'Django Model Question'
>>>
여기까지만 해서는 수정이 되지 않는다. 반드시 다음처럼 save를 수행해 주어야 변경된 데이터가 반영된다는 것을 꼭 기억하자.

>>> q.save()
>>> q
<Question: Django Model Question>
```



## Question 삭제

```
이번에는 id 값이 1인 Question 데이터를 삭제해 보자.

>>> q = Question.objects.get(id=1)
>>> q.delete()
(1, {'pybo.Question': 1})
delete를 수행하면 해당 데이터가 삭제된다. 삭제될 때는 위와 같이 추가정보가 리턴된다. (1, {'pybo.Question': 1})은 Question 모델이 1개 삭제되었음을 의미한다. 앞의 숫자는 삭제된 데이터의 갯수를 의미하고, 뒤의 숫자는 모델별 삭제된 숫자를 의미한다.

실제로 삭제되었는지 다음처럼 Question.objects.all() 로 확인해 보자.

>>> Question.objects.all()
<QuerySet [<Question: Django Model Question>]>
첫번째 질문은 삭제되고 두번째 질문만 조회되는 것을 확인할 수 있다.
```



## Answer 작성

```
>>> q = Question.objects.get(id=2)
>>> q
<Question: Django Model Question>
>>> from django.utils import timezone
>>> a = Answer(question=q, content='네 자동으로 생성됩니다.', create_date=timezone.now())
>>> a.save()
답변 데이터를 만들기 위해서는 질문이 필요하므로 id가 2인 질문을 먼저 조회한 후 question 속성에 대입해 주었다.

Answer 모델도 Question 모델과 마찬가지로 유일한 값을 의미하는 id가 자동으로 생성 된다.

>>> a.id
1
```



## Answer 조회

```
답변을 조회하는 방법은 질문과 마찬가지로 Answer의 id 값을 사용하면 된다.

>>> a = Answer.objects.get(id=1)
>>> a
<Answer: Answer object (1)>
Answer객체인 a를 사용하면 답변에 연결된 질문도 조회할 수 있다.

>>> a.question
<Question: Django Model Question>
Answer 모델 객체인 a를 통해서 질문을 찾는것은 Answer 모델에 question 속성이 연결되어 있기 때문에 매우 쉽다. 그렇다면 질문을 이용하여 답변을 찾는 것은 가능할까?

가능하다. 다음처럼 하면 된다.

>>> q.answer_set.all()
<QuerySet [<Answer: Answer object (1)>]>

q.answer_set을 사용하면 질문에 연결된 답변을 가져올 수 있다. Question 모델에는 answer_set 이라는 속성이 없지만 Answer 모델에 Question 모델이 ForignKey로 연결되어 있기 때문에 q.answer_set 과 같은 역방향 접근이 가능하다.

연결모델명_set(예:answer_set)은 상식적으로 생각하면 더 쉽다. 질문 하나에는 여러개의 답변이 가능하므로 q.answer_set이 가능하지만 답변 하나에는 여러개의 질문이 있을 수 없으므로 a.question_set은 불가능하다. 답변 하나에는 질문 하나만 가능하기 때문에 a.question만 가능하다.

정말 신통방통한 장고의 기능이 아닐수 없다. 연결모델명_set 방법은 자주 사용하니 꼭 기억해 두도록 하자.
```

