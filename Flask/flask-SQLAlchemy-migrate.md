# flask Migrate를 이용한 ORM 적용하기

### 📄 flask db migrate

✔️ 모델을 새로 생성하거나 변경할 때 사용한다.  
이 명령을 수행하면 데이터베이스 변경을 처리할 리비전(revision) 파일이 생성된다. - 이름은 무작위로 생성된다. 

### 📄 flask db upgrade
✔️ 모델의 변경 내용을 실제 데이터베이스에 적용할 때 사용한다. 

```ubuntu
flask db migrate  
flask db upgrade
```
이렇게 순서대로 진행하면 `model` 변경 내용 적용이 가능하다

### ❌ 에러 ❌

`migrate`은 성공했지만 `upgrade`를 실패할 경우 다시 `migrate`을 시도할 때 에러가 발생한다.

```ubuntu
flask db stamp head
```
- 현재 리비전을 최종 리비전으로 변경하는 명령어

그 후에 `migrate`와 `upgrade` 진행  
```ubuntu
flask db migrate  
flask db upgrade
```

> `flask db upgrade`를 꼭 해야만 `db.session.commit()`이 가능해진다 