# N사 해커톤 코딩테스트
2020.4.11

3문제 2시간이었는데 1,2번은 쉬웠고 3번이 까다로웠다.  
10분 남겨두고 풀었는데 부등호 부분을 잘 못 생각해서 결국 틀렸다.  

## 문제풀이
스키,슬로프 번갈아가면서 만드는건데 문제를 올리면 안되는것같고..  
어쨋든 핵심은  
**f(p,q,r) : p개의 공을 q개의 방에 넣는 경우의수(하나의 방에 공은 최대 r개만 넣을 수 있다)** 를 식으로 쓰는 것이었다.  
최대 중복갯수가 정해진 중복순열 문제?  
최대r개만 넣을 수 있기 때문에 고등학교때 배운 수학으론 못푼다.  

점화식을 써보면
f(p,q,r) = SUM(f(p-k,q-1,r)) (k는 0~r)  
메모이제이션을 이용하기 때문에 O(p*q)로 풀 수 있다.

## 코드
```python
memo =[[[-1 for k in range(151)]for j in range(151)]for i in range(151)]

def solution(n, m, k):
    if not(n<=m and m<=k*n):
        return 0

    p1 = (m-n)//2
    q1= n//2
    p2 = (m-n)//2
    if n%2==1:
       q2 = n//2+1
    else :
       q2 = n//2

    c1 = f(p1,q1,k)
    c2 = f(p2,q2,k)
    answer = (c1*c2)*2

    return answer%1000000007

def f(p,q,r):
    global memo
    
    if p<0:
       return 0
    if q==1:
        if p>=r: return 0
        else: return 1
    
    if not memo[p][q][r]==-1:
        return memo[p][q][r]
    
    count = 0
    for k in range(r):
        count += f(p-k,q-1,r)
        count %=1000000007
    
    memo[p][q][r]=count

    return count


print(solution(50,150,20))
```
