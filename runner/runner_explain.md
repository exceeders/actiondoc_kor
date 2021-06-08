# Actions Runner
- GitHub Actions의 Runner는 GitHub-hosted runner와 Self-hosted runner 두 가지가 있습니다. 
- GitHub-hosted runner는 GitHub에서 Hosting하여 서비스 하는 러너입니다. 
- Self-hosted runner는 Enterprise에서 직접 Compute자원을 준비하여 실행하는 러너 입니다.
- GHES 3.0/3.1에서는 Self-hosted Runner만 지원됩니다. 

<img src="https://user-images.githubusercontent.com/40287191/121185766-5f5aad00-c8a1-11eb-9af2-57ef2ec38254.png">  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <img src="https://user-images.githubusercontent.com/40287191/121161933-6b864080-c888-11eb-87a4-eae91b4a7210.png">  


# GitHub-hosted Runner vs. Self-hosted Runner

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
         <td> Linux, Windows, MacOS - virtual machine </td>
         <td> Linux, Windows, MacOS <br>  - physical, virtual, container, on-premises, or in a cloud </td>
        </tr>
        <tr>
         <td> Virtual machine에 직접 동작 또는 Docker 컨테이터로 워크 플로우 동작 가능 </td>
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

# GitHub-hosted Runner 
 
 <details><summary> </summary>
 <p>
 
  1. GitHub-hosted Runner는 어디서 호스팅 되나요?
     - [Windows, Linux 러너](https://docs.github.com/en/enterprise-server@3.1/actions/using-github-hosted-runners/about-github-hosted-runners#cloud-hosts-for-github-hosted-runners) : Azure - `Standard_DS2_v2 virtual machine`
     - [Mac 러너](https://docs.github.com/en/enterprise-server@3.1/actions/using-github-hosted-runners/about-github-hosted-runners#cloud-hosts-for-github-hosted-runners) : GitHub 자체 macOS Cloud
   
  <br/>
  
  2. [GitHub-hosted Runner 과금](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions#about-billing-for-github-actions)
     - GitHub Enterprise는 기본적으로 **월별 50,000분/50GB Storage**가 포함되어 있습니다. 
   
     - 초과되는 사용량에 대해서 아래와 같이 분당 과금됩니다. 
     <img src="https://user-images.githubusercontent.com/40287191/121186647-48688a80-c8a2-11eb-9874-45fd40619203.png" width="550" height="150">

     - 초과되는 사용량은 Admin page에서 확인 가능하며, 월별 최대사용한도를 미리 정해 놓을 수 있습니다. 
       - [사용량 계산 예시](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions#calculating-minute-and-storage-spending)
   
     - 초과 사용량에 대해서만 월별 결재, 또는 사전에 일정량을 Pre-paid로 구매 가능합니다. 
  
     - Microsoft Enterprise Agreement로 GitHub Enterprise를 구매했다면, [Azure Subscription ID를 GitHub Enterprise Account와 연결](https://docs.github.com/en/github/setting-up-and-managing-your-enterprise/connecting-an-azure-subscription-to-your-enterprise)하여 초과 사용량에 대한 지불을 포함시킬 수 있습니다. 
 
   <br/>
  
  3. GitHub-hosted Runner 지원 OS 
     
     - 아래의 표와 같이 [지원되는 OS](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources)가 있습니다. 
    
      <img src="https://user-images.githubusercontent.com/40287191/121195196-5ae6c200-c8aa-11eb-8bcb-5648f677d4e6.png" width="500" height="250">


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
        API requests | 1000 request /1시간 (전체 Actions에 대해)
        Concurrent jobs | 180개, MacOS는 50개
        Job matrix | 256 job /워크플로우
        Workflow run queue | 저장소 당 10초에 최대 100개 워크 플로우

  
 </p>
  </details> 

# Self-hosted Runner

 <details><summary> </summary>
 <p>

  - 보안을 위해 Public repository들에서는 Self Hosted Runner의 사용이 권장되지 않음
  
  1. Self-hosted Runner 계위
  2. 러너 그룹
  3. 러너 Label
  4. Self-hosted Runner 추가
  5. Self-hosted Runner와 GHES사이의 Communication
     - HTTPS 프로토콜을 통한 통신
     - Self Hosted Runner는 Jobs에 대한 정보를 주고받기 위해 GitHub과 통신
     - Self Hosted Runner에 “GitHub Action Runner Application”이 설치되어 실행되어야 GitHub으로 부터 Action의 Job들을 수신하여 실행 할 수 있음
    
   
  </p>
  </details> 
