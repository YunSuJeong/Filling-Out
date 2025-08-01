# Components
> 화면을 구성하는 **조각(UI) 을 하나의 함수로 만든 것**  
> → 그리고 그 함수를 HTML 태그처럼 써서 화면에 붙일 수 있다

**코드를 깔끔하게 관리하고, 재사용하기 위해서 컴포넌트를 .tsx 파일로 분리하여 관리한다.**  

### tsx파일
- TypeScript + JSX 확장자, 즉 "타입 안정성을 가진 React 컴포넌트 파일" 이라고 생각하면 된다.
- 파일 이름은 보통 컴포넌트 이름이랑 똑같이 지음
  - 예: Header.tsx → Header라는 컴포넌트 포함
- **컴포넌트 이름은 대문자로 시작**해야 함 (React 규칙)

## 자주 쓰이는 기본 컴포넌트
| 컴포넌트               | 역할                      |
| ------------------ | ----------------------- |
| `View`             | HTML의 `div`처럼 레이아웃 컨테이너 |
| `Text`             | 텍스트 출력                  |
| `Image`            | 이미지 표시                  |
| `TouchableOpacity` | 터치 가능한 버튼               |
| `FlatList`         | 리스트 반복 출력               |
| `ScrollView`       | 스크롤 가능한 뷰               |

### `<View>` vs `<SafeAreaView>`
> `<View>` 컴포넌트 내에 `<CalendarList>`를 이용하여 스와이프 기본 달력을 구현하는 도중, 달력 위치가 밀려보이는 현상이 있었다.  
> **`<View>`를 `<SafeAreaView>`로 변경하여 해결**했고, ChatGPT도 잡아주지 못한 오류여서 기록해놓으려고 한다.

| `<View>` | `<SafeAreaView>` |
| ----------- | -------------------- |
| 노치/상단바 무시   | 시스템 UI 영역 피해서 안정적    |
| 렌더링 깨질 수 있음 | 스와이프 정렬 포함 레이아웃 안정   |


## 컴포넌트 기본 구조
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
- import한 이름이 곧 태그명이 됨
- import할 때 정하는 이름은 꼭 파일명이랑 같을 필요는 없지만, **코드 일관성/가독성을 위해 “파일명 = 컴포넌트명 = import 이름”으로 맞춰서 쓰기**
- 첫 글자는 대문자!
  - 소문자로 시작하는 JSX 태그는 HTML 태그로 처리
``` tsx
import Header from './Header';

export default function MyComponent() {
return <Header />
``` 

### 2. export default function ...()
- **export : 이 파일 밖에서 이 컴포넌트를 쓰겠다는 뜻**
- 이 컴포넌트의 본체라고 생각하면 됨, 화면에 보여질 내용 정의하는 부분  
- return(...)안에 실제 렌더링할 JSX UI 구조를 작성한다.

### 3. StyleSheet.create()
- 스타일을 정의하는 부분
- CSS처럼 쓰지만 JS 문법을 사용한다.

