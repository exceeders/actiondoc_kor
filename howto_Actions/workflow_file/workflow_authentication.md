# [Workflow 내에서의 인증](https://docs.github.com/en/enterprise-server@3.1/actions/reference/authentication-in-a-workflow)

1. GitHub은 자동으로 `GITHUB_TOKEN`을 생성합니다. 이것은 워크플로우내에서 인증을 위해 편리하게 사용될 수 있습니다. 각 job이 시작되기 전, GitHub은 job을 위한 `GITHUB_TOKEN`을 가져오고, job실행이 완료되면 만료됩니다.

2. `GITHUB_TOKEN`은 [기본 권한](https://docs.github.com/en/enterprise-server@3.1/actions/reference/authentication-in-a-workflow#permissions-for-the-github_token)을 가지고 있습니다.
   - 만약 기본 권한 이외에 추가적인 권한이 필요하다면, Personal Access token을 만들어 충분한 권한을 설정하여 사용해야 합니다.  
   
   <br/>
   
   Scope	| Access type	| Access by forked repos
   --|--|--
   actions | read/write |	read
   checks |	read/write |	read
   contents | read/write	| read
   deployments | read/write |	read
   issues |	read/write	| read
   metadata | read	| read
   packages	| read/write	| read
   pull requests	| read/write	| read
   repository projects	| read/write	| read
   statuses |	read/write	| read

3. `GITHUB_TOKEN`을 사용하려면, 워크 플로우에 아래 예와 같이 `${{ secrets.GITHUB_TOKEN }}` 을 사용하면 됩니다. 

   ```
      name: Pull request labeler

      on: [ pull_request_target ]

      jobs:
        triage:
          runs-on: ubuntu-latest
          steps:
            - uses: actions/labeler@v2
              with:
                repo-token: ${{ secrets.GITHUB_TOKEN }}
    ```
    
 4. Personal Access Token은 `${{ secrets.SECRET_NAME }}` 과 같이 사용합니다. 
