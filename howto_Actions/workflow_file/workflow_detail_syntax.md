# [Workflow syntax](https://docs.github.com/en/enterprise-server@3.1/actions/reference/workflow-syntax-for-github-actions) 



syntax | 설명
--|--
`name` | 워크플로우 이름
`on` | **Required** . 워크플로우가 트리거될 조건
`on.<event_name>.types` | 워크플로우가 트리거되는 이벤트의 이름과 세부 타입 <br> 예: <pre> on: <br>  release:  <br>   - types: [published, created, edited] </pre>
`on.<push \| pull_request>.<branches \| tags>` | `push` 와 `pull_reques` 이벤트에 대해 적용할 브랜치와 tag 설정  <br> <pre> on: <br>  push: <br>   branches: <br>    - main <br>    - 'mona/octocat' <br>    - 'releases/\*\*' <br>   tags: <br>    - v1 <br>    - v1.* </pre>  - `branches-ignore`: 제외할 브랜치  <br> - `tags-ignore`: 제외할 tag <br> - 브랜치와 tag이름에 \*\*사용, '!' negative 패턴 <pre> - branches: <br>  - 'releases/\*\*' <br>  - '!releases/\*\*-alpha' </pre>
`on.<push\|pull_request>.paths` |  `paths`/`paths-ignore` : 적용할 패스와 제외할 패스
`on.schedule` | 워크 플로우 트리거 스케쥴지정 (cron)
`env`| 워크플로우 내 모든 job들에서 사용 가능한 환경 변수
`defaults`| 워크플로우 내 모든 job들에 적용할 default 세팅
`defaults.run` | 디폴트로 사용할 `shell` 과 `working-directory` 설정 <pre> default: <br>  run: <br>   shell: bash <br>   working-directory: scripts </pre> 
`concurrency` | 같은 concurrency 그룹을 사용하는 워크플로우나 job이 동시에 하나만 실행 <br> <pre>- concurrency: ci-${{ github.ref }} <br>- concurrency: staging_environment <br>- concurrency:<br>    group: ${{ github.head_ref }} <br>    cancel-in-progress: true </pre>
`jobs.<job_id>.needs` | 워크 플로우내 job들은 기본적으로 동시에 실행되나, 'needs'를 이용해 순차적으로 실행
`jobs.runs-on` | **Required** 실행될 러너 
`jobs.environment` | Job이 참조하는 environment. 'environment protection rule'에 의해 보호되기 위해 지정하는 environment
`jobs.<job_id>.concurrency` | 동일한 concurrency group에 있는 job은 동시에 하나의 job만 수행되도록 함
`jobs.<job_id>.outputs` | Job의 아웃풋. `needs` 키워드로 이 Job에 의존하는 모든 다운스트림 job들이 사용가능 <pre> jobs: <br>  job1: <br>    runs-on: ubuntu-latest <br>    # Map a step output to a job output <br>    outputs: <br>      output1: ${{ steps.step1.outputs.test }} <br>      output2: ${{ steps.step2.outputs.test }} <br>    steps: <br>      - id: step1 <br>        run: echo "::set-output name=test::hello" <br>      - id: step2 <br>        run: echo "::set-output name=test::world" <br>  job2: <br>   runs-on: ubuntu-latest <br>    needs: job1 <br>    steps: <br>       - run: echo ${{needs.job1.outputs.output1}} ${{needs.job1.outputs.output2}}
`jobs.<job_id>.env`| job내에 모든 step들에 사용가능한 환경변수
`jobs.<job_id>.defaults`| job내에 모든 step들에 적용되는 default 세팅
`jobs.<job_id>.defaults.run`| 'run' 스텝에 디폴트 `shell` 과 `working-directory` 설정
`jobs.<job_id>.if` | `if` 컨디션을 통해 조건이 충족되지 못할 경우 job의 실행을 방지 <br> `if`조건의 표현식에서 연산자가 없다면 `${{ }}` 사용하지 않아도 됨. 
`jobs.<job_id>.uses` | step에서 실행할 action <br> - `{owner}/{repo}@{ref}` <br> - `{owner}/{repo}/{path}@{ref}` <br> - `./path/to/dir` <br> - `docker://{image}:{tag}` <br> - `docker://{host}/{image}:{tag}`
`jobs.<job_id>.steps` | job내에 순차적으로 실행되는 steps
`jobs.<job_id>.steps[*].if` | `if` 컨디션을 통해 조건이 충족되지 못할 경우 step의 실행을 방지 <br> `if`조건의 표현식에서 연산자가 없다면 `${{ }}` 사용하지 않아도 됨. <pre> steps: <br>  - name: My first step <br>  if: ${{ github.event_name == 'pull_request' && github.event.action == 'unassigned' }} <br>  run: echo This event is a pull request that had an assignee removed.
`jobs.<job_id>.steps[*].run` | - `\|` : 멀티라인 명령어 <br> - `working-directory:` <br> - `shell`: [사용할 특정 shell 지정](https://docs.github.com/en/enterprise-server@3.1/actions/reference/workflow-syntax-for-github-actions#using-a-specific-shell) <br> 
`jobs.<job_id>.steps[*].with` | 환경 변수로 정의된 인풋 파라미터의 사용. 각 인풋 파라미터는 key/value pair <pre> jobs:<br>  my_first_job:<br>    steps:<br>      - name: My first step<br>        uses: actions/hello_world@main<br>        with:<br>          first_name: Mona<br>          middle_name: The<br>          last_name: Octocat      </pre>
`jobs.<job_id>.steps[*].with.args` | 도커 컨테이너를 위한 인풋을 정의하는 string. GitHub은 `args`를 컨테이너 시작시 `ENTRYPOINT`로 전달. <pre> steps:<br>  - name: Explain why this job ran<br>    uses: monacorp/action-name@main<br>    with:<br>      entrypoint: /bin/echo<br>      args: The ${{ github.event_name }} event triggered this step.</pre>
`jobs.<job_id>.steps[*].with.entrypoint` | `Dokerfile`내에 `ENTRYPOINT`를 덮어씀, 또는 `ENTRYPOINT`로 설정되지 않았으면 설정.
`jobs.<job_id>.steps[*].env`| 러너 환경에서 사용할 수 있도록 step을 위한 환경변수 설정
`jobs.<job_id>.steps[*].continue-on-error` | step이 실패해도 job이 계속 실행하도록 설정 : `true`
`jobs.<job_id>.steps[*].timeout-minutes` | 프로세스를 kill하기 전에 step을 실행할 최대 시간 (분)
`jobs.<job_id>.timeout-minutes` | 취소될 때 까지 job을 실행할 최대 시간 (분) Default: 360분
`jobs.<job_id>.strategy` | job에 대한 build matrix 지정
`jobs.<job_id>.strategy.matrix` | job에 대한 다양한 조합의 build matrix. <pre>strategy:<br>  matrix:<br>    node: [10, 12, 14]<br>steps:<br>  # Configures the node version used on GitHub-hosted runners<br>  - uses: actions/setup-node@v2<br>    with:<br>      # The Node.js version to configure<br>      node-version: ${{ matrix.node }} </pre>
`jobs.<job_id>.strategy.fail-fast` | matrix job중에 어느 하나가 fail되면 모든 진행중인 job을 취소: Default `true`
`jobs.<job_id>.strategy.max-parallel` | matrix job을 동시에 실행할 수 있는 최대 job수
`jobs.<job_id>.continue-on-error` | job이 fail되어도 워크플로우 계속 실행. <br> 예를 들어, 실험적인 job이 `node: 15` 에서 fail되어도 워크플로우는 계속 실행되도록 설정하려면 <pre>runs-on: ${{ matrix.os }}<br>continue-on-error: ${{ matrix.experimental }}<br>strategy:<br>  fail-fast: false<br>  matrix:<br>    node: [13, 14]<br>    os: [macos-latest, ubuntu-18.04]<br>    experimental: [false]<br>    include:<br>      - node: 15<br>        os: ubuntu-18.04<br>        experimental: true </pre>
`jobs.<job_id>.container` | job에서 step들을 실행할 컨테이너 설정. `container`를 설정하지 않으면 모든 step들은 `runs-on`에서 설정된 러너 환경에서 실행됨. <br>If you have steps that use both script and container actions, the container actions will run as sibling containers on the same network with the same volume mounts. <pre>jobs:<br>  my_job:<br>    container:<br>      image: node:14.16<br>      env:<br>        NODE_ENV: development<br>      ports:<br>        - 80<br>      volumes:<br>        - my_docker_volume:/volume_mount<br>      options: --cpus 1 </pre>
`jobs.<job_id>.container.image` | 컨테이너 이미지
`jobs.<job_id>.container.credentials` | 컨테이너 이미지의 레지스트리가 인증이 필요하다면 사용할 credential : `username`, `password`
`jobs.<job_id>.container.env` | 컨테이너 환경변수
`jobs.<job_id>.container.ports` | 컨테이너 포트
`jobs.<job_id>.container.volumes` | 컨테이너 볼륨 array
`jobs.<job_id>.container.options`| 추가적인 [도커 컨테이너 리소스 옵션](https://docs.docker.com/engine/reference/commandline/create/#options)
`jobs.<job_id>.services`| 'Service container'를 host하기 위한 선언 * 만약, 워크플로우가 도커 컨테이너 Action, 또는 service 컨테이너 action을 사용한다면, `Linux`러너를 사용해야 함 
`jobs.<job_id>.services.<service_id>.image` | 서비스 컨테이너로 사용할 도커 컨테이너 이미지
`jobs.<job_id>.services.<service_id>.credentials` | 이미지 컨테이너 레지스트의 인증을 위한 credential : `username`, `password`
`jobs.<job_id>.services.<service_id>.env` | 서비스 컨테이너에 환경변수 
`jobs.<job_id>.services.<service_id>.ports` | 서비스 컨테이너에 노출되는 포트 array
`jobs.<job_id>.services.<service_id>.volumes` | 서비스 컨테이너가 사용할 볼륨 array
`jobs.<job_id>.services.<service_id>.options` | 추가적인 [도커 컨테이너 리소스 옵션](https://docs.docker.com/engine/reference/commandline/create/#options)



