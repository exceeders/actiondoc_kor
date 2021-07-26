# [Workflow 실행관리](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs)

1. [Visualization graph](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/using-the-visualization-graph) : 저장소 Actions 탭에서, 왼편의 사이드바에서 보고자 할 워크플로우 클릭 > 오른쪽의 워크플로우 run 리스트 중 선택
   
    <img src="https://user-images.githubusercontent.com/40287191/123577235-658fd980-d80e-11eb-8a9e-bf144fe94993.png" width="600" height="400">

<br/>

2. [워크플로우 run log](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/using-workflow-run-logs) : 저장소 Actions 탭에서, 왼편의 사이드바에서 보고자 할 워크플로우 클릭 > 오른쪽의 워크플로우 run 리스트 중 선택 > 왼편 하단의 'Jobs'에서 보고자 할 job 선택
  
    <img src="https://user-images.githubusercontent.com/40287191/123577493-e64ed580-d80e-11eb-98be-a4d9c86399da.png" width="550" height="200">


    - Search logs : 로그 화면 우측 상단에 Search 박스
     
     <img src="https://user-images.githubusercontent.com/40287191/123583693-05ebfb00-d81b-11eb-941e-a3f69cd5630d.png" width="760" height="120">
  
    - Downloading logs : 로그 화면 우측 상단의 톱니바퀴 아이콘( ![image](https://user-images.githubusercontent.com/40287191/123583858-4b102d00-d81b-11eb-8319-bbd1005c02fa.png)) 클릭 후, 'Download log archive' 메뉴
  
     <img src="https://user-images.githubusercontent.com/40287191/123583900-654a0b00-d81b-11eb-8909-c323bc840e50.png" width="700" height="200">

  <br/>
  
3. [워크플로우 수동으로 run](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/manually-running-a-workflow)

   - 워크 플로우의 트리거 조건이 `workflow_dispatch`로 설정되어 있을 때, Actions 탭 > 왼편 사이드 바에서 워크플로우 선택 > 오른편 'Run workflows'
   
     <img src="https://user-images.githubusercontent.com/40287191/123585501-50bb4200-d81e-11eb-9699-ad72382c01cf.png" width="650" height="300"> 
    
     <img src="https://user-images.githubusercontent.com/40287191/123585587-6fb9d400-d81e-11eb-9762-63f573fda588.png" width="250" height="200">

<br/>
  
4. [워크플로우 re-run](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/re-running-a-workflow)

   - Action 탭 > 왼편 사이드바에서 워크플로우 클릭 > 오른편의 워크플로우 run 리스트에서 재실행하고자 하는 것 클릭 > 오른쪽 상단의 'Re-run jobs' 또는 'Re-run all jobs' 메뉴
   
     <img src="https://user-images.githubusercontent.com/40287191/123586553-dbe90780-d81f-11eb-8ba2-2fffbc3eabd7.png" width="650" height="150">
  
<br/>
  
5. [워크플로우 실행 취소](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/canceling-a-workflow)

   - 실행중인 워크 플로우 취소 : Action 탭 > 왼편 사이드바에서 워크플로우 클릭 > 오른편의 워크플로우 run 리스트에서 `queued` 또는 `in progress`클릭 > 'Cancel workflow' 

 
     <img src="https://user-images.githubusercontent.com/40287191/123586927-6e89a680-d820-11eb-94b4-f8f37fddb3f7.png" width="600" height="200">
    
     <img src="https://user-images.githubusercontent.com/40287191/123586941-777a7800-d820-11eb-8403-f6ec35f3ac19.png" width="600" height="150">

<br/>
  
6. [워크플로우 활성화/비활성화](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/disabling-and-enabling-a-workflow)

   - 워크 플로우를 GitHub UI, Rest API, GitHub CLI를 통해 활성화, 비활성화 할 수 있습니다. 
   - 비활성화된 워크플로우는 워크플로우 파일내 트리거 조건에 의해 실행되지 않습니다 (워크플로우 파일 삭제 불필요)
   - Action 탭 > 왼편 사이드바에서 워크플로우 클릭 > 오른편의 '...' 클릭 > 'Disable workflow'
   
     ![image](https://user-images.githubusercontent.com/40287191/123589529-51ef6d80-d824-11eb-8b05-f3304190f085.png)
     ![image](https://user-images.githubusercontent.com/40287191/123589572-63387a00-d824-11eb-8d6d-54abbd572616.png)

   - 비활성화된 워크플로우는 ![image](https://user-images.githubusercontent.com/40287191/123589645-7f3c1b80-d824-11eb-9b38-ba9236274ee6.png) 표시
    
     ![image](https://user-images.githubusercontent.com/40287191/123589682-89f6b080-d824-11eb-95b2-a2b8658dcbd6.png)
     
   - 다시 활성화하기 위해서는 비활성화된 워크플로우에서 'enable workflow' 메뉴
     ![image](https://user-images.githubusercontent.com/40287191/123590117-2d47c580-d825-11eb-89d5-b005b7ee9dd6.png)
   
<br/>
  
7. [워크플로우 run 삭제](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/deleting-a-workflow-run)

   - Action 탭 > 왼편 사이드바에서 워크플로우 클릭 > 오른편의 워크플로우 run 리스트에서 삭제하고자 하는 것 클릭
     <img src="https://user-images.githubusercontent.com/40287191/123590278-66803580-d825-11eb-8e0b-559e01b806b2.png" width="750" height="150">
   
<br/>
  
8. 워크플로우 artifact [다운로드](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/downloading-workflow-artifacts), [삭제](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/removing-workflow-artifacts)

   - Action 탭 > 왼편 사이드바에서 워크플로우 클릭 > 오른편의 워크플로우 run 리스트에서 실행했던 run 선택 > 하단의 'Artifact' 클릭
    <img src="https://user-images.githubusercontent.com/40287191/123590564-c37beb80-d825-11eb-9579-8bb9ef6da3de.png" width="600" height="150">
   
<br/>
  
9. [디버그 로깅 활성화](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/enabling-debug-logging)

   - 워크 플로우의 트러블 슈팅을 위한 추가적인 상세 디버그 활성화할 수 있습니다.
   - 이를 위해, 워크플로우가 있는 저장소에 'secret'을 생성해야 하며, 저장소의 owner 혹은 organization의 admin 권한이 필요합니다. 
   - [Runner diagnostic 로깅 활성화](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/enabling-debug-logging#enabling-runner-diagnostic-logging)
     - 'runner process log' : 러너가 job을 실행하기 위해 필요한 설정에 관련된 로그 
     - 'worker process log' : job 실행에 관련된 로그
     - 워크플로우가 있는 저장소의 secret 메뉴에 `ACTIONS_RUNNER_DEBUG` 추가 (값은 `true`)
     - Runner diagnostic 로그를 다운로드 하기 위해서는 위 2항에서 설명된 log archive 다운로드. Runner diagnostic 로그는 `runner-diagnostic-logs` 폴더내에 위치
     
   - [Step 디버깅 로깅 활성화](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/enabling-debug-logging#enabling-step-debug-logging)
     - Job 실행로그에 상세 내용이 추가됨
     - 워크플로우가 있는 저장소의 secret 메뉴에 'ACTIONS_STEP_DEBUG` 추가 (값은 `true`)
     - 확인은 step log에서 확인 

<br/>
  
10. [배포 리뷰](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/reviewing-deployments) 

    - 저장소의 'environment' 과 그에 대한 보호룰이 지정된 경우
      <img src="https://user-images.githubusercontent.com/40287191/123595247-a64a1b80-d82b-11eb-8b7a-bf43f439accb.png"  width="700" height="250">


    - 최대 6명까지의 'Required Reviewers' 지정가능
    - Wait Timer: Job이 처음 트리거되고, 설정된 시간(분) 동안 지연 (0~43,200(30일))
    - 리뷰어로 지정된 사람은, 워크플로우에서 아래와 같이 작업을 승인 또는 거부
      ![image](https://user-images.githubusercontent.com/40287191/123595984-8c5d0880-d82c-11eb-91ef-960ea8a97eab.png)
      <img src="https://user-images.githubusercontent.com/40287191/123595998-8ff08f80-d82c-11eb-8281-07f759146b48.png" width="400" height="300">


<br/>
  

11. [Status 배지 추가](https://docs.github.com/en/enterprise-server@3.1/actions/managing-workflow-runs/adding-a-workflow-status-badge)
 
    - 워크플로우의 성공 혹은 실패를 특정 파일 (`README.md`등)에 추가
     ![image](https://user-images.githubusercontent.com/40287191/123596746-83206b80-d82d-11eb-86c0-79dead486c9f.png)
     
    - 워크플로우 메뉴에서 오른편의 "..." 클릭 > Create Status Badge 
 
     <img src="https://user-images.githubusercontent.com/40287191/123597537-6cc6df80-d82e-11eb-88c4-af9f70c9b282.png" width="800" height="180">
    
     <br/>
         
      <img src="https://user-images.githubusercontent.com/40287191/123597430-4bfe8a00-d82e-11eb-93c3-e795be0ff1fc.png" width="370" height="300">


  

