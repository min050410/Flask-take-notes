## Learn_Flask 
> <a href="https://github.com/min050410/Flask-take-notes/tree/master">View my code</a>    


### 개발시에 시간이 오래 걸렸거나 헷갈렸던 것들 모임  
> #1  
- `GET`은 서버의 리소스에서 데이터를 요청할 때, `POST`는 서버의 리소스를 새로 생성하거나 업데이트할 때 사용한다.  
- DB로 따지면 `GET`은 `SELECT` 에 가깝고, `POST`는 `Create` 에 가깝다고 보면 된다.

> #2  
- `html` or `css href` 안에(이미지 파일참조 모두 포함) 
```html
href = "{{url_for('static', filename='main.css')}}"
```
> #3
```bash  
export FLASK_APP=__init__  
export FLASK_ENV=development  
```
- 우분투 환경에서는 `set` 이 `export` 이다. 참고!!  
- `.bash` 파일에서 환경변수를 이렇게 설정해야   
`flask run`을 쓸수 있고 애플리케이션 환경에서 개발 가능하다.
```ubuntu
flask run --host=0.0.0.0 --port=8000
```
> #4  

__*"역시 믿고보는 stackoverflow"*__  
```ubuntu
flask db stamp head
```
- 현재 리비전을 최종 리비전으로 변경하는 명령어  
그 후에 `migrate`와 `upgrade` 진행  
```ubuntu
flask db migrate  
flask db upgrade
```
  
`flask db upgrade`를 꼭 해야만 `db.session.commit()`이 가능해진다  
  
  
> #5

```python
def detail(post_id): #매개변수에는 <int:post_id>가 들어감  
	post = Post.query.get_or_404(post_id)  
	return render_template('post_detail.html', post=post)  
```

- 보면 `detail`의 매개 변수에는 `post_id`이다.  
`templetes` 에서 블루프린트 `detail`을 참조할 때,  
`post_id=post.id`로 들어가야 한다 (왼쪽이 `매개변수` 오른쪽이 `db`)  
아, 또 블루프린트를 참조할 때 __꿀팁__  
`url_for('main.detail')` main은 blueprint 이름, detail은 blueprint 함수 이름

> #6  
- 플라스크 폼 모듈을 사용할 때  
`Secret_key` 무조건 필요    
`config.py` 에 정의 해야 한다.  
~~+ 폼 모듈 너무 좋아요~~

> #7  

이 문제에 삽질한 횟수  
  
![image](https://user-images.githubusercontent.com/45661217/134806966-9ee02c84-74f4-4b6d-aed4-46daea631f67.png) 
  
`gunicorn` 을 사용할 때 모듈 네임드 에러가 계속 발생했었다.  
`flask run` 사용시 잘 되었지만  
`gunicorn`을 사용할 때만 모듈 상대 참조 오류가 계속 일어났다.    
```ubuntu
gunicorn --bind 0:8080 "zelda:create_app()"  
```
`__init__ :create_app()` 이 아닌 그 상위 디렉토리인 zelda로 설정해 줘야  
정상적인 참조가 가능하다.  
또, 디렉토리가 ch01 - zelda - \_\_init\_\_ 이런 배치로 있다면  
`flask run` 과 달리 상위 디렉토리 ch01에서 명령어를 입력해야 한다.  
> 초보적인 실수지만 참조 오류는 뼈아프다는걸 깨달았다.. ㅠㅠ   

