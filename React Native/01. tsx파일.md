# .tsx 파일에 대하여

## .tsx파일은 뭘까
> .tsx는 **TypeScript + JSX** 확장자, 즉 **"타입 안정성을 가진 React 컴포넌트 파일"** 이라고 생각하면 된다.

## 기본 구조
> import → component → style 흐름을 가진다.
``` tsx
// 1. 필요한 모듈(React, 컴포넌트, 스타일 등) 불러오기
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

// 2. 컴포넌트 정의
export default function MyComponent() {
  return (
    <View style={styles.container}>
      <Text>Hello!</Text>
    </View>
  );
}

// 3. 스타일 정의
const styles = StyleSheet.create({
  container: {
    padding: 20,
  },
});
```
### 1. import
- 다른 라이브러리/컴포넌트 가져오는 부분
### 2. export default function ...()
- 이 컴포넌트의 본체하고 생각하면 됨, 화면에 보여질 내용 정의하는 부분  
- return(...)안에 실제 렌더링할 JSX UI 구조를 작성한다.
### 3. StyleSheet.create()
- 스타일을 정의하는 부분
- CSS처럼 쓰지만 JS 문법을 사용한다.
