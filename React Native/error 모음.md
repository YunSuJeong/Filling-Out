# 리액트 에러 모음
> 에러는 나를 항상 당황하게 한다.


## Invalid hook call
> ❌ Hook을 잘못된 위치에서 호출했을 때 발생하는 오류

### 예: `useNavigation()` hook함수 
```tsx
import React from 'react';
import { useNavigation } from '@react-navigation/native';

const navigation = useNavigation();   // ❌ 잘못된 예시 : 함수 컴포넌트 바깥

const Header = () => {
  const navigation = useNavigation();   // ✅ OK: 컴포넌트 내부니까 가능

  return (
    <TouchableOpacity onPress={() => navigation.navigate('편집')}>
      <Text>편집</Text>
    </TouchableOpacity>
  );
};
```


