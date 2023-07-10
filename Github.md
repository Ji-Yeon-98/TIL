# 1. Git과 Github

#### 정의
 * git : 코드 변경 기록, 특정 지점 되돌아감 (버전 관리 도구)

* github : 협업, 백업 (코드 관리해주는 원격 저장소)

</br>
</br>


# 2. Git 명령어


1. 초기화
```
git init
```
- 가장 맨 처음, 버전 관리 시작
- 딱 한번만 입력

</br>

2. 저장하고 싶은 파일 지정 

```
git add <파일명> or git add . 
``````
- . : 모든 파일

</br>

3. 실제 저장

```
git commit -m "기능 개발 관련된 기록"
```

</br>

4. 커밋 내역 확인 
```
git log
```
- 저장한 커밋 내역 확인
- q : 끝내기

</br>

5. 상태 확인
```
git status
```
- 코드의 변경은 있지만 저장을 하지 않은 파일, 브랜치 확인

</br>

6. 복사본 생성
```
git branch <브랜치명> 
```

- 복사본 만듦 
- 새로운 곳에서 코드 짜는 것

</br>

7. 브랜치 변경

```
git switch <브랜치명> 
```
</br>

8. 코드 합치기
```
git merge <새롭게 기능 개발한 브랜치> 
```
- 다른 브랜치에서 만든 코드 합침
- 원본 브랜치에서 입력

</br>

#### vim (텍스트 편집기)

- i : 메세지 입력하기
- esc : 입력에서 나가기
- :wq : 편집기 빠져나오기

</br>
</br>

# 3. Github

#### 1) 내 컴퓨터 코드 올리기

```
git remote add origin <github 주소>
git branch -M main
git push -u origin main
```

- git push할 때 주소 미리 지정
- 기본 브랜치 master -> main
- github에 코드 업로드


##### 수정 후 올릴 때
```
git add .
git commit -m "내용"
git push origin main
```

</br>

#### 2) 협업할 때 Github 사용법

1. github 온라인 저장소 -> 로컬 (내 컴퓨터) 이동

```
//처음인 경우
git clone <주소>

//처음이 아닌 경우
git pull origin main
```

- 협업할 파일 불러오기

</br>

2. 로컬(내 컴퓨터) : 새로운 브랜치 생성

```
git branch <브랜치명>
git switch <브랜치명>
```

- 복사본 생성 후 수정

</br>

3. 로컬(내 컴퓨터) -> github 온라인 저장소
```
git add .
git commit -m "수정 내용"
git push origin <브랜치명>
```
- 새로운 브랜치로 github 올려줌

</br>

4. github 온라인 저장소 : merge

- github 내에서
- Pull requests -> Compare&pull request
- create pull request
- 코드 합칠 수 있는 상태면 merge

</br>

5. 충돌 : 브랜치로 다시 pull
```
git pull origin main

//경고문 뜬 경우
git config pull.rebase false
```
</br>

##### .gitinore

- git으로 관리하고 싶지 않은 파일
- github에 업로드 하고 싶지 않은 파일
- ex) 비밀번호, 키

