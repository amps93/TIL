# makemigration

* migrate 수행

```
(mysite) c:\projects\mysite>python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  No migrations to apply.
  Your models in app(s): 'pybo' have changes that are not yet reflected in a migration, and so won't be applied.
  Run 'manage.py makemigrations' to make new migrations, and then re-run 'manage.py migrate' to apply them.

(mysite) c:\projects\mysite>                                    
```

* 하지만 결과 문구를 보니 `migrate`가 정상적으로 수행되지 않았다. 왜냐하면 모델이 신규로 생성되거나 변경되면 `makemigrations` 명령을 먼저 수행한 후에 `migrate` 명령을 수행해 주어야 하기 때문이다.

* makemigrations 수행 시 pybo/migrations/0001_initial.py라는 파이썬 파일이 자동 생성됨
* makemigrations를 수행해도 실제로 테이블이 생성되지는 않음. 실제 테이블 생성은 migrate를 통해 가능

## sqlmigrate

* `python manage.py sqlmigrate pybo 0001`

* 실행된느 쿼리만 조회할 뿐 실제 쿼리가 수행되지는 않음