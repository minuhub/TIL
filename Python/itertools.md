## python의 순열, 조합 경우의 수를 뽑을 때 itertools를 이용하자

product : 데카르트곱  
permutations : 순열  
combinations : 조합   
combinations_with_replacement : 중복조합  

```python
import itertools
list(itertools.permutations("ABCD",2))
```
이런 형태로 쓸 수 있다.  


## 참고 0~14 자리에서 3자리 뽑는 방법을 list로 만들어야 할 때
백준 17135번을 풀다가

3중 for문으로 뽑으려면 이렇게 길게 써야한다.
```python
cnt = 0
for i in range(M):
	archor[cnt] = i
	cnt+=1
	for j in range(i+1,M):
		archor[cnt] =j
		cnt+=1
		for k in range(j+1,M):
			archor[cnt]=k
		cnt -=1
	cnt -=1
```

itertools 의 조합을 사용하면 아래와 같이 빠르고 쉽게 코딩 가능하다.

```python
import itertools
l = [i for i in range(15)]
list(itertools.combinations(l,3))
```



