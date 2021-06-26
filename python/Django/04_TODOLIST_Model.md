# Model 생성

* manage.py 경로에서 `python manage.py makemigrations` 입력
* 해당 명령어는 테이블이 생성된 것이 아니고 데이터베이스에 전해 줄 초안, 설계도, 작업 지시서와 비슷한 역할을 함
* 실제로 테이블을 만들려면 `python manage.py migrate` 입력
* `python manage.py dbsell`입력해 제대로 만들어졌는지 확인