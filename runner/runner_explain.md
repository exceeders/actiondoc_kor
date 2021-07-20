# Actions Runner
- GitHub Actions의 Runner는 GitHub-hosted runner와 Self-hosted runner 두 가지가 있습니다. 
- GitHub-hosted runner는 GitHub에서 Hosting하여 서비스 하는 러너입니다. 
- Self-hosted runner는 Enterprise에서 직접 Compute자원을 준비하여 실행하는 러너 입니다.
- 현재 GHES 3.0/3.1에서는 **Self-hosted Runner만 지원됩니다.**

<img src="https://user-images.githubusercontent.com/40287191/121185766-5f5aad00-c8a1-11eb-9af2-57ef2ec38254.png">  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <img src="https://user-images.githubusercontent.com/40287191/121161933-6b864080-c888-11eb-87a4-eae91b4a7210.png">  


# 1. GitHub-hosted Runner vs. Self-hosted Runner

<details><summary> </summary>
<p>
 
<table>
    <thead>
        <tr>
            <th>GitHub-hosted runner </th>
            <th>Self-hosted runner </th>
        </tr>
    </thead>
    <tbody>
        <tr>
         <td> GitHub에 의해 호스팅 되는 Runner </td>
         <td> 사용자가 직접 on-prem에 호스팅하는 Runner  </td>
        </tr>
        <tr>
         <td> Linux, Windows, MacOS - virtual machine, container </td>
         <td> Linux, Windows, MacOS <br>  - physical, virtual, container, on-premises, or in a cloud </td>
        </tr>
        <tr>
         <td> Virtual machine에 직접 동작 또는 Docker 컨테이너로 워크 플로우 동작 가능 </td>
         <td> GitHub Enterprise와 연결을 위한 "GitHub Actions runner 어플리케이션" 설치 후 실행 해야 함 </td>
        </tr>
        <tr>
          <td>  Runner Hardware resources : Linux/Window <br> - 2core CPU / 7GB Mem / 14GB SSD disk space </td>
          <td> 사용자가 구성하는 하드웨어 리소스; 필요에 따라 맞춤화된 하드웨어 구성가능 </td>
        </tr>
        <tr>
         <td>  Runner Hardware resources : MacOS <br> - 3core CPU / 14GB Mem / 14GB SSD disk space </td>
         <td> 사용자가 구성하는 하드웨어 리소스; 필요에 따라 맞춤화된 하드웨어 구성가능 </td>
        </tr>
        <tr>
          <td>  OS별 사전 설치된 소프트웨어/패키지 (하단 별도설명) </td>
          <td> 사용자가 필요한 소프트웨어/패키지등을 직접설치 </td>
        </tr>
    </tbody>
</table>


  </p>
  </details> 

<br/>
  
# 2. GitHub-hosted Runner 
 
 <details><summary> </summary>
 <p>
 
  1. GitHub-hosted Runner는 어디서 호스팅 되나요? ☁️
     - [Windows, Linux 러너](https://docs.github.com/en/enterprise-server@3.1/actions/using-github-hosted-runners/about-github-hosted-runners#cloud-hosts-for-github-hosted-runners) : Azure - `Standard_DS2_v2 virtual machine`
     - [Mac 러너](https://docs.github.com/en/enterprise-server@3.1/actions/using-github-hosted-runners/about-github-hosted-runners#cloud-hosts-for-github-hosted-runners) : GitHub 자체 macOS Cloud
   
  <br/>
  
  2. [GitHub-hosted Runner 과금](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions#about-billing-for-github-actions)
     - GitHub Enterprise는 기본적으로 **월별 50,000분/50GB Storage**(Actions/Packages용도)가 포함되어 있습니다. 
   
     - 초과되는 사용량에 대해서 아래와 같이 분당 ⏰ 과금됩니다. 
     <img src="https://user-images.githubusercontent.com/40287191/121186647-48688a80-c8a2-11eb-9874-45fd40619203.png" width="650" height="150">

     - 초과되는 사용량은 Admin page에서 확인 가능 ([Organization](https://docs.github.com/en/billing/managing-billing-for-github-actions/viewing-your-github-actions-usage#viewing-github-actions-usage-for-your-organization), [Enterprise](https://docs.github.com/en/billing/managing-billing-for-github-actions/viewing-your-github-actions-usage#viewing-github-actions-usage-for-your-enterprise-account))하며, _월별 최대사용한도_ 📊를 미리 정해 놓을 수 있습니다. 
       - [사용량 계산 예시](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions#calculating-minute-and-storage-spending)
       - 월별사용한도 설정 : [Organization](https://docs.github.com/en/github/setting-up-and-managing-your-enterprise/setting-policies-for-organizations-in-your-enterprise-account/enforcing-github-actions-policies-in-your-enterprise-account#setting-the-permissions-of-the-github_token-for-your-enterprise), [Enterprise](https://docs.github.com/en/billing/managing-billing-for-github-actions/managing-your-spending-limit-for-github-actions#managing-the-spending-limit-for-github-actions-for-your-enterprise-account)
   
       <img src="https://user-images.githubusercontent.com/40287191/121212009-eadf3880-c8b7-11eb-8742-84f2ec094047.png" width="700" height="250">

     - 초과 사용량에 대해서만 월별 결재, 또는 사전에 일정량을 Pre-paid로 구매 가능합니다. 
  
     - Microsoft Enterprise Agreement로 GitHub Enterprise를 구매했다면, [Azure Subscription ID를 GitHub Enterprise Account와 연결](https://docs.github.com/en/github/setting-up-and-managing-your-enterprise/connecting-an-azure-subscription-to-your-enterprise)하여 초과 사용량에 대한 지불을 포함시킬 수 있습니다. 
 
   <br/>
  
  3. GitHub-hosted Runner 지원 OS 
     
     - 아래의 표와 같이 [지원되는 OS](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources)가 있습니다. 
    
      <img src="https://user-images.githubusercontent.com/40287191/121195196-5ae6c200-c8aa-11eb-8bcb-5648f677d4e6.png" width="450" height="250">


   <br/>
  
  4. GitHub-hosted Runner 사전 설치된 소프트웨어
   
     - [OS별 사전 설치된 소프트웨어 확인](https://docs.github.com/en/enterprise-server@3.1/actions/using-github-hosted-runners/about-github-hosted-runners#preinstalled-software)
    
     - 예: Ubuntu 20.04 LTS 
  
   <img src="https://user-images.githubusercontent.com/40287191/121188796-6b943980-c8a4-11eb-8cd7-9f935c4f033d.png" width="250" height="600"> &nbsp; &nbsp; &nbsp;  &nbsp; ![image](https://user-images.githubusercontent.com/40287191/121188890-81a1fa00-c8a4-11eb-9dd6-0f681770c4cc.png) &nbsp; &nbsp; &nbsp; &nbsp; !<img src="https://user-images.githubusercontent.com/40287191/121189004-a007f580-c8a4-11eb-8c1b-25297a8a760a.png" width="250" height="600">

   <br/>
  
  5. IP address of GitHub-hosted runner
  
     - GitHub-hosted runner를 위해 Actions가 사용하는 IP address range는 [GitHub REST API](https://docs.github.com/en/enterprise-server@3.1/rest/reference/meta#get-github-meta-information)로 확인 가능 : https://api.github.com/meta

     * `Note`: If you use an `IP address allow list` for your GitHub organization or enterprise account, you cannot use GitHub-hosted runners and must instead use self-hosted runners. 
   
  <br/>
  
  6. 사용량 최대치 limit
  
     - GitHub-hosted runner를 사용할 때 아래와 같은 [사용량의 한계](https://docs.github.com/en/actions/reference/usage-limits-billing-and-administration#usage-limits)가 정해져 있습니다. (이 내용은 변경될 수 있습니다)

        항목 | 최대치
        --|--
        Job Execution time | 6시간
        Workflow run time | 72시간
        API requests | 1000 request /1시간 (한 저장소내 전체 Actions에 대해)
        Concurrent jobs | 180개, MacOS는 50개
        Job matrix | 256 job /워크플로우
        Workflow run queue | 저장소 당 10초에 최대 100개 워크 플로우

  
 </p>
  </details> 


<br/>
  
# 3. Self-hosted Runner

 <details><summary> </summary>
 <p>
  
  1. Self-hosted Runner는 별도 과금이 없습니다. 
  
  2. Self-hosted Runner 어플리케이션
  
     - Self-hosted Runner를 GitHub Enterprise와 연결해 주는 어플리케이션 입니다. 
     - 오픈소스이며, https://github.com/actions/runner 에서 보실 수 있습니다. 
     - Self-hosted Runner 추가시, 화면에 보여지는 가이드의 순서데로 설치 진행 하면 됩니다. (아래 5.Self-hosted Runner 추가)
    
  3. [지원되는 OS및 Architecture](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/about-self-hosted-runners#supported-architectures-and-operating-systems-for-self-hosted-runners)
    
      Linux | Windows | MacOS | Architectures
      --|--|--|--
      Red Hat Enterprise Linux 7 or later<br>CentOS 7 or later<br>Oracle Linux 7<br>Fedora 29 or later<br>Debian 9 or later<br>Ubuntu 16.04 or later<br>Linux Mint 18 or later<br>openSUSE 15 or later<br>SUSE Enterprise Linux (SLES) 12 SP2 or later | Windows 7 64-bit<br>Windows 8.1 64-bit<br>Windows 10 64-bit<br>Windows Server 2012 R2 64-bit<br>Windows Server 2016 64-bit<br>Windows Server 2019 64-bit |macOS 10.13 (High Sierra) or later |x64 - Linux, macOS, Windows.<br>ARM64 - Linux only.<br>ARM32 - Linux only.  
      
    
  <br/>
  
  4. [Self-hosted Runner 계위](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/about-self-hosted-runners#about-self-hosted-runners)
  
     - Self-hosted Runner는 아래와 같이 크게 3가지로 구성하여 사용할 수 있습니다. 
      
       Enterprise 레벨 러너 | GitHub Enterprise 전체에서 사용가능 (개인계정의 저장소 제외)
       --|--
       **Organization 레벨 러너** | **Organization에 소속된 모든 저장소에서 사용 가능**
       **Repository 레벨 러너** | **해당 저장소에서만 사용가능**
  
      ![image](https://user-images.githubusercontent.com/40287191/121205776-e7957e00-c8b2-11eb-9866-d5fcee9c885c.png)
   
  <br/>
  
  5. [Self-hosted Runner 추가](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/adding-self-hosted-runners)
  
      - 저장소 settings메뉴 > Actions 
      - Organizations settings메뉴 > Actions
      - Enterprise settings > Policies > Actions 
      - "Self-hosted runners"에서 "Add runner"
  
       ![image](https://user-images.githubusercontent.com/40287191/121208239-e1080600-c8b4-11eb-8c65-463a9f8b0a6b.png)
      - Add runner 화면에 나오는 순서데로, 디렉토리 생성 후, 생성된 디렉토리내에서 self-hosted runner 어플리케이션을 다운받아 설치 후 연결
  
  <br/>
  
  6. [Self-hosted Runner as a service](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/configuring-the-self-hosted-runner-application-as-a-service)
  
      - `systemd`을 사용하는 Linux 시스템에서 self-hosted runner 어플리케이션에 포함된 `svc.sh`스크립트를 실행
      - Runner 어플리케이션이 실행중이면 실행을 종료하고, `svc.sh` install
        
         ```
         sudo ./svc.sh install
         ```
      
       - 서비스 시작
  
         ```
         sudo ./svc.sh start
         ```
  
       - 서비스 상태 확인
     
         ```
         sudo ./svc.sh status
         ```
      
       - 서비스 종료
     
         ```
         sudo ./svc.sh stop
         ```
  
    
  <br/>
  
  7. [러너를 그룹으로 묶어서 사용하기](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups)
  
      - 여러개의 Self-hosted 러너들을 그룹으로 묶어서 Organization과 Enterprise 레벨에서 한꺼번에 여러 Self-hosted 러너들에 대한 접근 제어를 위해 사용
      - 예를들어, Organization에 러너 그룹을 만들고 특정 저장소들만 러너그룹에 할당하여 사용
      - 또는, Enterprise레벨에 러너 그룹을 만들고 특정 Organization들만 러너그룹에 할당하여 사용
      - 러너 그룹 생성 : [Organization](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups#creating-a-self-hosted-runner-group-for-an-organization), [Enterprise](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups#creating-a-self-hosted-runner-group-for-an-enterprise) 
  
          <img src="https://user-images.githubusercontent.com/40287191/121213577-537ae500-c8b9-11eb-8678-a7193b5329a2.png" width="400" height="300">

  <br/>
  
  8. [러너에 Label 붙여 사용하기](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/using-labels-with-self-hosted-runners)
    
     - 러너를 생성할 때, 혹은 생성된 러너에 대해 아래와 같이 UI메뉴에서 Label을 추가/수정 할 수 있습니다. 
     ![image](https://user-images.githubusercontent.com/40287191/121207836-8e2e4e80-c8b4-11eb-9d87-fef26c1f8336.png)

    
  <br/>
  
  9. [Self-hosted Runner와 GHES사이의 Communication](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/about-self-hosted-runners#communication-between-self-hosted-runners-and-github-enterprise-server)
     - HTTPS 프로토콜을 통한 통신
     - Self Hosted Runner는 Jobs에 대한 정보를 주고받기 위해 GitHub과 통신
     - Self Hosted Runner에 “GitHub Action Runner Application”이 설치되어 실행되어야 GitHub으로 부터 Action의 Job들을 수신하여 실행 할 수 있음
    
    
  <br/>
  
  10. [Self-hosted Runner의 인터넷 연결](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners#communication-between-self-hosted-runners-and-github)
      - Self-hosted Runner는 아래와 같은 용도로 인터넷 연결이 필요합니다. 
        - Self-hosted Runner application update 
        - GitHub.com의 Actions download
        - Toolcache (setup-node, setup-python, setup-java,,) Action들의 패키지 다운로드
  
      - Self-hosted Runner가 인터넷 연결이 불가할 시, 인터넷이 가능한 곳에서 다운로드하여 [수동으로 사용할 수 있는 방법](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/setting-up-the-tool-cache-on-self-hosted-runners-without-internet-access)을 제공합니다.
  
     
  <br/> 
  
  
  11. [Self-hosted Runner 어플리케이션의 업그레이드](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners#about-self-hosted-runners)
     
      - Self-hosted Runner 어플리케이션은 새로운 버젼이 출시되면, Job이 러너에 할당 될 때 자동으로 업데이트 합니다.
      
      - Job이 할당되지 않더라도 새로운 버젼 출시 후 1주일 이내에 자동으로 업데이트 됩니다. 
  
  <br/> 
  
 
  12. [Self-hosted Runner security with Public repositories](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners/about-self-hosted-runners#self-hosted-runner-security-with-public-repositories)
  
      - 보안을 위해 Public repository들에서는 Self Hosted Runner의 사용이 권장되지 않습니다. 

      - 처음 Org/Enterprise 레벨에 Self-hosted Runner를 추가하면 기본으로 생성된 'default' 러너그룹에 추가되는데, 이 러너그룹은 'public' 저장소를 포함하지 않도록 설정되어져 있습니다. 

      - Public저장소에 대해서도 사용하려면, 아래 그림과 같이 'public' 저장소를 포함하도록 하는 옵션을 체크하시면 됩니다. 

        <img src="https://user-images.githubusercontent.com/40287191/121277614-f3f9f500-c90b-11eb-94c7-d36bc4cc2f70.png" width="600" height="150"> &nbsp; &nbsp; 

        <img src="https://user-images.githubusercontent.com/40287191/121277586-dfb5f800-c90b-11eb-956a-9c6feb1a36cd.png" width="300" height="200">

   <br/>
  
   13. Self-hosted Runner는 30일 이상 GitHub Action과 연결되지 않으면 [자동으로 삭제됩니다](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners#about-self-hosted-runners). 
  
  <br/>
  
   14. [사용량 최대치 limit](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners#usage-limits)
  
        항목 | 최대치
        --|--
        Workflow run time | 72시간
        API requests | 1000 request /1시간 (한 저정소내 전체 Actions에 대해)
        Job matrix | 256 job /워크플로우
        Workflow run queue | 저장소 당 10초에 최대 100개 워크 플로우
        Job queue time | 각 job은 최대 24시간 동안 큐에 대기
  
        * 표의 값들은 변경될 수 있습니다. 
  
  </p>
  </details> 

[🔙](https://github.com/exceeders/Actions_gettingStarted/blob/main/README.md#2-minio-nas-gateway)
