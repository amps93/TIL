# 재귀함수

* 재귀함수는 종료조건을 반드시 명시해야함

```python
def recursive_function(i):
    #100번째 호출을 했을때 종료되도록 종료 조건 명시
    if i == 100:
        return
    print(i, '번쨰 재귀함수에서', i+1, '번째 재귀함수를 호출합니다')
    recursive_function(i+1)
    print(i,'번째 재귀함수를 종료합니다.')
    
recursive_function(1)    
```



## 팩토리얼 구현 예제

* n! = 1x2x3x ... x(n-1)xn

```python
def factorial_recursive(n):
    if n <= 1: #n이 1이하인 경우 1을 반환
        return 1
    #n! = n*(n-1)!를 그대로 코드로 작성
    return n*factorial_recursive(n-1)

print('재귀 : ',factorial_recursive(5))
```



## 최대공약수 계산(유클리드 호제법)

* 유클리드 호제법
  * 두 자연수 A, B에 대하여 (A>B) A를 B로 나눈 나머지를 R이라고 한다
  * 이때 A와B의 최대공약수는 B와 R의 최대공약수와 같다
* 유클리드 호제법의 아이디어를 그대로 재귀함수로 작성할 수 있다
  * 예시 : GCD(192, 162)

| 단계 | A    | B    |
| ---- | ---- | ---- |
| 1    | 192  | 162  |
| 2    | 162  | 30   |
| 3    | 30   | 12   |
| 4    | 12   | 6    |

```python
#최대 공약수 계산(유클리드 호제법)
def gcd(a,b):
    if a%b == 0:
        return b
    else:
        return gcd(b,a%b)

print(gcd(192,162))
```



## 재귀 함수 사용의 유의 사항

* 재귀 함수를 잘 활용하면 복잡한 알고리즘을 간결하게 작성할 수 있다
  * 단, 오히려 다른 사람이 이해하기 어려운 형태의 코드가 될 수 있으므로 신중하게 사용해야 한다
* 모든 재귀함수는 반복문을 이용하여 동일한 기능을 구현할 수 있다
* 재귀함수가 반복문보다 유리할 수도 불리할 수도 있다
* 컴퓨터가 함수를 연속적으로 호출하면 컴퓨터의 메모리 내부에 스택프레임에 쌓인다
  * 그래서 스택을 사용해야 할 때 구현상 스택 라이브러리 대신에 재귀함수를 이용하는 경우가 많다



참고 코드 : PythonStudy/00_SideStudy/01_Algorithm/22_recursive_function.py
