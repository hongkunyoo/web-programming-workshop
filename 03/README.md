# 파이썬 기본

## 장점

1. 배우기 쉽고 사용하기 편리함
2. 여러 필드에서 사용 - 웹 프로그래밍, 기계학습
3. 생산성이 높음


## 파이썬 설치

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash Miniconda3-latest-Linux-x86_64.sh -f -b
echo "export PATH=$HOME/miniconda3/bin:$PATH" >> ~/.bashrc

which python
```

## 파이썬 기초

### 특징

#### 들여쓰기

파이썬은 꼭 들여쓰기를 맞춰야 함.

#### 세미콜론 없어도 됨

```python
print('hello');
print('hello')
```

#### 동적 타입

타입이 동적으로 변경이 될 수 있다.
```python
abc = 1
abc = "string"
```


#### 실행자와 실행파일

- executor: `python`
- executable file: `.py`


### 자료형

#### int

```python
abc = 1
abc = 20
```

#### float

```python
abc = 1.1
```

#### string

```python
abc = "string"
abc = 'other string'

print(abc)

# placeholder
friend = "bob"
me = "tonny"

abc = "hello %s my name is %s" % (friend, me)
print(abc)

abc = "hello {} my name is {}".format(friend, me)
print(abc)
```

#### Boolean

```python
abc = True
abc = False
```

#### 리스트

```python
abc = [1,2,3]
```

#### 딕셔너리

```python
abc = { "key": "value", "abc": 123 }
```

#### 셋

```python
abc = {1,2,3}
```

### 함수

```python

def abc(abc):
	abc = abc + 1
	return abc

abc(123)
```

### 클래스

```python
class A:
    volume = 0

    def play(self):
        song = []
        for i in range(self.volume):
            song.append("play")
        return " ".join(song)

    def set_volume(self, volume):
        self.volume = volume

    def reset(self):
        self.volume = 0


a = A()

a.play()
a.set_volume(10)
a.play()
a.reset()
```

### 흐름제어


#### if

```python
if a == 1:
	print('1')
elif a == 2:
	print('2')
else:
	print('else')
```


#### and & or

```python
if (a == 1) and (b == 2):
	print('1')
elif (a == 2) or (b == 3):
	print('2')
elif not (a == 4):
	pass
else:
	print('else')
```


#### while

```python
count = 0
while True
	print(count)

	if count > 10:
		break
	count += 1
```

#### for

```python
for i in range(10):
	print(i)
```

### import


```python
import os

lists = os.listdir()

for l in lists:
	print(l)
```


### sys.argv

파이썬 실행시 파라미터를 넘기고 받을 수가 있다.
아래와 같이 파이썬을 실행합니다.

```bash
python arg-test.py a b c 123
```

```python
import sys

val0 = sys.argv[0]
val1 = sys.argv[1]
val2 = sys.argv[2]
val3 = sys.argv[3]
val4 = sys.argv[4]


print(val0, val1, val2, val3, val4)

# 혹은

print(sys.argv)
```


## 파이썬 패키지 설치

`pip` 패키지 매니저. 파이썬용 신규 패키지를 설치할 수 있다.


아래와 같은 YAML 파일을 생성합니다.
```yaml
# conf.yaml

abc: 123
dic:
  a: 1
  b: 2
  c: [1,2,3]
l:
- abc
- def
- inner_dic:
    in_a: 1
    in_b: 2
```

그리고 난 후 아래와 같이 실행합니다.
```python
import yaml

with open("conf.yaml") as f:
    conf = yaml.load(f)

print(conf)
```

yaml 패키지가 없다고 에러가 납니다. `pyyaml`을 설치하고 다시 위의 스크립트를 실행해 보자.

```bash
pip install pyyaml
```

### :trophy: Do it more #1

특정 디렉토리를 파라미터로 전달하면 그 아래에 있는 모든 파일 및 디렉토리를 출력해주는 파이썬 프로그램을 만들어라.

```python
# 예시

python dir.py /usr
# bin
# bin/apt-extracttemplates
# bin/apt-ftparchive
# bin/apt-get
# ....
# games
# games/...
# games/...
# include
#...
```

*힌트* `os.path` 모듈을 참고하시오.


### :trophy: Do it more #2

파이썬을 이용하여 자료 구조 stack을 구현하라.
API Requirement는 다음과 같다.

```python
# 다음과 같은 class를 만드시오.
stack = Stack()

stack.push('a')
stack.push(1)
stack.push([1,2,3])
stack.push(1.1)
stack.push("String")

item = stack.pop()
print(item)
# String

stack.reverse()
print(stack.pop())
# a

print(stack.is_empty())
# False
```

[Requirement]
- `push`: stack에 item을 삽입한다.
- `pop`: stack에서 맨위의 item을 꺼낸다.
- `reverse`: stack의 순서를 반대로 바꾼다.
- `is_empty`: stack이 비었는지 체크한다.