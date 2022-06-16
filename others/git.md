## git이 뭐고, 왜 쓰는 건데? 🧐

git은 간단히 말해 코드의 버전을 관리하는 툴이다.
> 🥲 이 글에서는 기초는 간단히 다룰 예정이니 GitHub에 대해 모른다면 다른 친절한 글들들을 잘 읽어보자

<br>

## 코드가 있는 곳 🏢

git의 동작은 코드가 있는 곳을 보며 이해하면 쉽다.
코드는 사용자 로컬 환경과 git의 서버에 존재할 수 있으며, git 명령어를 통해 각 위치로 옮길 수 있다.

다음 그림을 보며 이해해 보자.

![](https://aprilamb.com/wp-content/uploads/2022/03/git_alone.png)

### 사용자 Local 환경

사용자 로컬 환경은 Working Directory, Staging Area, Local Git Repository 이 세 가지의 환경으로 또 나뉜다.


#### (1) Working Directory

Working Directory는 말 그대로 작업 환경이다. 우리가 코드를 짜는 곳이 바로 여기이다. 여기서 작업을 하면 `version 기록이 남지 않는다`.

#### (2) Staging Area

Staging Area에서도 역시 version 기록이 남지 않는다. 그냥 중간중간 저장해두는 것 정도로 생각하면 된다.

#### (3) Local Repository

Local Repository는 local 환경에서 `version을 기록한다`.
version을 기록하며 짧막한 코멘트를 남길 수 있으며, version이 기록되어 있어 Working Directory에서 삐끗하면 이곳에서 예전 버전으로 돌아가는 작업을 할 수 있다.

### Git 서버
#### (1) Remote Git Repository

git 서버는 사용자의 local 환경에서 아예 분리되어 있다. GitHub의 server단에 내 코드를 올려 놓고 version을 관리한다. 꼭 내 노트북이 아니더라도 다른 사람의 노트북에서도 내 코드를 다운 받아 작업할 수 있고, 여러 명이 각자의 local 환경에서 작업하고 코드를 하나로 합칠수도 있다.

<br>

## 그래서 그 위치로 어떻게 옮기는데요? 🎢
위에서 잠깐 언급했듯이 git이 정해놓은 명령어를 그냥 써주면 된다.
다음 그림이 모든 것을 말해주고 있으므로 자세한 설명은 생략하겠다.

![](https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/3K6t/image/_630fSrZQJj7XdswACSoCGDI1vE.png)

<br>

## 기초는 이 정도로 하고 🌝
이 정도면 git의 모든 것을 **간파**해버렸다.
이제 이를 응용해서, 다른 사람들과 협업할 수 있다.
~~몰랐겠지만 이 글의 주제는 git으로 협업하기이다...~~

### 협업을 왜 git으로 해요?
문득 이런 의문이 들수도 있다. 답은 단순하다. 개발은 혼자하는 것이 아니기 때문이다. 혼자하는 사람은 아주 불쌍한 사람이다. (← 작년의 나)
취업을 하든, 학교에서 팀 프로젝트를 하든, 모든 게 **팀**이다. 부분부분을 나눠서 개발하기 때문에 이 코드들을 합치는 과정이 필요하다.
> 👨‍👧‍👦 내가 회원가입 기능을 개발하고, 쟤는 로그인 기능을 개발하고, 걔는 게시글 기능을 개발하고, 그분은 채팅 기능을 개발해 옵시다!!!

### 알겠어요 그래서 어떻게 하는 건데
여기서부터 좀 복잡해진다. git으로 협업을 하기 위한 기능은 바로 `branch`이다. branch는 한국어로 '나뭇가지'를 뜻한다. 그리고 진짜 나뭇가지같다.

<br>

## Branch 이해하기 🪵
당신은 노트북에서 코드를 짜고, 변경 사항에 맞추어 다음과 같이 세 번의 commit을 했다. 이 그림에서 branch가 무엇일까? 바로 저 세 커밋이 올라가 있는 판이다. 즉, 작업을 하고 있는 작업 공간인 셈이다.
![](https://velog.velcdn.com/images/gimhanul/post/df81e444-1f5e-4c32-9f1c-760bcca7e567/image.png)

지금부터 편의를 위해 branch를 색깔로 이름지어 부르겠다. 다음 그림은 연두 branch의 commit2에서 새로운 branch인 보라 branch를 만든 모습이다.
branch를 딸 때, 그 커밋 버전의 코드에서부터 작업한다.

![](https://velog.velcdn.com/images/gimhanul/post/6f072794-bd12-4f44-bef3-65abdc13c4e6/image.png)

<br>

### branch는 다른 branch와 격리되어 있다

같은 사람이 연두 branch의 commit2에서부터 어떤 작업을 해서 commit3을 commit해도 작업한 내용은 branch별로 다르므로 연두 branch에서 작업한 내용과 보라 `branch에서 작업한 내용은 서로 영향을 주지 않는다`.

따라서 내가 연두 branch에서 "A"라는 기능을 개발하다가, 작업하는 branch를 보라 branch로 바꿔서 "B"라는 기능을 개발할 수 있는 것이다. 이때 연두 branch에서 작업한 내용은 보라 branch에는 없으며, 보라 branch에서 작업한 내용도 마찬가지로 연두 branch에 없다.

### branch를 따는 이유

이게 협업에 왜 유용한지 의문이 들지도 모른다. 
그렇다면 가정해보자. 만약 연두 branch에서 5명이 각자의 작업을 하고 있다.
사람1, 사람2는 commit1일 때 repository를 clone해와서 작업하기 시작했고, 사람3은 commit2일 때, 사람4는 commit3일 때, 사람5는 commit4일 때 작업하기 시작했다. 그리고 각자의 작업내용을 local repository에 commit했다.
물론 이때까지는 아무 문제 없을 것이다. 하지만 이를 remote repository에 push를 하는 순간 **confilict(충돌)**가 날 것이다.
> 🙋🏻 물론 branch를 이용해도 conflict가 나긴 한다.

이러한 상황을 방지하기 위해 여러 명이 협업할 때 branch를 사용한다.
그렇다면 branch를 따로 따오는 이유는 _**각자 작업하고, 다시 합치기 위함**_ 이라고 할 수 있겠다.


### branch를 합쳐보자

그렇다면 branch는 어떻게 합칠까? 바로 `merge(병합)` 기능을 사용해서 합칠 수 있다. merge는 branch와 branch 간에 일어날 수 있다.

local 환경에서는 명령어를 써서 merge를 할 수 있다.
> 😊 가끔 다른 사람이 작업한 내용을 내 branch에서도 사용해야 할 때 사용한다.

하지만 보통 merge는 remote repository에서 많이 한다. 현재 커밋내역이 다음과 같다고 생각해보자. 보라 branch에서 기능A 개발이 끝나고 이제 이 작업 내역을 합쳐야 한다.

![](https://velog.velcdn.com/images/gimhanul/post/d4ff6224-3449-4942-b72d-a2db6d151baa/image.png)

rmoete repository에서 merge를 하는 방법은 바로 _**Pull Request**_(이하 PR)을 보내는 것이다. PR은 각 repository의 Pull Request tab에서 보낼 수 있다. PR을 보내게 되면, git이 자동으로 각 branch를 비교하여 merge가 가능한지 확인하고, merge를 시켜준다.

merge는 merge 받는 branch의 마지막 commit에 된다.
![](https://velog.velcdn.com/images/gimhanul/post/8bbcb190-b40e-44cd-8fab-e806e0624b6a/image.png)

이런 식으로 branch를 사용해 자동으로, 그리고 쉽게 작업한 내용을 합칠 수 있다.

<br>

## Branch 활용하기 - Git Flow 🌊

이러한 branch의 특성을 이용한 게 바로 한 번 쯤은 들어봤을 **Git Flow 전략**이다.
효율적인 협업을 위한 전략으로, branch를 따고 머지하며 개발한다.
> 📄 [이 글](https://techblog.woowahan.com/2553/)이 아주 설명이 잘 되어 있고 좋다.

### 항상 가지고 있는 branch

다음 branch는 항상 가지고 있으며, 이 branch들에는 직접 commit 하지 않는 것이 좋다.

- main: 현재 배포되어 있는 branch
- develop: 개발 중인 내용을 merge하는 branch

### 일시적인 branch

다음 branch는 필요할 때 새롭게 생성해 쓴다.

- feature: 새로운 기능을 개발하는 branch
	→ develop branch에서 따온다.
- release: 배포 전 준비하는 branch
	→ develop branch에서 따온다.
- hotfix: release branch에서 난 bug를 고치는 branch
	→ release branch에서 따온다.
    
### git-flow를 따르며 개발해보자

"A"라는 기능을 배포해야 한다고 가정하자.
다음과 같은 순서를 따른다.

1. develop branch에서 feature branch를 따온다.
2. feature branch에서 작업한다.
3. 개발 완료 후 develop branch에 PR을 날려 merge한다.
4. release를 하기로 했으면, release branch를 딴다.
5. release branch에서 QA를 진행한다.
6. bug가 났다면 release branch에서 hotfix branch를 따와서 fix한다.
7. QA가 끝난 뒤 release branch를 main, develop에 각각 merge한다.

![](https://techblog.woowahan.com/wp-content/uploads/img/2017-10-30/git-flow_overall_graph.png)

> 🍞 하지만 요새는 CICD를 많이 구축하기 때문에 Release branch에 대해서는 고민이 필요하다.

<br>

## 그럼 난 이제 협업 마스터? 😳

### 가 아닙니다~

gitHub의 branch를 이해하고, 이를 활용해 git-flow를 사용할 수 있으면 효율적으로 협업할 수 있다. 그러나 이보다 더 나은 협업을 할 수 있도록 돕는 gitHub의 기능도 있다. 이제부턴 짜잘한 협업 꿀팁들을 얘기하겠다.

<br>

### 1. commit message를 자세히 남기자 📄

commit을 할 때 message로 무엇을 남기는지 생각해보자. 강력하게 말하는데, **commit message는 자세하게 남겨야 한다**.

나와 협업하는 사람들은 내 코드를 읽는다. 그리고 나중에 내가 내 코드를 돌려 읽는 경우도 허다하다. 그래서 내가 무슨 작업을 했는지 분명히 남겨 놓는 것이 좋다.

#### 나는 이렇게 한다 - commit message의 구조
```
TYPE :: title (#issue-number)

body
```

TYPE에는 내가 한 작업의 유형을 남기고, title에는 한 작업을 간단히 요약해서 적는다.
issue number는 곧 나올 issue에 자동으로 부여된 번호를 적는다.

또한 body에는 내가 한 작업을 구체적으로 적는다.

<br>

### 2. gitignore을 사용하자 🫥

`.gitignore` 파일을 사용하면 remote repository에 작업 내용을 push할 때 쓸모없는 파일을 제외하고 올릴 수 있다. remote repository에 필요 없는 파일이나 폴더가 올라가 있다면, repository를 보고 코드를 읽어야 하는 사람이 이건 뭐야? 싶을 것이다. 필요 없는 파일의 예는 macOS에서 자동으로 생기는 .DS_Store, IDE를 사용하면 맘대로 생기는 .idea, .metadata 같은 것이 있다.

<br>

### 3. Issue를 발행하자 🦷

issue는 만들 기능을 작성하거나, 질문을 하거나, 버그를 report하는 등의 다양한 용도로 자유롭게 사용할 수 있다. issue를 해결했으면 close 해서 해결했음을 나타내야 한다.
내용은 markdown 문법을 사용해 작성할 수 있으며, issue를 쓰고 나면 자동으로 번호가 부여되어 commit message와 PR에 연결할 수 있다.

> 단순히 `#<issue number>` 형태로 쓰면 연결이 되어 이슈 번호를 눌러 해당 이슈로 이동할 수 있게 된다.

<br>

### 4. Issue, PR의 사이드바를 꽊 채우자 🤲

PR과 issue의 오른쪽 사이드를 보면 다음과 같은 칸이 있다. 이런 기능을 적극 활용하자.

![](https://velog.velcdn.com/images/gimhanul/post/8639d6d9-d887-4297-9d08-bc21423753c6/image.png)

- Assignees: 담당자를 지정할 수 있다.
- Labels: 해당 PR, issue의 type, 우선순위 등을 지정한다.
  > 🏓 custom 하여 사용할 수 있다. 필요한 label을 만들어 쓰면 훨씬 관리하기 편해진다.
- Projects: project를 지정할 수 있다. (이는 추후에 설명하겠다)
- Milestone: milestone을 지정할 수 있다. (간단히 설명하자면 특정 기간 동안 해결할 issue를 정해놓고, 현재 진행사항을 보여준다)
- Development: PR과 issue를 서로 연결할 수 있다.


<br>

### 5. PR과 Issue template을 정하자 🫶

원래 PR과 issue는 자유 형식으로 작성한다. 하지만 PR template과 Issue template 기능으로 template을 지정할 수 있다. 이러한 template들을 정해놓고, 정해진 내용의 글(새로운 기능 추가, 버그 발생, 질문이 있어요 등)을 올릴 때는 정해진 형식에 맞추어 올리게 설정해 놓으면 협업할 때 아주 유용하다.

<br>

### 6. Issue를 자동으로 닫자 🤸

PR을 날리고 일일이 issue를 연결하고, 닫는 것은 여간 쉬운 일이 아니지만 현재 프로젝트의 진척도를 알기 위해 issue를 관리하는 것은 중요하다. gitHub는 귀찮은 사람들을 위해 issue를 쉽게 관리하게 해준다.

위의 PR, Issue의 사이드바의 Development에 서로를 연결할 수 있다고 했다. 얘네를 서로 연결하면, PR을 merge할 때 issue가 자동으로 닫힌다. 이를 사이드바에서도 설정할 수 있지만 PR에 글을 남기며 특정 키워드를 통해 설정 가능하다.

> 💡 close, closes, closed, fix, fixes, fixed, resolve, resolves, resolved 뒤에 #issue-number 를 남기면 된다.

<br>

### 7. 서로 Code를 Review 하자 ✍️

가장 중요하다. 중! 요! 중! 요! 서로의 코드를 리뷰하며 서로 성장한다. 남의 코드를 리뷰하며 아이디어를 얻고, product를 더 나은 방향으로 이끌어갈 수 있으며 내 코드를 개선시킬 수 있다. 코드 리뷰는 무엇보다 받아들이는 자세가 중요하다. ~~기분 나빠하면 안 돼요~~

사실 PR의 사이드바는 위에 제시한 그 사이드바가 아니다. 위에 Reviewer 필드가 하나 더 있다. 이 Reviewer 필드에 리뷰할 사람을 할당해서 리뷰해달라고 요청할 수 있다.

code review는 PR에서 진행한다.
그러니까, PR을 보내고 → 코드 리뷰를 받고 → 머지하면 된다.


#### review를 하는 사람은

PR에서 File Changed 탭에 들어가면, 그 PR에서 변경된 코드를 모두 볼 수 있다. 리뷰를 해야 하는 사람은 이 탭에서 코드를 찬찬히 읽으며 더 나은 코드를 제안하면 된다.

이제부터 자세한 방법을 소개한다. 먼저 제안할 사항이 있는 코드에 + 버튼을 누르고, 코멘트를 남기면 된다.

![](https://velog.velcdn.com/images/gimhanul/post/0026796a-a792-45e5-8a42-59b719826280/image.png)

이렇게 shift를 누르고 코드를 잡아서 여러 줄에 대해 리뷰할수도 있다.

![](https://velog.velcdn.com/images/gimhanul/post/eb30f79e-fb88-41d4-a2e1-d01ae787aa37/image.png)

모든 코드에 리뷰를 마치고, 오른쪽 위에 submit review를 눌러 review를 마무리 할 수 있다.
![](https://velog.velcdn.com/images/gimhanul/post/6ff93f85-6fd3-4428-97af-b94d3884a18b/image.png)

밑에 comment, approve, request changes는 review type을 지정한다.

- Comment: 단순 comment
- Approve: merge 해도 된다. ok.
- Request changes: 이 부분은 변경해주세요~

그래서 Approve를 받아야 머지를 할 수 있도록 하자고 팀원들과 규칙을 만들어 놓는 게 좋다.
또한, review는 한 번만 하고 끝나는 게 아니라, 코드가 괜찮다고 느껴질 때까지 계속 하는 것이다.

#### review를 받는 사람은

다른 사람이 제안 사항을 달아서 보내면 PR에 이런 식으로 나온다.

![](https://velog.velcdn.com/images/gimhanul/post/c47eee6f-0121-4b73-a1bf-d794b7126288/image.png)

이 제안 사항에 동의한다면 해당 사항을 반영하여 코드를 수정하고, 아니라면 댓글로 의견을 제시하면 된다. 무엇을 하였든 이 문제를 해결했다면, resolve conversation을 눌러 해결됐다는 표시를 하고, 또 코드를 수정했기 때문에 다음 버튼을 눌러 다시 review를 해달라고 요청하면 된다.

![](https://velog.velcdn.com/images/gimhanul/post/2464a6a8-2ea2-4f06-a871-6df0a6297651/image.png)

위 과정을 **Approve를 받을 때까지 반복**하면 된다.

> 😺 코드 리뷰 문화는 여러 기업의 tech blog를 살펴보면 많은 도움이 된다.


<br>

### 8. CODEOWNERS 지정해서 편한 삶을 살자 👶

Reviewer를 PR마다 지정해주는 것은 아주 골치아픈 일이다. 그래서 CODEOWNERS 파일을 작성해 자동으로 넣어줄 수 있다. 한 번만 설정해 놓으면, PR을 보낼 때마다 자동으로 Review Request를 보내준다.

<br>

### 9. 협업이니까 Organization을 사용하자 👨‍👧‍👦

팀 프로젝트를 할 때, web을 예로 들었을 때 frontend를 개발하는 팀원 계정에 front repository, backend를 개발하는 팀원 계정에 backend repository가 있고, 각각 따로따로 있으면 한 눈에 보기 힘들 것이다. 그리고 backend에도 한 명만 있는 것이 아니라 여러 명이 있기 때문에 개인 계정에 repository를 파게 되면, 그 한 명에게 의존하게 된다. 따라서 팀 프로젝트에는 `Organization (단체 계정)`을 이용하는 게 좋다.

<br>

### 10. Project로 관리하자 🗓

Project는 현재 작업하고 있는 이슈, PR의 진행사항을 칸반보드로 보여준다.
이를 이슈 기반으로 자동으로 관리해 주기 때문에, 아주 편리하다. 하지만 정해진 것은 없기 때문에 custom하여 사용할 수 있다.

<br>

## 나애. 협업-Flow 👨‍👦👨‍👧‍👦👩‍👦👨‍👧‍👧
결론! 나는 이렇게 협업한다.

1. 해야 할 일을 issue로 발행한다.
2. 할 일을 정하고, Project에서 해당 issue를 `In Progress 🚀`로 옮긴다.
3. 관련된 branch를 따온다.
4. 작업한다.
5. PR을 보낸다.
6. code review를 받는다.
7. approve를 받으면, merge한다.
8. 1~7 반복

<br>

## 이쯤에서 🤨

내가 아는 것은 여기까지이다. 내가 gitHub로 협업하는 방법에 대해 쓸 만큼 많이 협업해 본 것은 아니다. 하지만, 이런 경험, 지식들이 남들에게 도움이 되었으면 좋겠다. (또 다른 좋은 협업 방법, 기능에 대해 댓글로 남겨주세요 → 알고 싶다!!)

그리고 마지막으로 남기고 싶은 말은 **"좋은 PR에 대한 고민하자"** 이다. 이걸 11번째 꿀팁으로 넣을지 고민하다가 결국 안 넣고 마지막에 덧붙이게 되었다. 왜냐하면, 나도 잘 모르기 때문이다. 많은 tech blog를 읽었고, 좋은 PR에 대해 많은 의견을 보았다. 이건 사실이 아닌 의견이기에 직접 찾아보는 게 좋을 것 같다.

### 찐막

**모르겠는 거, 궁금한 건 검색하자!!** 감사합니다.