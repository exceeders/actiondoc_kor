# [Workflow Commands](https://docs.github.com/en/enterprise-server@3.1/actions/reference/workflow-commands-for-github-actions)

### 1. 설명
   - Actions는 러너와 통신하여 환경변수를 설정하거나, 다른 Actions들에서 사용할 output value, 또는 디버그를 위해 output log에 디버그 메세지를 포함하는 등 다양한 task들을 수행할 수 있습니다. 
    
<br/>


### 2. Toolkit functions에 접근하기 위한 workflow command
    
   - [actions/toolkit](https://github.com/actions/toolkit)은 workflow 커맨드로서 실행할 수 있는 다양한 function들을 포함합니다. 
   - `::` syntax를 사용해 이러한 workflow 커맨드를 실행할 수 있고, 이러한 명령어들은 `stdout` 으로 러너에 전달됩니다. 
   - 예를들어, output을 설정하는데 코드 (`core.setOutput('SELECTED_COLOR', 'green');`) 를 사용하는 대신, workflow에 아래와 같이 `set-output`을 이용해 동일한 값을 설정할 수 있습니다. 
   
   ```
      - name: Set selected color
        run: echo '::set-output name=SELECTED_COLOR::green'
        id: random-color-generator
      - name: Get color
        run: echo "The selected color is ${{ steps.random-color-generator.outputs.SELECTED_COLOR }}"
   ```
   
   - 아래 표는 toolkit function들이 workflow에 가능한 커맨드를 보여줍니다. 
   
      Toolkit function	| Equivalent workflow command
      --|--
      `core.addPath`	| Accessible using environment file `GITHUB_PATH`
      `core.debug`	| `debug`
      `core.error`	| `error`
      `core.endGroup`	| `endgroup`
      `core.exportVariable`	| Accessible using environment file `GITHUB_ENV`
      `core.getInput`	| Accessible using environment variable `INPUT_{NAME}`
      `core.getState`	| Accessible using environment variable `STATE_{NAME}`
      `core.isDebug`	| Accessible using environment variable `RUNNER_DEBUG`
      `core.saveState`	| `save-state`
      `core.setFailed`	| Used as a shortcut for `::error` and `exit 1`
      `core.setOutput`	| `set-output`
      `core.setSecret`	| `add-mask`
      `core.startGroup`	| `group`
      `core.warning`	| `warning file`

<br/>


### 3. Output 파라미터 설정하기
    
  - `::set-output name={name}::{value}`
  - Action의 output 파라미터 설정
  - 부가적으로, `action.yml`, `action.yaml`의 [메타데이터 파일을 통해 output 파라미터를 설정](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/metadata-syntax-for-github-actions#outputs)할 수도 있습니다. 
  - 예
  
     ```
      echo "::set-output name=action_fruit::strawberry"
     ```
  
  
<br/>


### 4. 디버그 메세지 설정하기
    
  - `::debug::{message}`
  - log에 디버그 메세지 출력. 
  - 반드시 저장소에 `ACTIONS_STEP_DEBUG` 라는 이름을 가진 secret을 생성해야 하고, 값은 `true` 로 설정해야 합니다. ([설명](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/enabling-debug-logging))
  - 예

     ```
     echo "::debug::Set the Octocat variable"
     ```

<br/>


### 5. 경고 메세지 설정하기
    
  - `::warning file={name},line={line},col={col}::{message}`
  - 경고 메세지를 생성하고 log에 출력. 
  - 옵션으로 에러가 발생한 filename, line number, column number 

     ```
     echo "::warning file=app.js,line=1,col=5::Missing semicolon"
     ```

<br/>


### 6. 에레 메세지 설정하기
   
  - `::error file={name},line={line},col={col}::{message}`
  - 에러 메세지를 생성하고 log에 출력. 
  - 옵션으로 에러가 발생한 filename, line number, column number 

     ```
     echo "::error file=app.js,line=10,col=15::Something went wrong"
     ``` 

    
<br/>


### 7. 로그 라인들 그룹핑하기

  ```
  ::group::{title}
  ::endgroup::
  ``` 
    
  - log에 확장가능한 그룹 생성. 
  - `group` 커맨드를 사용하고, `title`을 지정
  - `group` 과 `endgroup` 커맨드 사이에 출력된 내용은 로그에서 확장 가능한 엔트리로 표현됨
  
     ```
     echo "::group::My title"
     echo "Inside group"
     echo "::endgroup::
     ```
   <img src="https://user-images.githubusercontent.com/40287191/123775887-bcc6a480-d909-11eb-825b-aee9ac4fc3c2.png" width="400" height="150">

  
<br/>


### 8. 로그의 value값 마스킹

  - `::add-mask::{value}`
  - 어떤 값을 masking하여 string이나 변수가 로그에 출력되는 것을 방지.
  - 각각의 masking된 값들은 공백으로 분리되고, `*` 표시로 대치됩니다. 
  - masking의 `value`로 환경변수나 string을 사용할 수 있습니다.
  - 예 : 로그에서 `"Mona The Octocat"` 대신 `"***"`
  
     ```
     echo "::add-mask::Mona The Octocat"
     ```  
  
  - 예: 환경 변수의 masking : `MY_NAME` 이라는 환경 변수를 정의하고 이것을 masking
  
     ```
     MY_NAME="Mona The Octocat"
     echo "::add-mask::$MY_NAME"
     ```

<br/>


### 9. Workflow command 멈추기와 시작하기

  - `::stop-commands::{endtoken}`
  - workflow 커맨드의 처리를 중단.
  - workflow 커맨드를 실수로 실행하지 않고 log, 예를들어, logging을 중단할 수 있습니다. 
 
  - 예 : 로그에서 `"Mona The Octocat"` 대신 `"***"`
  
     ```
     echo "::stop-commands::pause-logging"
     ```  
  
  - 다시 workflow 커맨드를 시작하려면, workflow 커맨드를 멈출 때 사용했던 token을 전달
  `::{endtoken}::`
  
     ```
     echo "::pause-logging::"
     ```
  
<br/>

### 10. Actions 실행 전과 후에 값 보내기

   - `save-state` 커맨드를 이용해 워크플로우의 `pre:` 또는 `post:` action을 공유하기 위한 환경 변수들을 생성할 수 있습니다. 
   - 예를들어, `pre:` action을 통해 파일을 만들고, 파일의 위치를 `main:` action으로 보내고, `post:` action을 이용해 파일을 삭제할 수 있습니다. 또는 `main:` action으로 파일을 생성하고, 파일 위치를 `post:` action으로 보내고, `post:` action을 이용해 파일을 삭제할 수 있습니다.
   - 만약 여러개의 `pre:` 또는 `post:` action들이 존재한다면, `save-state` 가 사용된 action에 저장된 값만 접근할 수 있습니다. 
   - 더 자세한 정보는 ["Metadata Syntax for GitHub Actions"](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/metadata-syntax-for-github-actions#post)에 설명되어 있습니다. 
   - `save-state` 커맨드는 action내에서만 사용가능하고, YAML 파일에서는 사용가능하지 않습니다. 저장된 값은 `STATE_` prefix가 붙은 환경값으로 저장됩니다. 
   - 아래 예는 JavaScript로 `save-state` 커맨드를 실행한 예제입니다. 결과로 저장되는 환경변수는 `STATE_processID`라는 이름으로 값은 `12345`가 저장됩니다. 
   
      ```
      console.log('::save-state name=processID::12345')
      ```
   
   - `STATE_processID` 변수는 `main` action하에서 실행되는 cleanup 스크립트에만 독점적으로 사용가능합니다. 아래 예는 `main`에서 실행되고, JavaScript를 사용하여 `STATE_processID` 환경변수에 할당된 값을 표시해 줍니다. 
   
      ```
      console.log("The running PID from the main action is: " +  process.env.STATE_processID);
      ```
    
<br/>

### 11. Environment Files

   - 워크플로우의 실행동안, 러너는 특정 actions들을 실행하는데 사용될 수 있는 임시 파일들을 생성합니다. 
   - 이 파일들의 경로는 환경 변수들로 노출됩니다. 
   - 이 파일들에 쓰기를 하기 위해서는 UTF-8 인코딩이 필요하며, 이는 커맨드의 적절한 처리를 할 수 있게 해줍니다. 
   - New line으로 분리하면서 여러개의 커맨드들을 같은 파일에 쓸 수 있습니다. 
   - `Warning` : Powershell은 기본으로 UTF-8을 사용하지 않습니다. 따라서, 경로를 설정할 때 UTF-8 인코딩을 설정해 주어야 합니다. 

       ```
       steps:
         - run: echo "mypath" | Out-File -FilePath $env:GITHUB_PATH -Encoding utf8 -Append
       ```
    
<br/>

### 12. Enviroment variable 설정

   - `echo "{name}={value}" >> $GITHUB_ENV` 
   - Job에서 다음번에 실행될 Actions를 위한 환경변수 생성 또는 수정
   - 환경 변수를 생성하거나 업데이트 하는 Action 자체는 새로운 값을 사용할 수 없지만, Job내에 모든 이어지는 Actions들은 사용가능
   - 환경 변수는 대소문자 구별하고, 구두점(punctutation)을 포함할 수 있다. 
   - 예:
   
      ```
      steps:
       - name: Set the value
         id: step_one
         run: |
           echo "action_state=yellow" >> $GITHUB_ENV
       - name: Use the value
         id: step_two
         run: |
           echo "${{ env.action_state }}" # This will output 'yellow'
       ```
    
<br/>

### 13. 시스템 Path 추가

   - 시스템 `PATH` variable에 디렉토리를 붙이고, 이것을 현재 job의 모든 이어지는 Actions들에서 사용할 수 있게 해 줌. 
   - 현재 실행되고 있는 Action은 업데이드된 path 변수를 사용할 수 없음.
   - 현재 job에 정의된 paths를 보려면 : `echo "$PATH"`을 step이나 Action에서 사용
   - 예 : 사용자의 `$HOME/.lobal/bin` 디렉토리를 `PATH` 에 추가
    
       ```
        echo "$HOME/.local/bin" >> $GITHUB_PATH
        ```
