# JSX(JavaScript XML)
**자바스크립트 안에서 HTML처럼 생긴 코드를 쓸 수 있게 만든 문법**  
HTML처럼 생겼지만, 사실은 자바스크립트!

```jsx
const name = "이지듀티";

return (
  <View>
    <Text>안녕, {name}님!</Text>
  </View>
);
```
- `<Text>...</Text>` → HTML 같지만 실제로는 JS 함수
- `{}` 안에 JS 변수/코드가 들어갈 수 있음


## 왜 HTML이 아니라 JSX를 쓸까?
HTML처럼 쓰면 직관적이고 편해  
그리고 자바스크립트를 섞어서 **동적인 UI**를 만들 수 있기 때문!


## HTML이랑은 뭐가 다를까?
|         | HTML          | JSX                                |
| --------- | ------------- | ---------------------------------- |
| 문법        | 태그 기반         | 태그처럼 보이지만 JavaScript               |
| 문서 구성 | 웹페이지 전체 구성    | 컴포넌트 단위로 조립                        |
| 동적 데이터    | ❌ 직접 못 넣음     | ✅ `{}`로 JS 값 삽입 가능                 |
| class 속성  | `class="btn"` | `className="btn"` ← JS와 겹치지 않도록 다름 |
| 닫는 태그     | 없어도 되는 경우 있음  | 항상 닫아야 함 (`<img />` 등)             |
