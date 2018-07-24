# 만들면서 배우는 Git GitHub 입문

## 저장소 사용에 필요한 Git 기본 명령어

```
git init 저장소생성
#현재 위치를 Git 저장소로 초기화 한다.

git add 파일이름
#해당 파일을 Git이 추적할 수 있게 저장소에 추가한다.

git commit
#변경된 파일을 저장소에 제출한다.

git commit -a
#변경된 저장소 파일 모두를 커밋한다.

git status
#현재 저장소의 상태를 출력한다.
```

## 저장소 사용을 위한 branch 명령어

```
git branch
#현재 어떤브랜치가 있는지 보여준다.

git branch 이름
#'이름'의 브랜치를 만든다.

git checkout 브랜치이름
#작업중인 브랜치를 '브랜치이름'으로 변경한다.

git checkout -b 브랜치이름
#'브랜치이름'의 브랜치를 만들면서 바로 checkout한다.

git merge 브랜치이름
#현재 브랜치에 '브랜치이름'의 브랜치를 끌어와서 병합한다.
```

**.gitignore **
불필요한 파일 및 폴더 무시하도록 작성해 두는 파일
[gitignore 생성기](https://www.gitignore.io/)

## conflict

```
print('Hello world')
print('tell yout world');
<<<<< HEAD                #충돌 발생 시작부분(현재 checkout한 브랜치)
print('Tell his world');
==========                #구분자
print('Tell her world');
>>>>> hotfix              #충돌 발생 끝 부분(merge할 브랜치)


git commit
#conflict 수정후 commit을 진행하면 된다.
```

## 기록보기

```
git log -p
#각 커밋에 적용된 실제 변경 내용을 보여준다.

git log --word-diff
#diff 명령의 실행 결과를 단어 단위로 보여준다.

git log --stat
#각 커밋에서 수정된 파일의 통계 정보를 보여준다.

git log --name-only
#커밋 정보 중에서 수정된 파일의 목록만 보여준다.

git log --relative-date
#정확한 시간을 부여 주는 것이 아니라 1일 전, 1주 전처럼 상대적인 시간을 비교하는 형식으로 보여준다.

git log --graph
#브랜치 분기와 병합 내역을 아스키 그래프로 보여준다.
```
