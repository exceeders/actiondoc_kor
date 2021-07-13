# howto_Actions ✨
<img src="https://user-images.githubusercontent.com/40287191/122417056-2ec2f380-cfc4-11eb-8147-b3e869b1fb4a.png" width="460" height="250">



# 1. 🎯 Actions 작성, 사용, 공유 

<details><summary> </summary>
<p>
  
  - Actions는 전체 Workflow의 각 단계를 구성하는 단위 요소이며, 각각 지정된 동작을 수행합니다. 
  
  - 저장소와 상호작용하는 action을 생성할 수 있고, 이것을 이용해 GitHub API와 다른 third-party API와 통합하는 action도 생성할 수 있습니다. 예를 들어, npm module을 publish하는 action, 긴급한 issue가 생성되었을 때 SMS alert를 보내는 action, 또는 상용할 준비가된 코드를 deploy하는 action등을 생성할 수 있습니다. 
  
  
  - Workflow는 여러 Actions들을 포함하며, 각 Actions들을 커뮤니티에서 만들어진 것을 사용하거나, 직접 만들어서 사용할 수 있습니다.
    
     ```
     steps:
       - uses : {owner}/{repo}@{ref}
     ```

     ```
     steps
       - uses : ./path/to/dir 
     ```
  
  - [현재 저장소에서 만들어진 Actions를 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/finding-and-customizing-actions#referencing-an-action-in-the-same-repository-where-a-workflow-file-uses-the-action)하기 위해서는 아래 example과 같이 구성합니다. 
  
    - 디렉토리
      ```
      |-- hello-world (repository)
      |   |__ .github
      |       └── workflows
      |           └── my-first-workflow.yml
      |       └── actions
      |           |__ hello-world-action
      |               └── action.yml
      ```
    - Workflow 파일
      ```
      jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          # This step checks out a copy of your repository.
          - uses: actions/checkout@v2
          # This step references the directory that contains the action.
          - uses: ./.github/actions/hello-world-action
      ```
  
  - 만약 [Docker Hub에 컨테이너 이미지로 된 Actions를 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/finding-and-customizing-actions#referencing-a-container-on-docker-hub)한다면 아래와 같이 지정합니다. 
  
  ```
  jobs:
   my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
  ```
  
  
  
  - 함께 사용할 Actions를 작성한다면, [별도의 저장소에 Actions를 만들고 공유하는 것이 좋습니다](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/about-actions#choosing-a-location-for-your-action). (Application등의 코드와 섞이지 않게)
  
  - 함께 사용할 Actions는 [release management를 하여 version tag을 통해](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/about-actions#good-practices-for-release-management) 사용하도록 하는 것이 좋습니다. 
  
    - Tag 
    
     ```
     steps:
       - uses: actions/javascript-action@v1
     ```
  
    - Tag
     ```
     steps:
       - uses: actions/javascript-action@v1.0.1
     ```
  
    - branch
     ```
     steps:
       - uses: actions/javascript-action@v1-beta
     ```
  
    - SHA
     ```
     steps:
       - uses: actions/javascript-action@172239021f7ba04fe7327647b213799853a9eb89
     ```
 
 - [Actions의 종류](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/about-actions#types-of-actions)
   
    - Actions는 Docker container와 JavaScript, 그리고 여러 명령어를 묶어 하나의 action으로 실행하는 세 가지  있습니다. 
    - Actions는 메타데이터 파일을 이용해 input, output 그리고 main entrypoint를 지정할 수 있습니다. 메타데이터 파일의 이름은 `action.yml` 또는 `action.yaml` 이어야 합니다. 
    
       Type |	Operating system
       --|--
       Docker container	| Linux
       JavaScript	| Linux, macOS, Windows
       Composite run steps	| Linux, macOS, Windows
    
    - ℹ️ 메타데이터 파일(`action.yml`, `action.yaml` ) [syntax 참조](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/metadata-syntax-for-github-actions)
       - [Syntax 설명](actions_metadata.md)
  
  
  
 </p>
 </details>

<br/>

# 2. Actions의 주요 features

<details><summary> </summary>
<p>
  
  1. [Workflow내 Variable 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/essential-features-of-github-actions#using-variables-in-your-workflows)
    
     - GitHub Actions는 [기본 환경 변수](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environment-variables#default-environment-variables)들을 가지고 있습니다.
     - 또, 필요시 Workflow 파일내에 필요한 환경 변수들을 생성하고 사용할 수 있습니다. 
     - 아래 예시는, `POSTGRES_HOST` 와 `POSTGRES_PORT`를 생성하고 `node client.js`에서 사용하는 예제 입니다. 
  
       ```
        jobs:
        example-job:
            steps:
              - name: Connect to PostgreSQL
                run: node client.js
                env:
                  POSTGRES_HOST: postgres
                  POSTGRES_PORT: 5432
       ```
  
     - [Environment variables](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environment-variables) 참조
  
  <br/>
  
  2. [Workflow에 스크립트 추가](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/essential-features-of-github-actions#adding-scripts-to-your-workflow)
   
     - `run` 키워드를 사용해 스크립트나 쉘 명령어를 수행하는 Actions를 구성할 수 있습니다. 
  
       ```
       jobs:
         example-job:
          steps:
            - run: npm install -g bats
       ```

       ```
       jobs:
          example-job:
            steps:
              - name: Run build script
                run: ./.github/scripts/build.sh
                shell: bash
       ```
  
  <br/>
  
  3. [Job간의 데이터 공유](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/essential-features-of-github-actions#sharing-data-between-jobs)
  
     - 같은 workflow내에서 어느 job이 생성한 파일을 다른 job에 공유하도록 구성할 수 있습니다. 
     - 또는, 향후의 참조를 위해 생성된 파일을 artifact로 저장할 수 있습니다. 
     - Artifact는 빌드와 테스트를 거쳐 생성된 파일들 입니다. (예: 바이너리, 패키지 파일들, 테스트 결과, 로그 파일, 화면 스크린 샷)
     - 예를 들어, 아래와 같이 파일을 생성하고 artifiact로 업로드 합니다. 

     ```
     jobs:
        example-job:
          name: Save output
          steps:
            - shell: bash
              run: |
                expr 1 + 1 > output.log
            - name: Upload output file
              uses: actions/upload-artifact@v2
              with:
                name: output-log-file
                path: output.log
     ```

     - `actions/download-artifact` Actions를 사용하여, 별도의 workflow 실행에서 위의 파일을 다운로드 할 수 있습니다. 

  
     ``` 
      jobs:
        example-job:
          steps:
            - name: Download a single artifact
              uses: actions/download-artifact@v2
              with:
                name: output-log-file
     ```
  
  <br/>
  
  4. [Secret의 저장](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#storing-secrets)
   
     - Workflow 내에서 패스워드 또는 certificate을 사용해야 할 때, 저장소 또는 조직에 `secret`을 저장하고 환경 변수로서 사용할 수 있습니다. 
   
      ```
      jobs:
        example-job:
          runs-on: ubuntu-latest
          steps:
            - name: Retrieve secret
              env:
                super_secret: ${{ secrets.SUPERSECRET }}
              run: |
                example-command "$super_secret"
      ```
 
  <br/>
  
  5. [Dependent job 생성](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#creating-dependent-jobs)
  
       - 기본적으로 workflow내의 모든 job들은 동시에 실행됩니다. 따라서, 어떠한 job이 반드시 다른 job이 끝난 이후에 실행되어야 한다면, `needs` 키워드를 사용하여 이러한 의존성을 설정할 수 있습니다. 

       ```
       jobs:
          setup:
            runs-on: ubuntu-latest
            steps:
              - run: ./setup_server.sh
          build:
            needs: setup
            runs-on: ubuntu-latest
            steps:
              - run: ./build_server.sh
          test:
            needs: build
            runs-on: ubuntu-latest
            steps:
              - run: ./test_server.sh
       ```
  
  <br/>
  
  6. [Build Matrix 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-a-build-matrix)
  
       - Build Matrix를 이용해 OS, 플랫폼, 언어등의 다양한 조합으로 동시에 워크 플로우를 실행할 수 있습니다. 
       - Build Matrix는 `strategy` 키워드로 구성합니다. 

       ```
       jobs:
          build:
            runs-on: ubuntu-latest
            strategy:
              matrix:
                node: [6, 8, 10]
            steps:
              - uses: actions/setup-node@v2
                with:
                  node-version: ${{ matrix.node }}
       ```
   
  <br/>
  
  7. [Database와 서비스 컨테이너 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-databases-and-service-containers)
  
       - Job이 데이터베이스 또는 Cache 서비스를 필요로 한다면, `services` 키워드를 사용하여 한시적으로 서비스를 생성할 수 있습니다. 이렇게 생성된 컨테이너는 해당 job내 모든 step들이 사용할 수 있고, job의 실행이 완료되면 삭제됩니다.
       - 아래 예는, job이 `services`를 사용해 `postgre` 컨테이너를 생성하고 `node`를 사용해 서비스에 연결하는 방법을 보여줍니다. 

      ```
      jobs:
        container-job:
          runs-on: ubuntu-latest
          container: node:10.18-jessie
          services:
            postgres:
              image: postgres
          steps:
            - name: Check out repository code
              uses: actions/checkout@v2
            - name: Install dependencies
              run: npm ci
            - name: Connect to PostgreSQL
              run: node client.js
              env:
                POSTGRES_HOST: postgres
                POSTGRES_PORT: 5432
      ```
  
  <br/>
  
  8. [Label의 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-labels-to-route-workflows)

       - job을 특정 self-hosted 러너에 할당하기 위해 label을 사용합니다. 특정 형태의 러너가 job을 실행하도록 하기 위해 label을 사용해 job이 실행될 러너를 지정합니다. 

       ```
       jobs:
        example-job:
          runs-on: [self-hosted, linux, x64, gpu]
       ```
 
  <br/>
  
  9. [Environment 사용](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-environments)
  
       - Environment에 대한 보호 룰과 secret을 설정할 수 있습니다. 
       - 각 job은 하나의 environment를 참조할 수 있습니다. 
       - Job이 참조하는 environment가 러너로 보내지기 전에, 해당 environment에 대한 보호룰을 먼저 통과 해야만 합니다. 
       - ['Environment'](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environments) 참조
  
</p>
</details>

<br/>


# 3. Workflow 파일 ♾️
 
 <details><summary> </summary>
 <p>
   
   1. ⚙️ [Workflow 파일 구조](workflow_file/workflow_file_component.md)
   
   2. [Workflow 파일 템플릿 : 조직내 워크플로우 공유](workflow_file/workflow_template.md) 📔
   
   3. [Workflow 트리거](workflow_file/workflow_trigger.md) 🔫
   
   4. [Workflow 파일 YAML 예제와 설명](workflow_file/workflow_yaml_syntax.md) 📗
   
   5. [👷 Workflow 실행 관리](workflow_file/workflow_manage.md)
   
   6. [Workflow 내에서의 인증 : `GITHUB_TOKEN` 또는 PAT ](workflow_file/workflow_authentication.md) 🔑

   7. Workflow syntax, Workflow Command, Context/Expression Syntax
     
      - ✅ [Workflow syntax](workflow_file/workflow_detail_syntax.md)
   
      - [Workflow Commands](workflow_file/workflow_commands.md)

      - [Context and expression syntax](workflow_file/context_and_expression_syntax.md)
   
 
 
   </p>
 </details>

<br/>
 
# 4. Docker 컨테이너 Actions 📦
 
 <details><summary> </summary>
 <p>
   
   - Docker 컨테이너는 GitHub Actions의 코드와 실행환경을 함께 패키징합니다. 이것은 Actions의 사용자가 tool이나 의존성등을 걱정할 필요없이 더욱 일관되고 신뢰할 수 있는 action 실행 단위를 만들어 줍니다. 
   - Docker 컨테이너를 통해 OS의 특정 버젼, 의존성, tools와 코드를 사용할 수 있습니다. 특정한 환경 구성에서 동작해야만 하는 actions들은 Docker가 가장 적합한 방법입니다. 컨테이터를 생성하고 필요한 것들을 가져오는 데 소요되는 latency로 인해 JavaScript actions에 비해 느립니다.
   - Docker 컨테이너 actions는 Linux의 러너에서만 실행됩니다. Self-hosted 러너는 OS로 Linux, 그리고 Docker가 함께 설치되어 있어야 Docker 컨테이너 action을 실행할 수 있습니다. 
   
   - [Docker 컨테이너 actions 생성 방법 예시](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/creating-a-docker-container-action)
   
 </p>
 </details>
 
<br/>
 

# 5. JavaScript Actions 📜

 <details><summary> </summary>
 <p>
   
   - JavaScript actions는 러너 머신에서 직접적으로 실행되고, action의 코드가 코드를 실행하는데 사용되는 환경으로 부터 분리됩니다. 

   - JavaScript actions를 이용하면 Docker 컨테이너 action보다 action의 코드를 더 단순화하고, 더 빠르게 실행할 수 있습니다. 
   
   - JavaScript actions가 모든 GitHub-hosted runners (Ubuntu, Windows, macOS)와 호환될 수 있도록 하기 위해, 여러분이 작성하는 JavaScript 코드는 온전한 JavaScript여야 하고, 다른 바이너리들에 의존하면 안됩니다. JavaScript actions는 러너에서 직접적으로 실행되며, virtual environment에 이미 존재하는 바이너리들을 사용합니다.
   
   - 여러분이 Node.js 프로젝트를 개발한다면, 여러분이 사용할 수 있는 GitHub Actions Toolkit을 사용하여 더 빠르게 개발할 수 있습니다. (추가정보는 actions/toolkit repository참조)
   
   - [JavaScript actions 생성 방법 예시](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/creating-a-javascript-action)
   
   
   
 </p>
 </details>
 
 <br/>
 

# 6. Composite run steps Actions

 <details><summary> </summary>
 <p>

   - _Composite run steps_ actions는 하나의 action에 여러개의 steps들을 묶어 실행시킬 수 있습니다.
   
   - 예를 들어, 여러개의 run 명령어를 하나의 action에 묶어서 워크플로우가 이 묶음 명령어를 하나의 step으로 처리하도록 하는 방식입니다. 
   
   - [Composite run step action 생성 방법 예시](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/creating-a-composite-run-steps-action)
 
 </p>
 </details>

 <br/>
 



