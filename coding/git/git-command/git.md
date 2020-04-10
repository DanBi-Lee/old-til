# 자주 쓰는 git 명령어

### 커밋하지 않은 변경사항을 다른 브랜치에 커밋하기

```text
$ git stash // 커밋하지 않은 변경사항 저장
$ git stash pop // 저장한 변경사항을 복원
```

### git 저장소 병

**1. 사용중 브랜치로 이동**

```text
$ git checkout <사용브랜치>
```

**2. 병합하기**

```text
$ git merge <병합할 브랜치>
```

