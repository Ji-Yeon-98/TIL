## 파일 삭제

</br>

1. Local 컴퓨터와 Github에서 모두 삭제

```
git rm [디렉토리명/파일명]
git commit -m "delete source"
git push

```

</br>

2. 로컬 디렉토리 유지하고 github만 삭제

```
git rm --cached -r [디렉토리명/파일명]
git commit -m "delete source"
git push
```


</br>
</br>

## Merge 협업

</br>

#### 1. Github에서 branch 생성
```
master or main : 최종 저장 branch
dev : 중간 저장 branch
[이름 지정] : 개인 branch
```

</br>


#### 2. Android studio (Terminal)
```

- git fetch : 원격 저장소 (Github)의 변경사항 Local 저장소에 인식
- git pull origin [branch] : 내용 불러오기
- git checkout : branch 확인
- 맨 왼쪽의 branch 변경 버튼

```

</br>

```

- 내용 수정
- commit
- push

```

</br>

#### 3. Github

```

- compare & pull request
- 원하는 브런치 선택 후 merge

```

</br>

- 수정한 내용이 겹치는 경우
```

- 웹페이지에서 수정 후 merge
- AndroidStudio -> Git -> Resolve 통해 수정

```

