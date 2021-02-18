# 나랑살개 :dog:

> 인터페이스 개발 프로젝트 기간동안 새로 배운 것들 정리하기
>
> 우선 까먹기 전에 모두 적어놓는 것이 목표
>
> 예쁘게 정리는 나중에 천천히 ..!



## 부트스트랩

* M : margin
* P: padding



* t : top
* b : botton
* l : left
* r : right
* x : x축 (left, right)
* y : y축 (top, bottom)



* sm, lg 등 : 화면 해상도
* bg- : 배경



* btn-outline- : 테두리있는 버튼



* class="footer bg-light py-3 mt-auto" : 밝은 회색 배경, y축 3만큼의 패딩값 위쪽 마진 자동 설정



* 그리드

  * row
  * col
  * 12열로 구성, col-lg-4, col-lg-8 이런 식으로 비율 설정 가능

  

## 장고 - DB 연동

> 작업하다가 model을 수정하는 일이 몇 번 있었는데 존재하던 속성을 삭제하고 새로 추가하는 과정에서 변경 사항이 데이터베이스 (mysql)에는 반영되지 않는 문제가 있었다. 



### 해결방법

1. 다시 migrate하기

   * 추가한 속성을 주석처리 한 후 makemigrations, migrate 진행 (해당 속성을 지운다는 내용을 makemigrations에서 확인할 수 있다.)
   * 이 후 주석을 지우고 다시 makemigrations를 하면 다시 해당 속성을 추가한다는 내용이 보인다.

2. mysql에서 직접 해당 속성 추가하기

   ```mysql
   mysql -u root -p /* 루트 계정으로 로그인 */
   use db_name;/* 수정하려는 데이터베이스 사용 */
   show tables; /* 테이블 명 확인 */
   alter table table_name add column column_name varchar(16) not null;
   /* 테이블 수정 - 컬럼 추가 */
   ```

   이렇게 반영이 안 된 속성을 데이터베이스에서 직접 추가해주는 방법도 있다

3. 그냥 다시 만들기

   * ~~정확한 이유는 기억이 안나는데 1, 2번 방법 모두 잘 안돼서 짜증 났던 적이 있던 것 같다.  그래서 귀찮아서 그냥 지워버리고 다시 만들었다. 근데 이렇게 하면 생성하고 권한 부여까지 다시 해야한다 어쩌면 이게 더 귀찮을지도 .. 그래도 뭔가 잘 안될 때는 그냥 밀어버리는게 최고다~~ 

     ```mysql
     drop table table_name; /* 테이블 삭제 */
     drop database db_name; /* 데이터베이스 삭제 */
     
     mysql -u root -p
     create database db_name character set utf-8;
     grant all on db_name.* to 'user_name'@'host';
     flush privileges; /* 사용자를 추가, 삭제, 권한 변경 등을 수행했을 때 변경 사항 반영하기 위해 사용하는 명령어 insert, delete, update 명령을 통해 변경했을 때만 해주면 된다 grant 명령어 사용했을 때는 안해도 됨*/
     ```

4. 방금 찾은 거 ~~다른 거 구글링 하다가 얼떨결에 찾음~~
   
   * `python manage.py migrate --run-syncdb` 명령어로 동기화



## django 이미지 파일 저장, 불러오기

> 사용자가 첨부한 이미지를 정해진 경로에 저장하고 db에는 파일명을 저장한다.
>
> pillow가 필요하다



### setting.py

```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```



### urls.py

```python
urlpatterns = [
    ...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
# 애플리케이션 폴더 내의 urls.py 말고 프로젝트 폴더에 있는 urls.py에 설정해준다
```



### .html (이미지 입력 받는 폼)

```html
<input type="file" name="" accept="image/*" multiple>
<!-- 이미지 파일의 모든 확장자를 허용, 즉 이미지 파일이기만 하면 확장자는 상관 없다 jpg든 png든 .. multiple 쓰면 이미지 파일 여러 개 받을 수 있음-->
```



### views.py

```python
def NAME(request):
    try:
        변수 = request.FILES['html에서 지정한 name']
    except:
        변수 = None
# 이미지 안 넣는 경우도 있어서 try except 문으로 처리해줌
```



### .html (이미지 보여줄 html)\

```html
<img src = "{{ 넘겨준키이름.이미지속성명.url }}">
```



## Django QuerySet

> 전달받은 모델의 객체 목록



### all()

```python
from app_name.models import model_name

model_name.objects.all()
```

모든 데이터 가져옴, 반환되는 객체는 QuerySet

해당하는 값이 없을 때 DoesNotExist 메시지 반환



### get()

```python
model_name.object.get(column_name='')
```

하나의 row만 가져옴, 반환되는 객체는 object



### filter()

```python
model_name.object.filter(column_name='')
```

()안의 조건을 만족하는 모든 row를 가져옴, 반환되는 객체는 object

해당하는 값이 없을 때 빈 쿼리셋을 불러옴



### create()

```python
model_name.object.create(column_name='')
```



### save()

```python
q = model_name(column_name='', ...)
q.save()
```

