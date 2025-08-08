# BigInteger
  Long형보다 큰 범위의 정수를 다뤄야 할 때 사용하는 클래스
  **java.math**에 속한다.
  산술연산자 사용이 불가능하며, 클래스에서 제공하는 메서드를 사용해야한다.

## 사칙연산
  - add() : 덧셈
  - subtract() : 뺄셈
  - multiply() : 곱셈
  - divide() : 나눗셈
  - remainder() : 나머지
    
## 배열 
**long형보다 큰 수**를 배열에 저장해야 할 때 사용!

### 예시) 조합 계산
```java
// BigInteger형 배열 선언
BigInteger arr[][] = new BigInteger[N+1][N+1];

// 조합 계산
for(int i=0; i<=N; i++) {
  for(int j=0; j<=i; j++) {
    if( j == 0 || j == i ) arr[i][j] = BigInteger.valueOf(1);
    else arr[i][j] = arr[i-1][j-1].add(arr[i-1][j]);
  }
}
```
