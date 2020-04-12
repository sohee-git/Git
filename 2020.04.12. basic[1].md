# Git-basic[1]
### Git 저장소 만들기 
#### 1. 디렉토리에 프로젝트 파일 생성
```
$ ! pwd  : 현재 위치
$ cd documents : 현재 위치에서 C드라이브 documents로 이동 
$ mkdir [폴더이름] : 현재 위치에 '폴더이름' 생성 
$ cd [폴더이름] : 해당 폴더로 이동
$ ls -al : 해당 디렉토리 파일 목록
```
#### 2.  git init을 통한 버전관리 
버전관리 할 디렉토리를 GIT에게 알려준다.
```
$ git : 사용 할 수 있는 명령어 list 가 뜬다
```
start a working area 
- clone 
- init  : 현재 디렉토리에 작업을 진행하겠다 라는 것을 git에게 알려준다.
```
$ git init : .git 디렉토리에 git의 저장소를 초기화 했다.
$ ls -al : 해당 디렉토리의 파일 목록
```
명령어 $ ls -al을 실행 하였을 때 .git 디렉토리가 생긴 것을 확인한다. 여기서 .git 이라는 디렉토리는 버전 관리 시 여러가지 정보들이 생성 되는데, 그 생성된 정보들은 .git 디렉토리에 저장된다. 
### Git이 관리할 대상으로 파일 등록 
git은 기본적으로 새로운 파일을 관리하지 않는다. 파일을 관리 하려면, 관리 대상으로 등록 해야한다. 
#### 1. 파일 생성 
```
$ vim [f1.txt] : vim 프로그램으로 f1.txt 파일 생성 
```
1.  i 를 누르면 insert 모드로 변경 (입력모드)
2. esc 를 누르면 다시 입력 할 수 없는 상태가 됨 
3. 다시 r을 누르면 입력모드
4. :wq 저장,종료 
```
$  cat [f1.txt] : f1.txt 파일 확인 
```
#### 2. 파일을 버전관리
```
$ git status : 프로젝트 폴더 파일 상태 확인 
```
생성한 파일이 Untracted files (추적되고 있지 않은 파일)  이라고 뜸 . 즉 생성 파일은 버전 관리 되고있는 폴더 안에 존재하지만, 이 파일을 git에게 버전관리를 시작해 라고 명령하기 전까지 무시. 
```
$ git add f1.txt : git이 파일을 추적하도록 명령
$ git status 
```
f1.txt 파일은 새로운 파일이다라고 git이 인식하기 시작함. 

### 버전을 만드는 방법
버전이란, 어떠한 작업이 있을 경우, 그 작업이 완결된 상태를 말한다. 

처음 git을 사용할 때, 버전이 자신이 만든 것이라는 것을 나타내야 한다.
```
$ git config --global user.name [이름]
$ git config --global user.email [이메일]
```
현재 버전의 메세지를 작성한다. 
이 변화가 어떤 변화를 담고있는 지, 왜 변경 되었는지 그 이유를 적는 것이 버전 메세지다. commit 메세지 라고도 함.
```
$ git commit : vim 실행
```
i로 수정하고 :wq 후 종료. 
create mode f1.txt - 파일이 새로운 버전이 되었다는 뜻.
```
git log : 버전 역사 확인 
```
파일을 수정 할 경우 
```
$ vim f1.txt
$ git status : modified 확인 
$ git add f1.txt 
```
여기서 vim 이 아니라, add 명령으로 다시 버전관리 시스템에 add라고 설명해줘야한다. 즉, 추적 시 에도 add로, 추적하기 전 수정되었을 때에도 add를 포함 해야한다. 

### Stage Area
git은 commit 전에 add를 해야한다. 그 이유는 선택적으로 파일을 버전에 포함시키기 위해서이다. 
#### 1. 복습 
```
$ cp f1.txt f2.txt : f1 txt파일을 복사해서 f2.txt 파일로 만들기.
$ git status : untracked files 
$ git add f2.txt
$ git status : new file
$ git commit
$ git log : git 역사 확인 
```
#### 2.  여러개 파일 모두 수정하기
파일을 수정 한 후 선택적으로 커밋이 가능하다.
```
$ vim f1.txt
$ vim f2.txt 
$ cat f1.txt 
$ cat f2.txt : 현재 상태 확인 가능
$ git status : modified(빨간색)
$ git add f1.txt 
$ git status
changes to be committed :
modified:f1.txt(초록색) - 커밋이 된 경우 
changes not staged for commit :
modified:f2.txt(빨간색)
$ git commit : f1.txt은 새로운 버전에 포함되지만, f2.txt는 포함되지 않음.
$ git log : 4번째 로그 생성
$ git stauts : f2.txt만 커밋이 안된 상태로 남아있음. 
```
정리해보자면,
```
$ git add f1.txt  : f1.txt파일 commit 대기상태, f2.txt는 아님.
f1.txt는 stage에 올라가게됨.
$ git commit : commit 대기 상태 파일 만을 버전에 포함시킨다. stage 위에 있는 파일들.
```
여기서 git은 커밋 대기상태를 stage area 라고 한다.
stage 는 commit 대기 파일들이 가는 곳이고, repository는 commit 된 파일들이 저장되는 저장소를 말한다. 

####  git 이 왜 add 라는 과정을 포함하는가? 
많은 작업들을 담는 commit를 만들어야 할 경우, 이때 git은 add라는 과정을 통해 commit 하려는 파일만 commit 할 수 있게 해준다.

### 변경사항 확인하기 
#### 1. 버전 간의 차이점 
```
$ git log -p : 로그에서 출력되는 버전 간 차이점을 출력하고 싶을 때
```
```
$ git log : 각 commit이 나오고 고유한 ID(주소)를 확인 할 수 있다. 
$ git log [commit ID] :해당 commit ID 이전 commit 을 확인 할 수 있다.
$ git diff [commit ID1]..[comit ID2]: 버전 간의 차이점을 비교할 때 
```
#### 2. 파일 수정 후 차이 확인하기
```
$ git diff : git add 하기 전과 add 한 후 파일 내용을 비교 할 때
-f1.txt: 4  : 수정전 
+f1.txt:5  : 수정후
```
commit 을 하기 전, 자기가 작업한 내용이 문제가 있는 지 없는지 점검 할 수 있는 기회를 제공한다. 
