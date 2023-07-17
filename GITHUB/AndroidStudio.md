## GITHUB와 AndroidStudio 연동

### 1. AndroidStduio

- File -> Setting -> Git
- Test 버전 확인 (작성일 기준 version 2.39.1 유사)

</br>

### 2. Github 토큰 발급

- github 홈페이지 -> 프르필 클릭
- Settings -> Developer settings
- Personal access tokens -> Tokens(classic)
- Generate new token -> Generate new token (classic)

- Note : 발급할 토큰에 대한 이름 or 설명
- Expiration : 유효기간 설정
- repo, admin:org, gist 체크

- 토큰 시리얼 번호 복사

</br>

### 3. AndroidStudio
- File -> Setting -> Github
- Add account -> Log in with Token
- 토큰 입력 -> Add Account


</br>
</br>

## Repository 연동


#### 1. Android Studio VCS -> Create Git Repository

- 연결하고자 하는 폴더 선택
- 폴더 안에 git 파일 생성
- 깃허브 사이트에 새로운 repository 생성

</br>

- github 터미널 연결
```
git remote add origin url
```
```
//정사 연결 확인
remote add origin url
```

</br>

- git -> commit
```
붉은색 파일 : 변동 파일
하나만 체크 = git add 파일명과 동일
전체 체크 = git add . 과 동일
하단 입력칸에 커밋 메세지 입력 = git commit -m “커밋 메세지” 와 동일
Commit / Commit and Push > 상황에 맞게 사용
```

</br>

- git push 

</br>

#### 2. Android Studio VCS -> Share Project on Github


