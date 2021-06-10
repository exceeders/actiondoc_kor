
# GitHub Actions_gettingStarted on GitHub Enterprise Server
![image](https://user-images.githubusercontent.com/40287191/121128830-fa826100-c866-11eb-80be-55502d6a757f.png)
- GA on GHES version 3.0
- GitHub플랫폼과 통합된 CI/CD환경
- 모든 GitHub Event에 대응하는 워크플로우개발
- 워크 플로우의 커뮤니티 공동 개발 및 활용
- Any platform, any language, any cloud
- Linux, macOS, Windows, and containers
- Matrix builds
- Streaming, searchable, linkable logs
- Built-in secret store
- Easy to write, easy to share

# GitHub Actions는 커뮤니티 기반으로 함께 성장합니다. 
- GitHub Actions는 큰 특징 중 하나는 커뮤니티 기반이라는 점 입니다. Actions들이 커뮤니티에 공유되어 있고, 필요한 Actions들을 검색하여 찾아 선언만으로 쉽게 사용할 수 있습니다. 
- 현재 [GitHub Marketplace에 8,000여개 이상의 Actions](https://github.com/marketplace?type=actions)들이 공유되어 있습니다. (Jun 2021 기준)

<br/>


# 1. GHES Actions/Packages 를 구성하기 위해 필요한 것? 🤔
<details><summary> </summary>
<p>
 
  ![image](https://user-images.githubusercontent.com/40287191/121131031-2f43e780-c86a-11eb-8bb0-e81b496cc3d1.png)
 
  ### 1. GitHub Enterprise Server with version 3.0 or higher
   - 3.0 with Actions : Actions의 사용을 위해 하드웨어 리소스 증가 필요 [Link](https://docs.github.com/en/enterprise-server@3.1/admin/installation/setting-up-a-github-enterprise-server-instance/installing-github-enterprise-server-on-azure#hardware-considerations)
   - CPU/메모리 별 최대 throughput을 나타내는 Job 갯수 : [GitHub 내부 테스트 설명 Link](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/getting-started-with-github-actions-for-github-enterprise-server)
  
  ### 2. [ Self-hosted Runner](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners)
   - 실제 Job을 수행할 환경 (Linux/Window/Mac)
   - GitHub-hosted runner는 현재 GitHub Enterprise Cloud에서만 가능 (GitHub Enterprise Server는 향후지원예정)
  
  ### 3. S3 compatible blob storage
   - Actions 로그 및 Packages 저장용
   - [Azure blob storage](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-azure-blob-storage), [AWS](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-amazon-s3-storage)
   - 순수 온프렘을 위해서는 [MinIO NAS Gateway](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-minio-gateway-for-nas-storage)



</p>
</details>

# 2. GHES Actions/Packages 설정 🛠️

<details><summary> </summary>
<p>
  
  ### 1. Instance에서 Actions/Packages 활성화 및 S3 blob storage 설정
 
  <details><summary> </summary>
  <p>
   
  ![image](https://user-images.githubusercontent.com/40287191/121275294-4edd1d80-c907-11eb-9946-16f815db6537.png)

   - **Force path style** 선택
  ![image](https://user-images.githubusercontent.com/40287191/121549627-fc0b7f00-ca48-11eb-80d5-fa7813baeed8.png)

   </p>
   </details>
 
  ### 2. GitHub Enterprise 레벨에서의 조직별 활성화/비활성화 설정 및 사용할 Actions 허용정책 설정
 
   <details><summary> </summary>
   <p>
    
   - Enterprise 설정 > Policies > Actions [메뉴](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enforcing-github-actions-policies-for-your-enterprise) 
   
   - 'Enable for all organizations' 또는 허용할 조직 선택
   <img src="https://user-images.githubusercontent.com/40287191/121139336-9ade8280-c873-11eb-8567-bcc028a8dfef.png" width="550" height="550">

  <br/>  
  <br/>
  <br/>  
    
  - 허용할 Actions 타입 선택
    
   - Allow all actions : 모든 Actions 허용
   - Allow local actions only : Enterprise 내부의 저장소에 정의된 Actions들만 허용
   - Allow select actions : 선택된 Actions들만 허용
   
   <img src="https://user-images.githubusercontent.com/40287191/121136603-cdd34700-c870-11eb-8257-9fc9f530b5d1.png" width="800" height="500">

  <br/>  
  <br/>
  <br/>  
    
   - Private folk로 부터의 Pull Requests에 의한 Workflow 실행 허용
  
   <img src="https://user-images.githubusercontent.com/40287191/121136657-db88cc80-c870-11eb-8b21-ee6ca6d4eed7.png" width="600" height="200">

   </p>
   </details>
 
  ### 3. Org 레벨에서의 Actions 허용 정책 설정
 
  <details><summary> </summary>
   <p>
    
   - Org 설정 > Actions [메뉴](https://docs.github.com/en/enterprise-server@3.1/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization)
   - Enterprise 레벨의 Actions 관련 정책 설정과 동일 : 허용할 Actions 설정 및 Private folk로 부터의 PR에 의한 워크플로우 실행
    
   </p>
   </details>
 
  ### 4. Repo 레벨에서의 Actions 허용 정책 설정
  
   <details><summary> </summary>
   <p>

   - Repo 설정 > Actions [메뉴](https://docs.github.com/en/enterprise-server@3.1/github/administering-a-repository/managing-repository-settings/disabling-or-limiting-github-actions-for-a-repository)
   - Enterprise 및 Org 레벨의 Actions 관련 정책 설정과 동일한 설정 : 허용할 Actions 설정 및 Private folk로 부터의 PR에 의한 워크플로우 실행

   </p>
   </details>
   
   
   
</p>
</details>

<br/>


# 3. Actions 구성요소 🤖

<details><summary> </summary>
<p>
 
### 1. [Actions Runner 설명](runner/runner_explain.md)
### 2. [Minio Gateway for NAS Storage](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-minio-gateway-for-nas-storage)
 
   - Minio NAS Gateway는 [Docker를 이용해 쉽게 구성](https://docs.min.io/docs/minio-gateway-for-nas.html)이 가능합니다. 
   
   - 버킷 생성 후 GitHub Enterprise Server와 연동
 
   - GitHub Enterprise Server가 HTTP Proxy Server와 연동되어 있다면, `localhost` 와 `127.0.0.1`을 `HTTP Proxy Exclusion list`에 추가
 
     ![image](https://user-images.githubusercontent.com/40287191/121275451-b5623b80-c907-11eb-9e55-16fa98a478e2.png)

 
</p>
</details>
   
<br/>


# 4. On-prem에서 GitHub.com/Marketplace의 Actions 사용을 위한 설정 및 인터넷 연결이 불가한 경우 사용방법

<details><summary> </summary>
<p>
 
### 1. GHES에는 기본 Actions들이 빌트인으로 포함되어 있습니다. 
 
  - [빌트인 Actions Org설명](runner/builtin_actions_org.md) 
 
 
### 2. [GitHub.com/Marketplace의 Action 사용을 위해 Connect 설정 허용](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/enabling-automatic-access-to-githubcom-actions-using-github-connect)
 
 - GHES에서는 GitHub.com 또는 GitHub Marketplace의 Actions를 직접적으로 사용할 수 없으나, `GitHub Connect`를 이용해 [옵션을 허용](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/enabling-automatic-access-to-githubcom-actions-using-github-connect#enabling-automatic-access-to-all-githubcom-actions)해 주면 사용이 가능합니다. 
 
 - Site-admin에 의한 설정 : Site admin메뉴 > Enterprise overview > Settings > GitHub Connect 
  
   <img src="https://user-images.githubusercontent.com/40287191/121316856-b1a0da00-c944-11eb-91d8-203ac1641481.png" width="500" height="180">

 
### 3. [Connect 설정 및 Self-hosted 러너의 인터넷 연결이 불가한 경우, Action-sync tool 사용](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/manually-syncing-actions-from-githubcom)
 
  - [Action-sync-tool 설명](runner/action-sync-tool.md)
 
### 4. [Tool Cache(`actions/setup-LANGUAGE`)의 수동 패키지 다운로드](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/setting-up-the-tool-cache-on-self-hosted-runners-without-internet-access)
 
  - Self-hosted runner는 `setup-node`와 같은 `actions/setup-LANGUAGE`의 환경 설정을 위해 인터넷 접속이 필요합니다. 그러나 인터넷을 연결할 수 없는 Self-hosted Runner는 인터넷으로 부터 환경 설정에 필요한 바이너리들을 다운로드 받을 수 없으므로, 이를 수동으로 진행해야 합니다. 
 
  - GitHub.com에서 워크플로우를 실행하여 tool cache를 가져온 뒤, 이것을 artifact로 업로드 합니다. 이것을 다운로드하여 Self-hosted Runner에 밀어 넣어 사용합니다. 
  - [예시](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/setting-up-the-tool-cache-on-self-hosted-runners-without-internet-access#populating-the-tool-cache-for-a-self-hosted-runner)
 
### 5. [CodeQL Action-sync tool 사용](https://docs.github.com/en/enterprise-server@3.1/admin/advanced-security/configuring-code-scanning-for-your-appliance#configuring-codeql-analysis-on-a-server-without-internet-access) (참고)
 
  - GitHub Enterprise의 Code Scanning은 정적분석을 수행하는 GitHub Enterprise의 Advanced Security 기능입니다. 
  - GitHub Actions를 바탕으로 개발의 워크 플로우에 자동화된 절차로 수행되며, 이를 통해 소프트웨어 개발 주기의 가장 빠른 단계에서 보안을 수행하는 shift left의 실질적인 워크 플로우가 이루어집니다. 
  - Code Scanning은 CodeQL이라고 하는 보안 분석의 핵심 쿼리엔진이 Action으로 수행되며, 이것 역시 GHES설치 시 기본적으로 내부에 빌트인으로 포함되어 있습니다. 
  - 인터넷에 연결되어 있지 않다면, 동기화를 수동으로 수행하는 별도의 sync tool(https://github.com/github/codeql-action-sync-tool) 을 사용해 동기화 할 수 있습니다. 

</p>
</details>

<br/>


# 5. Actions의 작성 ✍️

<details><summary> </summary>
<p>
 
 ### 1. Actions를 구성하는 파일들
 
 ### 2. Workflow 파일
     
   - Workflow 파일 템플릿
   - Workflow 파일 구조
   - Workflow 트리거 
     
 
 ### 3. Job과 Runner
 
 ### 4. CodeQL Action-sync tool 사용

</p>
</details>

<br/>

 
** 본 문서는 GitHub Enterprise Server 버젼 3.1을 기준으로 작성되었습니다. 
