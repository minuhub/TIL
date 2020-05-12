## python의 람다함수와 map,reduce,filter

## 람다함수(익명함수)

파이썬의 일반적인 함수
```python
def sumFunction(x,y):
  return x+y

>>>sumFunction(1,2)
3
```

함수를 한번만 만들어 쓰려면? 굳이 이름을 지어 줄 필요X
람다함수(익명함수)
```python
>>>(lambda x,y:x+y)(1,2)
3
```


## map(함수,리스트)
리스트에서 하나씩 꺼내어 함수 적용후 객체 반환

```python3
>>> list(map(lambda x:x*2, range(5)))
[0,1,2,3,4]
```

## reduce(함수,순서형자료)
순서형자료에서 하나씩 꺼내어 누적으로 함수 적용후 리스트로 반환

```python3
>>> from functools import reduce
>>> reduce(lambda x,y:x+y,[0,1,2,3,4])
10
```
## filter(함수,리스트)
리스트에서 하나씩 꺼내어 조건 적용 후 참인것만 객체 반환

```python3
>>> list(filter(lambda x:x<3,range(10))
[0,1,2]

```
