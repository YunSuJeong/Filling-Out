<img width="859" height="43" alt="image" src="https://github.com/user-attachments/assets/7dd83ff2-0d91-481b-bd86-627f0b638690" /># github repository 연동하기
*📌 OS환경 : Mac OS**

### 순서
1. Git 설치
2. GitHub에 연동 할 레파지토리 생성
3. Git 초기 설정 및 로컬 저장소 지정
4. GitHub에 파일 올리기

## 1. Git 설치
아래 명령어로 git이 설치되어있는지 확인하기  
Mac은 기본적으로 설치가 되어있다더라, 설치되어있지 않다면 homebrew를 이용하여 Git을 설치하면 된다.
```
git --version
```
<img width="724" height="60" alt="image" src="https://github.com/user-attachments/assets/9995505c-55f7-4cf2-9a4f-2b006b912673" />

## 2. GitHub에 연동 할 레파지토리 생성
GitHub에 로그인하기. 계정이 없다면 회원가입해야한다.

### 원격저장소(=레파지토리) 생성
두 가지 경로 중 아무데서나 New버튼을 클릭하여 레파지토리 생성화면으로 진입한다. (첨부한 이미지 참고)  
이미 생성했다면 패스해도 된다.  

> 1. https://github.com/ 화면의 좌상단
> <img width="612" height="228" alt="image" src="https://github.com/user-attachments/assets/5631a7f3-7646-4525-91fa-2bdfcdfe7b50" />
>  
> 2. 본인 GitHub의 'Your Repositories' 탭 우상단  
> <img width="613" height="179" alt="image" src="https://github.com/user-attachments/assets/89bbf3ab-f6c2-4945-a72c-3caca036ce88" />

New버튼을 클릭하면, 아래와 같은 화면이 나온다.  
원하는 레포지토리명과, 공개범위 및 README파일 선택하고 레파지토리 생성 버튼을 눌러 생성해준다.

<img width="554" height="540" alt="image" src="https://github.com/user-attachments/assets/8915f704-505b-404e-88e8-c04081308066" />

생성한 레포지토리로 이동되며 생성이 완료된다!

## 3. Git 초기 설정 및 로컬 저장소 지정
### 3-1. Git 초기 설정하기
맥에서 터미널을 열어준다.  
아래 명령어를 이용하여 초기 계정을 설정해준다.  
```
git config --global user.name "본인 github name"
git config --global user.email "본인 github email"
```
<img width="859" height="43" alt="image" src="https://github.com/user-attachments/assets/65516215-e640-4f52-9277-6959e8e63d78" />

### 3-2. 로컬 저장소 지정해주기
초기 설정을 완료하면 Finder를 열어 깃허브에 올릴 파일 위치로 간다.  
**내가 올릴 파일의 상위폴더**를 선택 → 우클릭 → '폴더에서 새로운 터미널 열기' 클릭하여 터미널을 연다.

<img width="314" height="516" alt="image" src="https://github.com/user-attachments/assets/ff9d06f8-6fa4-40a4-a0fe-b11ed73ccf57" />

해당 터미널에 아래 명령어를 입력하여 해당 폴더를 로컬 저장소로 지정해준다.
```
git init
```

로컬 저장소로 지정한 후, 폴더로 들어가보면 .git 파일이 생성되어 있는 것을 확인 할 수 있다.  
`숨겨진 파일 확인 단축키 : cmd + shift + .`

<img width="476" height="312" alt="image" src="https://github.com/user-attachments/assets/8b926f95-8f3b-4e2f-bea4-1d4cfa1fbf40" />


## 4. GitHub에 파일 올리기
이 단계가 Git과 Github를 연동해주는 단계이다.  

연동은 4단계로 이루어지는데, 아래와 같다.
> 1. git add .  
> 2. git commit -m "message"  
> 3. git remote add origin "my github url"
> 4. git push origin main

3단계에서 작업했던 터미널에 아래 순서대로 진행한다.

### 4-1. git add .
이 명령어는 가상 공간에 파일을 1차로 추가하는 과정이다. 
터미널에서 아래 명령어를 실행한다.
```
git add .
```

> **⚠️ "does not have a commit checked out" 에러 발생 시, 해결 방법**  
> 3-2단계에서 지정한 폴더 위치로 가서 하위폴더의 .git파일 삭제한 후, 다시 명령어 실행해주기
> 
> 더 자세한 설명은 [여기서](https://github.com/YunSuJeong/Filling-Out/blob/main/Git/%5B%EC%97%90%EB%9F%AC%5D%20does%20not%20have%20a%20commit%20checked%20out.md) 확인

### 4-2. git commit -m "message"
이 명령어는 가상 공간에 파일을 최종 저장하는 단계이다.
`"message"`부분은 커밋메시지이므로 본인이 알아서 작성하면 된다.

### 4-3. git remote add origin "my github url"
드디어 원격저장소(레포지토리)와 로컬저장소를 연결하는 단계이다.!

아래 명령어로 원격저장소와 로컬저장소가 연결되어있는지 확인해보자.
아무것도 뜨지 않는다면 연결되어 있지 않은 것이다.
```
git remote -v
```

이제 아래 명령어로 연결해보자.  
`"my github url"`에는 2단계에서 생성했던 레파지토리 url을 적어주면 된다. (레파지토리 url 확인 방법은 명령어 하단 이미지 참고)
```
git remote add origin "my github url"
```
**레파지토리 url 확인 방법**  
아까 생성한 레포지토리의 '<> Code'탭 → Code버튼 클릭 → url복사
<img width="614" height="306" alt="image" src="https://github.com/user-attachments/assets/1d0c0fc4-01c5-42b9-a6be-b0b70e430a69" />

> **⚠️ 명령어를 실행하면, username과 password를 입력하라고 나온다.**  
> `UserName`은 gitHub에서 사용하고 있는 username 그대로 작성하면되지만,  
> `Password`는 gitHub암호가 아닌, **토큰을 작성**해주어야한다. (깃허브 정책 변경때문)  
>
> - 🙆🏻 토큰 발급하여 잘 메모해둔 사람 : 복사해둔 토큰을 입력
> - 🤷🏻 토큰은 발급했지만 모르는 사람 : 재발급 받아서 입력 (+꼭 어딘가에 메모해놓기)
>   - 내가 여기에 해당하는 경우였는데, 재발급이 아닌 신규발급한 토큰으로는 연동이 안되는 상황이 있었다...
>   - 혹여나 누군가는 나와 같은 상황이 없길 바란다ㅠ
> - 🙅🏻 아예 발급이력이 없는 사람 : 신규 발급 받아서 입력 (+꼭 어딘가에 메모해놓기)
> 
> 혹여나 토큰 발급 방법을 모르는 사람은 (여기서)[] 확인

여기까지 완료했다면 다음단계로 넘어가기 전, 연결확인 명령어를 실행하여 연결에 성공했는지 확인해보자.

### 4-4. git push origin main
여기까지 했다면 이제 원격저장소로 파일을 올릴 수 있는 상태가 됐다! (와)  

`origin`은 원격 저장소의 주소, `main`은 최초 생성되는 브랜치이다.  
혹시 본인이 생성한 프로젝트 브랜치명을 바꾼 적이 있다면 바꾼 브랜치명으로 작성해주면 된다.  
(다른 블로그 기준으로 무작정 master로 했다가 안보여서 당황했다.)

이제 아래 명령어를 입력해보자.
```
git push origin main
```

잘 push됐다면 gitHub 레포지토리에서도 파일이 잘 올라왔나 확인하면 끝!
👏🏻👏🏻👏🏻


**[참고 블로그]**
https://wg-cy.tistory.com/343
