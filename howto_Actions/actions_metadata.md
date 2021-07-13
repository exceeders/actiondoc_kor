# [Metadata syntax](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/metadata-syntax-for-github-actions)

1. 메타 데이터 파일은 `action.yml` 또는 `action.yaml` 이라는 파일 이름을 가져야 합니다. 

2. 메타 데이터 파일은 input, output, main entrypoint를 설정하는데 사용됩니다. 

3. 키워드 설명

   키워드 | 설명
   --|--
   name | **Required** action의 이름. Actions 탭에 이름을 표시하여 각 job에서 action들을 가시적으로 표시해줌 
   author | **Optional** author의 이름.
   description | **Required** action에 대한 짧은 설명.
   inputs | **Optional** Input 파라미터는 런타임 동안 action이 사용할 데이터를 정의. Input 파라미터는 environment variables로 저장됨. Input ID는 소문자로 사용이 권고(대문자인 Input ID는 런타임동안 소문자로 변환됨) <br><br> Example: <br> - 이 예는 두 개의 input `numoctocats`와 `octocatEyeColor`를 정의. <br> - `numoctocats`은 항상 요구되지 않으며 기본값으로 '1'을 설정. <br> - `octocatEyeColor`는 항상 요구되며 기본값이 없음. <br> - 워크 플로우는 `with` 키워드를 사용해 `octocatEyeColor`의 input value를 지정해야 함. <br> <pre> inputs:<br>   numOctocats:<br>    description: 'Number of Octocats'<br>    required: false<br>    default: '1'<br>   octocatEyeColor:<br>    description: 'Eye color of the Octocats'<br>    required: true</pre> - 워크플로우 파일내에 input 값을 지정하거나, default value를 지정할 때, GitHub은 `INPUT_<VARIABLE_NAME>` 이라는 이름의 environment variable을 생성.<br> - composite으로 생성된 action은 자동으로 `INPUT_<VARIABLE_NAME>`을 자동으로 생성하지 않으며 수동으로 생성해야 함.<br> - Docker 컨테이너 action에서 이 environment variable에 접근하기 위해서는 메타데이터 파일에서 `arg`키워드를 사용해 input 값을 넘겨 줘야 함. 예를 들어, 워크플로우가 `numoctocats`와 `octocatEyeColor`의 input을 정의한다면, action은 이 값들을 각각 input의 값을 `INPUT_NUMOCTOCATS` 과 `INPUT_OCTOCATEYECOLOR` environment variables로 읽어들임.
   outputs | **Optional** Output 파라미터는 actions이 설정하는 데이터를 선언. 워크플로우내에 이후에 실행되는 Actions는 이전 실행되었던 actions들로 부터의 output 데이터 set을 사용할 수 있음. <br> - 예를들어, 두개의 input을 더하는 action이 있다면 (x + y = z), 이것의 output인 sum (z)를 다른 actions의 input으로 사용할 수 있습니다. <br> - Output을 선언하지 않아도, output을 워크플로우내에서 사용할 수 있습니다. Output에 대한 추가적인 정보는 ["Workflow commands for GitHub Actions."](https://docs.github.com/en/enterprise-server@3.1/actions/reference/workflow-commands-for-github-actions/#setting-an-output-parameter)<br> <pre> outputs: <br>  sum: # id of the output<br>    description: 'The sum of the inputs' </pre>
   runs | **Required** action의 코드와 코드를 실행하는 필요한 어플리케이션에 대한 경로 설정 
   branding | 자신의 action을 구분할 수 있도록 특정 색깔과 Feather 아이콘을 사용해 뱃지를 생성. 뱃지는 GitHub Marketplace에서 action이름의 옆에 보여짐. 

<br>

4. input

     key | 설명
     --|-- 
     `inputs.<input_id>` | **Required** input에 대한 고유의 `string` identifier. `<input_id>`는 letter 또는 `_`로 시작해야 하며, 알파벳문자와 `-`, `_`만 허용
     `inputs.<input_id>.description` | **Required** input 파라미터에 대한 `string` 정의
     `inputs.<input_id>.required` | **Required** action이 해당 input 파라미터가 요구되는지에 대한 `boolean` 값. 반드시 요구될 때 `true` 로 설정
     `inputs.<input_id>.default` | **Optional** 사용할 기본값 설정 `string`. 워크플로우에 input 파라미터가 지정되지 않았을 때 사용
     `inputs.<input_id>.deprecationMessage` | **Optional** warning메세지로 logging되는 `string`. 이 warning메세지를 사용해 사용자에게 input이 deprecated되었고, 다른 대안들을 언급하는데 사용할 수 있음. 

<br>

5. output

   key | 설명
   --|-- 
   `outputs.<output_id>` | **Required** output에 대한 고유의 `string` identifier. `<output_id>`는 letter 또는 `_`로 시작해야 하며, 알파벳문자와 `-`, `_`만 허용
   `outputs.<output_id>.description` | **Required** output 파라미터에 대한 `string` 정의
   
   - `Outputs` for composite run steps actions
   
      key | 설명
      --|--
      `outputs` | **Optional** `output`은 `outputs.<output_id>`와 `outputs.<output_id>.description`과 같은 파라미터 사용하지만, `value`토큰을 포함 <pre>outputs:<br>  random-number:<br>    description: "Random number"<br>    value: ${{ steps.random-number-generator.outputs.random-id }}<br>runs:<br>  using: "composite"<br>  steps:<br>    - id: random-number-generator<br>      run: echo "::set-output name=random-id::$(echo $RANDOM)"<br>      shell: bash </pre>
      `outputs.<output_id>.value` | **Required** action이 해당 input 파라미터가 요구되는지에 대한 `boolean` 값. 반드시 요구될 때 `true` 로 설정
   
<br>

6. `runs` for Javascript action

     key | 설명
     --|-- 
     `runs` | **required**. composite action와 코드를 실행하는데 필요한 어플리케이션에 대한 경로설정<pre>runs:<br>  using: 'node12'<br>  main: 'main.js'</pre>
     `runs.using` | **required** `main`에 지정된 코드를 실행할 어플리케이션
     `runs.main` | **required** action의 코드가 있는 파일. `using`에서 지정된 어플리케이션이 이 파일을 실행.
     `pre` | **Optional** `main:` action의 시작전에 job의 시작 단계에 실행될 스크립트. 예를 들어, 전제 조건으로 필요한 setup 스크립트를 실행. `using`에서 지정된 어플리케이션이 이 파일을 실행.<pre>runs:<br>  using: 'node12'<br>  pre: 'setup.js'<br>  main: 'index.js'<br>  post: 'cleanup.js' </pre>
     `pre-if` | **Optional** `pre:` action 실행을 위한 조건을 설정. `pre:` action은 `pre-if`의 조건이 부합할 때만 실행됨. <br> - example: `cleanup.js` 는 Linux-based 러너에서만 실행됨 <pre> pre: 'cleanup.js'<br> pre-if: runner.os == 'linux'</pre>
     `post` | **Optional** `main:` action이 완료되면 job의 마지막에 실행될 스크립트. 예를 들어, 특절 프로세스를 종료하거나 불필요한 파일을 삭제. `using`에서 지정된 어플리케이션이 이 파일을 실행. <pre>runs:<br>  using: 'node12'<br>  main: 'index.js'<br>  post: 'cleanup.js'</pre>
     `post-if` | **Optional** `post:` action 실행을 위한 조건을 설정. `post:` action은 `post-if`의 조건이 부합할 때만 실행됨. <br> - example: `cleanup.js` 는 Linux-based 러너에서만 실행됨 <pre> post: 'cleanup.js'<br> post-if: runner.os == 'linux'</pre>

<br>

7. `runs` for composite run steps action

   key | 설명
   --|-- 
   `runs` | **required**. composite action와 코드를 실행하는데 필요한 어플리케이션에 대한 경로설정
   `runs.using` | **required** action에서 composite run steps를 사용하려면 `"composite"`으로 설정
   `runs.steps` | **required** action에서 실행시킬 steps
   `runs.steps[*].run` | **required** 실행할 커맨드. inline 또는 저장소내 스크립트 <pre>runs:<br>  using: "composite"<br>  steps:<br>    - run: ${{ github.action_path }}/test/script.sh<br>      shell: bash</pre> - 또는 `$GITHUB_ACTION_PATH`를 사용 <pre>runs:<br>  using: "composite"<br>  steps:<br>    - run: $GITHUB_ACTION_PATH/script.sh<br>      shell: bash</pre>
   `runs.steps[*].shell` | **required** command를 실행할 shell 지정. [list중](https://docs.github.com/en/enterprise-server@3.1/actions/reference/workflow-syntax-for-github-actions#using-a-specific-shell) 지정
   `runs.steps[*].name` | **Optional** composite run step의 이름
   `runs.steps[*].id` | **Optional** step에 대한 고유의 id. `id`를 사용해 Contexts에서 step을 참조할 수 있음 (["Context and expression syntax for GitHub Actions"](https://docs.github.com/en/enterprise-server@3.1/actions/reference/context-and-expression-syntax-for-github-actions))
   `runs.steps[*].env` | **Optional** 해당 step에 대한 environment variable의 `map` 설정. 워크플로우에 저장된 environment variable을 수정하려면, composite 실행 step에서 `echo "{name}={value}" >> $GITHUB_ENV` 사용
   `runs.steps[*].working-directory` | **Optional** command가 실행되는 working 디렉토리 설정  
   
<br>

8. `runs` for Docker action

   key | 설명
   --|-- 
   `runs` | **required**. Docker action이 사용할 이미지 설정 <br> - Example using a Dockerfile in your repository <pre>runs:<br>  using: 'docker'<br>  image: 'Dockerfile'</pre> <br> - Example using public Docker registry container <pre>runs:<br>  using: 'docker'<br>  image: 'docker://debian:stretch-slim'<br>
   `runs.using` | **required**  반드시 `'docker'`로 설정
   `pre-entrypoint` | **Optional** `entrypoint`의 action이 시작되기 전 필요한 스크립트를 실행할 수 있도록 해줌<br> - 예를들어, 전제조건으로 필요한 setup script을 실행<br> - GitHub Actions는 `doker run`을 사용해 이 action을 시작하고, 동일한 베이스 이미지를 사용하는 새로운 컨테이너에서 스크립트를 실행.<br> - 이것은 즉, runtime 상태가 main `entrypoint`컨테이너와 다르다는 것을 의미하고, 필요한 state는 workspace, `HOME` 또는 `STATE_` variable로 접근하여야 함을 의미합니다. <br> - `pre-entrypoint:`는 항상 실행되지만, `pre-if`를 사용해 덮어쓸 수 있습니다. <pre>runs:<br>  using: 'docker'<br>  image: 'Dockerfile'<br>  args:<br>    - 'bzz'<br>  pre-entrypoint: 'setup.sh'<br>  entrypoint: 'main.sh' </pre>
   `runs.image` | **required** action을 실행하기 위한 컨테이너로 사용할 도커이미지. 도커 베이스 이미지 이름, 또는 저장소내의 `Dockerfile`, 도커 허브 또는 다른 레지스트리의 퍼블릭 이미지. <br> - 저장소내의 `Dockerfile`을 참조하기 위해서는, 파일 이름이 `Dockerfile`이어야 하고, 메타데이터 파일로 부터의 상대 경로를 사용해야 합니다. 
   `runs.env` | **Optional**  컨테이너 환경내에 environment variables의 key/value map을 설정
   `runs.entrypoint` | **Optional** 이 설정을 사용해 `Dockerfile`내에 지정된 `ENTRYPOINT`를 덮어씌우거나, `Dockerfile`이 `ENTRYPOINT`를 지정하지 않았을 때 사용. `ENTRYPOINT`는 shell 또는 exec 형태. 
   `post-entrypoint` | **Optional** `runs.entrypoint`가 완료되면 cleanup 스크립트를 실행할 수 있음. <br> - GitHub Actions는 `doker run`을 사용해 이 action을 시작 <br> - GitHub Actions는 동일한 베이스이미지를 사용하는 새로운 컨테이너에서 스크립트를 실행하므로, runtime 상태는 main `entrypoint`컨테이너와 다름. <br> - 필요한 state는 workspace, `HOME` 또는 `STATE_` variable로 접근가능. <br> - `post-entrypoint:`는 항상 실행되지만, `post-if`를 사용해 덮어쓸 수 있습니다. 
   `runs.args` | **Optional** 도커 컨테이너를 위한 input을 정의. Input은 hardcode된 string을 포함할 수 있습니다. `args`는 컨테이너의 `ENTRYPOINT`로 전달. <br> - `args`는 `Dockerfile`내에 `CMD` 대신에 사용됨. `Dockerfile`내에 `CMD`를 사용하려면, 아래 가이드라인을 따라 사용. <br> 1. 필요한 arguments들을 action의 README에 명시하고, `CMD` instruction에서 제외시킴 <br> 2. defaults 값을 사용해 `args`를 지정하지 않아도 action을 사용할 수 있도록 함 <br> 3. 만약 action이 `--help` flag 또는 비슷한 것을 노출한다면, 자체 문서화를 위해 이것을 사용할 것을 권고
   
   
   
