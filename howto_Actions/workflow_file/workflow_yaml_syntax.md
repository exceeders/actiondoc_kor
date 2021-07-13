# [Workflow file YAML Syntax](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/introduction-to-github-actions#create-an-example-workflow)

```
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
      - run: npm install -g bats
      - run: bats -v
```


YAML syntax example | 설명
--|--
`name: learn-github-actions` | Optional - Actions 탭에 보여지는 워크 플로우 이름 
`on: [push]` | 워크 플로우 파일을 자동으로 트리거하는 이벤트. 예에서는 저장소로의 push 이벤트로서 저장소에 push가 발생할 때 마다 워크플로우가 트리거. 특정 브랜치, path, 또는 tag에 대해서만 트리거되도록 설정할 수 있음. see ["Workflow syntax for GitHub Actions."](https://docs.github.com/actions/reference/workflow-syntax-for-github-actions#onpushpull_requestpaths)
`jobs:` | 워크 플로우 파일내 모든 job들의 그룹 
`check-bats-version:` | job의 이름 
  `runs-on: ubuntu-latest` | job이 실행될 러너환경 (Ubuntu Linux runner). job은 GitHub에서 호스팅되는 새로운 최신 버젼의 우분투 VM에서 실행됨을 의미. 다른 러너를 지정하는 syntax는 ["Workflow syntax for GitHub Actions."](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjob_idruns-on)
  `steps:` | job의 스텝. 각 스텝들은 별도의 action 또는 shell command.
  | `- uses: actions/checkout@v2` | `uses` 키워드는 커뮤니티 action인 `actions/checkout@v2`를 사용하도록 설정. `action/checkout`의 Action은 저장소의 내용을 체크아웃하여 러너로 다운로드 하는 Action으로서, 이것을 통해 여러분이 선언하는 action들이 저장소의 코드에 대해 수행될 수 있도록 함. checkout Action은 저장소 코드에 대해 action을 수행하거나, 저장소에 선언된 action을 사용하려면 항상 먼저 선언되어야 합니다.   
  | `- uses: actions/setup-node@v1` | 이 action은 node 소프트웨어 패키지들을 러너에 설치하여 npm 명령어들을 사용할 수 있게 해줍니다. 
  | `- run: npm install -g bats` | `run` 키워드는 러너에서 바로 실행할 명령어를 말해줍니다. 예에서는, npm으로 bats라는 소프트웨어 테스트 패키지를 설치 
  | `- run: bats -v` | 마지막으로 bats command의 `v` 파라미터를 이용해 버젼확인
