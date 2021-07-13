# [Context and expression syntax ](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions)

 ### 1. Expression 
   - Workflow 파일들 내에서 각종 변수들을 선언하거나 context에 접근하는 등의 프로그램 처리를 할 수 있습니다. 
   - Expression은 글자그대로의 값이거나, context를 참조하거나 또는 함수등의 어떠한 조합도 가능합니다. Operator들을 활용해 이러한 조합을 할 수 있습니다. 
   - Workflow 파일 내에서 Expression은 보통 조건의 `if`키워드와 함께 사용되어 step이 실행되어야 할 지를 결정합니다. `if`가 `true`일 때 실행됩니다. 
   - Expression으로 처리되기 위한 문법은 아래와 같습니다. 
    
     `${{ <expression> }}` 
 
   -  `if`조건내에서 expression을 사용할 때는, `${{ }}`를 생략할 수 있습니다. 그러나, expression이 operator를 포함한다면 `${{ }}`를 사용해야 합니다. 
   -  예
       
       ```
       steps:
        - uses: actions/hello-world-javascript-action@v1.1
          if: ${{ <expression> }}
       ```
       
   - [환경 변수를 설정하는 예](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#example-setting-an-environment-variable)
      
      ```
       env:
         MY_ENV_VAR: ${{ <expression> }}
       ```
       
### 2. Context
   - Context는 workflow 실행에 대한 정보, 러너 환경, job, step에 대한 정보에 접근하는 방법입니다. 
   - Context도 expression 문법을 사용합니다. 
     
     `${{ <context> }}`
     
      Context name| 	Type	| Description
      --|--|--
      github	| object	| workflow run에 대한 정보. [`github` context](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#github-context)참조.
      env	| object	| workflow, job, or step에 정의된 환경변수. [`env` context](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#env-context)참조.
      job	| object	| 현재 실행되는 job에 대한 정보. [`job` context](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#job-context)참조.
      steps	| object	| Job에서 실행된 step에 대한 정보. [`steps` context](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#steps-context) 참조.
      runner	| object	| 현재 job을 실행하는 러너에 대한 정보. [`runner` context](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#runner-context) 참조.
      secrets	| object	| secrets에 대한 접근을 활성화 함. ["Creating and using encrypted secrets."](https://docs.github.com/en/enterprise-server@3.1/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets) 참조
      strategy	| object	| 설정된 strategy parameters와 현재 job에 대한 정보에 접근을 활성화 함. Strategy parameters들 로는 `fail-fast`, `job-index`, `job-total`, `max-parallel`.
      matrix	| object	| 현재 job을 위해 설정한 matrix parameters에 대한 접근을 활성화 함. 예를 들어, `os` and `node` versions과 함께 설정한 matrix build가 있다면, `matrix` context 오브젝트는 현재 job의 `os`와 `node` versions들을 갖게 됨.
      needs	| object	| 현재 job의 의존성으로 정의된 모든 job들의 output들에 대한 접근을 활성화. [`needs` context](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#needs-context) 참조.

   - 아래 두가지 방법 중 하나로 이러한 context 정보에 접근할 수 있습니다. 
     - Index Syntax : `github['sha']`
     - Property dereference syntax: `github.sha`
   
   - Property deference syntax를 사용하기 위해, property name은 반드시 :
     - `a-Z`또는 `_` 로 시작해야 함
     - `a-Z` `0-9` `-` `_` 가 이어져야 함
   
   - 언제 Context를 사용할지 결정
     - GitHub Actions는 _contexts_ 라고 부르는 변수들과, _default environment variables_ 라고 부르는 변수들이 기본 포함되어 있습니다. 
     - 이러한 변수들은 workflow의 다른 지점들에서 사용되는 것을 목적으로 하고 있습니다. 
     - __Default Environment variables__ : 이 variable들은 job을 실행하는 러너에만 존재합니다. ["Default environment variables"](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environment-variables#default-environment-variables) 참조
     - __Contexts__ : 대부분의 context들은 워크플로우의 아무곳에서나 사용 가능합니다. 예를들어, context를 expression과 사용해 job이 실행될 러너로 전달되기 전에 초기 처리를 시작할 수 있습니다. 이것은, 조건의 `if` 키워드를 context와 함께 사용해 step의 수행 여부를 결정할 수 있도록 하는 것을 가능하게 해줍니다. Job이 한번 실행되면, 러너로 부터 `runner.os`와 같은 Context 변수들을 받아볼수 있습니다.(["Context availability"](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions#context-availability) 참조) 
     - 아래 예는, `if` statement가 `github.ref` context를 체크하여 현재 브랜치 이름을 확인합니다. 만약, 이름이 `refs/head/main`이면 이어지는 step들을 실행합니다. `if`확인은 GitHub Actions에 의해 처리되며, 그 결과가 `true`일 때만, job이 러너로 전송됩니다. Job이 러너로 일단 전달되면, step은 실행되고, 러너로부터 `$GITHUB_REF` 환경 변수를 참조합니다.

        ```
        name: CI
        on: push
        jobs:
          prod-check:
            if: ${{ github.ref == 'refs/heads/main' }}
            runs-on: ubuntu-latest
            steps:
              - run: echo "Deploying to production server on branch $GITHUB_REF"
        ```



