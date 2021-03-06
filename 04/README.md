# 웹 백엔드

웹 백엔드는 서버 로직을 구현하는 메인 컴포넌트입니다. web 서버, DB 서버와 통신하여 서버의 중심 역할을 담당합니다. 웹 백엔드의 구현체는 다양하게 있습니다. 언어에 따라서 다르고 같은 언어 안에서도 다양하게 나뉩니다. 몇가지 예시를 보겠습니다.

- java
	- Servlet
	- Spring
	- Struts
- ruby
	- Ruby On Rails
- python
	- *Flask*
	- *Django*
- php
	- Laravel
	- CodeIgniter
- nodeJs
	- Express
	- AdonisJs

본 워크샵에서는 [flask](https://flask.palletsprojects.com/en/1.1.x/)를 사용할 예정입니다. 

#### flask 장점
- 가볍다
- 배우기 쉽다.
- 기능이 간단하다.
- 작은 웹앱에 적당하다.

#### flask 단점
파이썬의 또 다른 웹 프레임워크 강자 Django(장고)와 비교하여
- 기능이 빈약하다.

하지만 본 워크샵에서 실습하기에 flask도 충분하기에 배우기 쉬운 flask로 사용할 예정입니다. 그리고 flask를 배우고 Django를 배우면 무척 쉽게 옮겨갈 수 있습니다.

## flask 설치

```bash
pip install flask
```

## flask 기초

### basic

다음과 같이 `app.py` 파일을 생서합니다.

```python
# app.py
from flask import Flask
app = Flask(__name__)


@app.route('/')
def hello():
    return "Hello World!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

`app.py` 실행

```bash
python app.py
```

```bash
curl localhost:5000

# 혹은 웹 브라우저에서 실행
```

### 라우팅

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello, World'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```


### 파라미터 전달

```python
from flask import Flask
app = Flask(__name__)


@app.route('/')
def hello():
    return "Hello World!"


@app.route('/<name>')
def hello_name(name):
    return "Hello {}!".format(name)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

```python
from flask import Flask
app = Flask(__name__)

@app.route('/user/<username>')
def show_user_profile(username):
    # show the user profile for that user
    return 'User %s' % username

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # show the post with the given id, the id is an integer
    return 'Post %d' % post_id

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```


### HTTP method

```python
from flask import Flask
from flask import request

app = Flask(__name__)

def do_the_login():
	return "you are logged in"

def show_the_login_form():
	login_template = \
"""
<html>
	<body>
		<form action="login" method="post">

		  <div class="container">
		    <label for="uname"><b>Username</b></label>
		    <input type="text" placeholder="Enter Username" name="uname" required>

		    <label for="psw"><b>Password</b></label>
		    <input type="password" placeholder="Enter Password" name="psw" required>

		    <button type="submit">Login</button>
		    <label>
		      <input type="checkbox" checked="checked" name="remember"> Remember me
		    </label>
		  </div>

		  <div class="container" style="background-color:#f1f1f1">
		    <button type="button" class="cancelbtn">Cancel</button>
		    <span class="psw">Forgot <a href="#">password?</a></span>
		  </div>
		</form>
	</body>
</html>
"""
	return login_template

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return do_the_login()
    else:
        return show_the_login_form()

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```


## 템플릿 사용하기

웹 템플릿을 생성하는 방법에 대해서 알아 봅니다. 먼저 사용자에게 환영 문구를 보내주는 웹 어플리케이션을 만들어 봅시다.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/<username>')
def login(username):
    homepage_name = 'Oreo'

    welcome_msg = \
"""
<html>
	<body>
		<div>
			<h1>Hello %s</h1>
			<p>Welcome to my home page, %s</p>
		</div>
	</body>
</html>
""" % (username, homepage_name)
    return welcome_msg
    

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

매번 이렇게 html 파일을 app.py 파일 안에서 생성하는 것이 비효율적으로 보입니다. 그래서 나눠봅시다.

```bash
mkdir templates
```

welcome.html
```html
<html>
	<body>
		<div>
			<h1>Hello {{ username }}</h1>
			<p>Welcome to my home page, {{ homepage_name }}</p>
		</div>
	</body>
</html>
```

```python
from flask import Flask
from flask import render_template


app = Flask(__name__)

@app.route('/<username>')
def login(username):
    homepage_name = 'Oreo'
    return render_template('welcome.html', username=username, homepage_name=homepage_name)
    

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```


#### template에 딕셔너리 전달

welcome2.html
```html
<html>
	<body>
		<div>
			<h1>Hello {{ value.username }}</h1>
			<p>Welcome to my home page, {{ value.homepage_name }}</p>
			<p>Today is , {{ value.today }}</p>
		</div>
	</body>
</html>
```

```python
from flask import Flask
from flask import render_template
import datetime

app = Flask(__name__)

@app.route('/<username>')
def login(username):
    homepage_name = 'Oreo'
    value = {}
    value['username'] = username
    value['homepage_name'] = homepage_name
    value['today'] = datetime.datetime.now()
    return render_template('welcome2.html', value=value)
    
    
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

## API 서버 만들기

아래와 같은 json을 리턴하는 API 서버를 만들고자 합니다.

#### Request
```bash

curl IP:5000/api/<USERNAME>
```

#### Response
```json
{
	"username" "<USERNAME>",
	"homepage_name" "<HOMEPAGE_NAME>",
	"today" "<TODAY>"
}
```

api.json
```json
{
	"{{ key1 }}": {{ value1 }},
	"{{ key2 }}": {{ value2 }},
	"{{ key3 }}": {{ value3 }}
}
```

```python
from flask import Flask
from flask import render_template
import datetime

app = Flask(__name__)

@app.route('/<username>')
def login(username):
    homepage_name = 'Oreo'
    return render_template('api.json', key1='username', value1=username, key2='homepage_name', value2=homepage_name, key3="today", value3=datetime.datetime.now())
    
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```


### :trophy: Do it more #1

api.json을 조금 더 범용성 있게 바꿀 순 없을까요?


### :trophy: Do it more #2

HTTP Basic Auth를 이용하여 사용자 로그인 페이지를 구현해 봅시다.

참고 사이트
- https://httpbin.org/
- https://reqbin.com/
