# 기초

- 주석 : `#`
- 파이썬에서는 `long`형이 따로 없다. 대신, `int`형에 어떤 크기의 정수든지 담을 수 있다.
## 문자열
  - `'hello python'` 작은 따옴표를 이용하여 작성
  - `"hello I'm python"` 큰 따옴표도 작은 따옴표와 동일. 큰 따옴표 안에 작은 따옴표가 포함되어도 됨.
  - `''' 또는 """`와 같이 세개의 따옴표로 묶여진 문자열은 여러줄에 걸친 문자열에 사용한다. 작은 따옴표든 큰 따옴표든 마음대로 사용이 가능.
    ```python
    ''' hello
    "python"
    '''

    """hello
    'python'
    """
    ```
  - 한번 만들면 수정이 불가
  - 포맷팅
    ```python
    age = 1
    name = 'ye'
    print ('{0} was {1} years old when he wrote this book'.format(name, age))
    print ('Why is {0} playing with that python?'.format(name))
    print ('{} was {} years old when he wrote this book'.format(name, age))
    print ('Why is {} playing with that python?'.format(name))
    ```
    ```python
    # 소수점 아래 셋째자리까지
    print ('{0:.3f}'.format(1.0/3))
    # _로 11칸을 채우고 가운데 정렬(^)하기
    print('{0:_^11}'.format('hello'))
    # 사용자 지정 키워드 이용
    print ('{name} plays {game}'.format(name='ye', game='overwatch'))
    ```
  - `print`는 줄을 바꿈.
    + 줄을 바꾸지 않기 위해서
      ```python
      print ('a', end='')
      print ('b')           # ab
      print ('a', end=' ')
      print ('b')           # a b
      ```
  - 이스케이프 문자
    ```python
    'What\'s your name?'
    'first line\nsecond line'
    'hello\tpython'

    # equal first line. second line.
    "first line. \
    second line."
    ```
  - 순 문자열
    + 문자열 내에 포함된 이스케이프 문자 등을 처리하지 않고 그대로 출력한다.
    + 문자열 앞에 r 또는 R을 붙인다.
    + 정규 표현식 사용 시 순 문자열 사용
## 흐름 제어
### if
```python
if 1 == 2:
  print('1 == 2')
elif 1 < 2:
  print('1 < 2')
else:
  print('1 > 2')

# 잠깐! 사용자한테 입력받기는?
# input('입력하세용')

# 최소한의 if문 사용
if True:
  print('true')
```
- 파이썬에는 `switch`문이 없어서 `if..elif..else`문을 사용하여야 한다.
### while
```python
number = 55
running = True

while running:
  guess = int(input('Enter an integer : '))

  if guess == number:
    print('You guessed it.')
  elif guess < number:
    print('It is a higher than that.')
  else:
    print('It is a lower than that.')

else:
  print('Loop is over')

print('Bye!')

# while 루프에 else문 사용 가능
```
### for
```python
for i in range(0, 5):
  print(i)
else:
  print('Loop is over')
```
- 파이썬에 내장된 `range`함수를 통해 숫자의 나열을 생성
  + `range(0, 5, 2)` 처럼 세번째 매개변수는, 세번째 매개변수만큼 증가하는 리스트를 반환
  + `range`함수는 호출될 때 해당 범위 내의 모든 숫자를 한번에 생성하여 반환하므로, 매우 큰 숫자 범위를 지정해주면 시간이 오래 걸림
  + 따라서 매우 큰 범위의 숫자를 다룰 때는 한번에 하나씩 숫자를 생성하도록 하자.
  + 이 경우에는 `xrange()`를 대신 사용할 수 있음
- `else`문을 포함할 수 있음. `break`문으로 강제로 빠져나오지 않는 한 루프를 다 돌면 항상 실행됨.
### break
루프를 강제로 빠져나오고 싶을 때 사용하며 `break`문을 통해 빠져나오면 `else`문은 실행되지 않음
### continue
현재 실행중인 루프 블록의 나머지 명령문들을 실행하지 않고 다음 루프로 넘어가도록 함
