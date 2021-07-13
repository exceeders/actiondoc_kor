p
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

# :octocat: GitHub Actions는 커뮤니티 🧑‍🤝‍🧑 기반으로 함께 성장합니다. 
- GitHub Actions는 큰 특징 중 하나는 커뮤니티 기반이라는 점 입니다. Actions들이 커뮤니티에 공유되어 있고, 필요한 Actions들을 검색하여 찾아 선언만으로 쉽게 사용할 수 있습니다. 
- 현재 [GitHub Marketplace에 8,000여개 이상의 Actions](https://github.com/marketplace?type=actions)들이 공유되어 있습니다. (Jun 2021 기준)

<br/>
<br/>
<br/>

# 🎯 GitHub Actions/Packages의 GHES 설정 및 사용 

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

<br/>

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
   
   - 'Enable for all organizations' 또는 허용할 조직 👫 선택
   <img src="https://user-images.githubusercontent.com/40287191/121139336-9ade8280-c873-11eb-8567-bcc028a8dfef.png" width="600" height="550">

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


# 3. GHES Actions 을 위한 구성요소 설명 🤖

<details><summary> </summary>
<p>
 
### 1. [Actions Runner 설명](runner/runner_explain.md) 🏃
### 2. [Minio Gateway for NAS Storage](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-minio-gateway-for-nas-storage) 🧺
 
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
 
### 1. GHES에는 기본 Actions들이 빌트인 📥 으로 포함되어 있습니다. 
 
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


# 5. [Actions의 작성 ](howto_Actions/README.md)✍️ 


<br/>

# 6. Actions 이중화, 백업

<details><summary> </summary>
<p>

### [1. GitHub Actions 이중화](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/advanced-configuration-and-troubleshooting/high-availability-for-github-actions)   
   
   - GitHub Enterprise Server 자체의 백업과 이중화 구성은, Action이 사용하는 외부 S3 blob 스토리지(Azure, Amazon, MinIO)의 백업과 이중화와는 **제공하지 않습니다**. 
 
   - 외부 S3 blob 스토리지에서 제공하는 이중화 및 백업에 의존하며, 이러한 스토리지 서비스의 데이터 이중화와 replication에 대한 구성이 강력히 권고됩니다. 
 
   - GitHub Enterprise Server 운영 중, 이중화 replica를 primary로 승격하는 경우, GitHub Actions을 위해 별도의 구성이나 작업이 필요하지 않습니다. 
 
   
### [2. Backup and restoring](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/advanced-configuration-and-troubleshooting/backing-up-and-restoring-github-enterprise-server-with-github-actions-enabled)
 
   - GitHub Enterprise Server 자체의 백업과 이중화 구성은, 외부 S3 blob 스토리지의 백업 및 이중화는 제공하지 않습니다. 
 
   - GitHub Action를 사용하던 instance의 백업데이터를, 신규 인스턴스에 restore할 때의 절차는 아래와 같습니다. 
 
     1) 원래의 인스턴스가 오프라인임을 확인
     2) 새로운 GHES 인스턴스의 네트웍 구성 설정. (네트웍 구성은 백업 스냅샷에 포함되지 않고, `ghe-restore` 명령으로도 덮어씌어 지지 않음)
     3) 새로운 GHES 인스턴스에 이전 원래 인스턴스가 사용하던 동일한 외부 스토리지 등록
     4) 새로운 GHES 인스턴스에 GitHub Actions 활성화
     5) `ghe-restore` 명령으로 백업 데이터 복구
     6) Self-hosted 러너 재등록
 
 
 </p>
 </details>


<br/>


# 7. Troublshooting, 로그파일

<details><summary> </summary>
 <p>

### [1. GitHub Actions Troubleshooting](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/advanced-configuration-and-troubleshooting/troubleshooting-github-actions-for-your-enterprise) 
  
   - GHES에 Self-signed certificate 사용시 Self-hosted 러너 등록 : GHES는 공인된 기관에서 서명된 공인 인증서의 사용이 강력히 권장되지만, self-signed 인증서를 사용할 때 방법이 설명되어 있습니다. 
  
   - GitHub Actions를 위한 HTTP proxy 설정 
     - GHES 인스턴스에 HTTP Proxy server가 구성되어 있다면, **HTTP Exclusion list**에 `localhost`와 `127.0.0.1`을 설정해야 합니다. 
     - 이 설정이 되어 있지 않으면 `Resource unexpectedly moved to https://<IP_ADDRESS>`와 유사한 에러가 발생됩니다. 
  
   - hostname 변경 후 러너가 연결되지 않음
     - GHES의 호스트네임을 변경하였다면, self-hosted러너들은 이전의 호스트네임으로 연결되지 않을 것입니다. 
     - 이 경우, self-hosted 러너의 구성을 업데이트 해야 하며, 
       - self-hosted 러너의 디렉토리에서 `.runner` 와 `.credentials` 파일에서 모든 예전 호스트네임을 새로운 호스트네임으로 변경하고, self-hosted 러너 어플리케이션을 재시작
       - 또는, GHES로 부터 Self-hosted 러너를 삭제하고 다시 추가
  
   - 메모리, CPU 용량 제약으로 GitHub Actions와 Job이 멈췄을 때
     
     - 과도한 Actions의 실행으로 메모리와 CPU 용량의 한도가 되었을 경우, (러너들이 idle한 것들이 있다해도) job들이 시작되지 않고 UI상에서 아무 변화가 없는 경우가 생길 수 있습니다. 
     
     - 1. [관리 콘솔에서 CPU와 메모리 사용량 확인](https://docs.github.com/en/enterprise-server@3.1/admin/enterprise-management/accessing-the-monitor-dashboard) 
        
       - Overall system health의 CPU와 메모리 사용량에 따라 [CPU, 메모리 용량 증설](https://docs.github.com/en/enterprise-server@3.1/admin/enterprise-management/increasing-cpu-or-memory-resources) 고려 
     
       <br>
     
     - 2. 만약, CPU, 메모리 사용량에 문제가 없다면, Nomad Job 섹션에서 "CPU Percent Value"와 "Memory Usage" 그래프 확인
        - Actions와 관련된 아래 서비스들 확인
          ```
          mps_frontend
          mps_backend
          token_frontend
          token_backend
          actions_frontend
          actions_backend
          ```
        - 이러한 서비스들 중, CPU 100%에 근접하거나 메모리가 최대치(2GB by default)에 근접하는 것이 있다면, 리소스 할당을 증가할 필요가 있습니다. 
  
       <br>
  
     - 3. 최대치에 근접한 서비스들에 대한 리소스 할당량 증가
        - SSH 관리 콘솔로 GHES 인스턴스에 접속
        - 아래 명령어로 추가 할당 가능한 리소스 확인
           ```
           nomad node status -self
           ```
        - 위 명령어로 나온 결과에서 "Allocated Resources" 섹션 부분 확인
           ```
           Allocated Resources
           CPU              Memory          Disk
           7740/49600 MHZ   23 GiB/32 GiB   4.4 GiB/7.9 GiB
           ```
        - `/etc/consul-templates/etc/nomad-jobs/actions` 디렉토리로 이동
            - 이 디렉토리에는 Actions의 서비스에 관련된 아래 세가지 파일이 있습니다. 
              ```
              mps.hcl.ctmpl
              token.hcl.ctmpl
              actions.hcl.ctmpl
              ```
        - 이 중, 위에서 확인된, 증가가 필요한 파일을 열어 `resource` 그룹 부분을 확인하고, CPU, 메모리 부분을 증가시킵니다.  
           ```
             resources {
             cpu = 512
             memory = 2048
             network {
               port "http" { }
               }
             }
           ```
        - 파일을 저장하고 빠져 나옵니다. 
        - `ghe-config-apply` 명령을 실행하여 변경된 내용을 적용합니다. 
           - 이 명령 실행 중 `failed to run nomad job '/etc/nomad-jobs/<name>.hcl'`와 같은 에러가 발생한다면, CPU나 메모리가 가용한 범위보다 초과되어 할당된 것입니다. 
  
        - `ghe-actions-check`을 실행하여 Actions의 상태를 확인합니다. 
  
### [2. Self-hosted 러너 Troublshooting, 로그파일](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/monitoring-and-troubleshooting-self-hosted-runners)
  
   - [Self-hoste runner 상태 확인](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/monitoring-and-troubleshooting-self-hosted-runners#checking-the-status-of-a-self-hosted-runner) : idle, Action, Offline
  
   <img src="https://user-images.githubusercontent.com/40287191/125399198-37ec8800-e3eb-11eb-84cc-e9500a6278ba.png" width="700" height="150">

   
   - Self-hosted 러너 로그 파일 : 로그파일은 러너 디렉토리 내부에 별도의 `_diag` 디렉토리에 생성되며, 러너 어플리케이션이 시작될 때 마다 새로운 로그가 생성됩니다. 
     - __Runner_파일 : Self-hosted 러너의 어플리케이션과 동작에 대한 로그파일 
     - __Worker_파일 : 각 job의 실행에 대한 로그 파일 
   
   - 리눅스 기반의 self-hosted 러너에서 service로 application을 실행할 때는 `journalctl`을 사용해 실시간 활동을 모니터링할 수 있습니다. 
  
   - self-hosted 러너에서의 컨테이너
     - 도커 설치 확인 : `sudo systemctl is-active docker.service`
     - 만약 job이 아래와 같은 에러메세지로 실패 한다면, 도커 permission 확인 
     
     ```
      dial unix /var/run/docker.sock: connect: permission denied
     ```
      - self-hosted 러너의 서비스 account가 도커 서비스를 사용할 수 있는 권한 확인
    
     ```
     $ sudo systemctl show -p User actions.runner.octo-org-octo-repo.runner01.service
     User=runner-user
     ```
  
   - [Self-hosted 러너 삭제](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/removing-self-hosted-runners)
  
 </p>
 </details>


<br/>


# 8. 기타

 <details><summary> </summary>
 <p>

   ### 1. Artifacts와 로그 저장 정책
    
   - artifact와 로그의 저장 기간은 [저장소별](https://docs.github.com/en/enterprise-server@3.1/github/administering-a-repository/configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-repository), [조직별](https://docs.github.com/en/enterprise-server@3.1/organizations/managing-organization-settings/configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-organization), 그리고 [enterprise에](https://docs.github.com/en/enterprise-server@3.1/github/setting-up-and-managing-your-enterprise/configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-enterprise-account) 대해 설정할 수 있습니다. 
    
   - default로 90일간 저장됩니다. 
  
   - Public저장소에 대해서 저장 기간은 1~90일 범위에서 설정할 수 있습니다. 
  
   - Private, Internal, GitHub Enterprise 저장소들은 1~400일 범위에서 설정할 수 있습니다.
  
   - 저장기간 변경시, 새로운 artifact와 로그들에 대해서만 적용되며, 이전에 생성된 artifact와 로그들에는 소급적용되지 않습니다. 
  
   ### 2. Scheduled workflow들의 불필요한 실행 방지
  
   - 불필요한 workflow의 실행을 방지하기 위해, scheduled workflow들은 자동으로 disable될 수 있습니다. 
  
   - Public 저장소가 fork되었을 때, scheduled workflow들은 자동으로 disable되어 있습니다. 
  
   - Public 저장소들에 대해서, 60일간 아무런 repository activity가 없을 때, scheduled workflow들은 자동으로 disable 됩니다. 
   
 </p>
 </details>

** 본 문서는 GitHub Enterprise Server 버젼 3.1을 기준으로 작성되었습니다. 
