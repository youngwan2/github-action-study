# 레포지토리 목적
- 깃허브 액션를 다양한 방식을 기반으로 활용해보는 용도
- 모르더라도 일단 간단한 것 부터 하나씩 적용해보며 이해도 높이기
- 이론만 머리에 가득해 봤자 조금만 지나면 다 까먹으니 연습장 처럼 활용하는 용도


# 학습 데이터

### 1 ) vite + react 를 깃허브 액션으로 build 해보기
```yaml

# 워크플로의 이름을 지정한다(즉, 문서 이름과 같다).
name: Build Action

# on 는 깃허브 액션이 동작하는 특정 이벤트를 등록하는 명령이다.
# 아래에서는 push 라는 키워드가 입력될 때 깃허브 액션이 동작하도록 되어 있다.
# branches 는 push 가 이루어질 때 어느 브랜치의 변경이 발생할 때 jobs 를 실행할 것인지 지정한다.
# ㄴ 여기서는 main 브랜치의 코드에 변경이 발생하면 워크플로가 이루어진다.
# ㄴ 즉, main 이 아니라 update/scroll-trigger 라는 다른 이름의 브랜치에서 변경이 발생한다면
# ㄴ 워크플로는 이루어지지 않는다.
on:
    push:
        branches: 
            - main

# jobs 는 말그대로 작업들을 의미한다. 실질적인 워크플로의 동작을 모아두는 컨테이너 역할을 한다.

jobs:
    build:
        runs-on: ubuntu-latest

        steps:

            # uses 는 현재 워크 플로우에서 사용할 Actions 을 지정하는 특수한 명령어 이다.
            # actions/checkout@v4 은 현재 워크플로우에서 저장소(레포지토리)에 접근하여 
            # ㄴ 체크아웃하는 동작을 수행해주는 actions 를 의미한다.
            - uses: actions/checkout@v4 

            # name 은 각 워크 플로우 단계를 구분하는 이름으로 사용된다.
            # with 는 actions 를 적용할 때 지정할 옵션을 의미한다. 
            # ㄴ 여기서는 node 설치 버전으로  현재 프로젝트에서 사용되는 Node.JS 버전을 구체적으로 명시
            - name: Set up NodeJS 
              uses: actions/setup-node@v4  
              with:
                node-version: 20.11.0              
        
           # 현재 package.json, package.lock.json 에 설정된 종속성을 설치     
           # run 은 해당 단계에서 실행할 명령어를 지정한다. 
            - name: Install Dependencies  
              run : npm install
            
           # npm run build 로 배포 파일을 생성한다.   
            - name: Build
              run: npm run build```
```


### 2 ) ... 계속 추가 예정