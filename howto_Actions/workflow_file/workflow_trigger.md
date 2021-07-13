# [Workflow Trigger Events](https://docs.github.com/en/enterprise-server@3.1/actions/reference/events-that-trigger-workflows)

### 워크플로우는 GitHub Enterprise의 특정 이벤트로, 스케쥴한 시간에, 수동으로, 또는 외부에서의 이벤트에 의해 트리거 될 수 있습니다. 

### [1. Configuring workflow events](https://docs.github.com/en/enterprise-server@3.1/actions/reference/events-that-trigger-workflows#configuring-workflow-events)

 
 <details><summary> </summary>
 <p>
   
   
   ```
   on : push
   ```
   
   
   ```
   on : [push, pull_request]
   ```
   
  
   ```
   on:
    # Trigger the workflow on push or pull request,
    # but only for the main branch
    push:
      branches:
        - main
    pull_request:
      branches:
        - main
    # Also trigger on page_build, as well as release created events
    page_build:
    release:
      types: # This configuration does not affect the page_build event above
        - created
   ```
   
 </p>
 </details>

<br/>
 


### [2. Scheduled events](https://docs.github.com/en/enterprise-server@3.1/actions/reference/events-that-trigger-workflows#scheduled-events)

 
 <details><summary> </summary>
 <p>
   
   
   ```
    on:
     schedule:
       # * is a special character in YAML so you have to quote this string
       - cron:  '30 5,17 * * *'
   
   ```
   
 </p>
 </details>

<br/>
 

### [3. Manual events](https://docs.github.com/en/enterprise-server@3.1/actions/reference/events-that-trigger-workflows#manual-events)

 
 <details><summary> </summary>
 <p>
   
   - `workflow_dispatch` : 수동으로 트리거
   
    
    on: workflow_dispatch
    
   
   
   - `repository_dispatch` : 외부에서 GitHub Enterprise의 API로 POST 리퀘스트하여 트리거 (`event_type`)
   
    
    on:
      repository_dispatch:
        types: [opened, deleted]
    
  
   
 </p>
 </details>

<br/>
 


### [4. Webhook events](https://docs.github.com/en/enterprise-server@3.1/actions/reference/events-that-trigger-workflows#webhook-events)

 
 <details><summary> </summary>
 <p>
   
   - GitHub Enterprise에서 발생하는 웹훅이벤트에 의해 트리거
   
   - 이벤트에 따라 여러가지 다양한 activity type이 있을 수 있습니다. 
   
   - 모든 웹훅 이벤트가 워크플로우를 트리거하지는 않습니다. (아래 표와, 위 제목에 링크된 Help 페이지에 설명 )
   
     Webhook event payload | Activity types
     --|--
     `check_run`| - `created`<br> - `requested`<br> - `completed`<br>
     `check_suite`| - `completed`<br> - `requested`<br> - `completed`<br>
     `create`| |
     `delete`| |
     `deployment`| |
     `deployment_status`| |
     `fork`| |
     `gollum`| |
     `issue_comment`| - `created`<br> - `edited`<br> - `deleted`<br>
     `issues`| - `opened`<br> - `edited`<br> - `deleted`<br> - `transferred`<br> - `pinned`<br> - `unpinned`<br> - `closed`<br> - `reopened`<br> - `assigned`<br> - `unassigned`<br> - `labeled`<br> - `unlabeled`<br> - `locked`<br> - `unlocked`<br> - `milestoned`<br> - `demilestoned`<br>
     `label`| - `created`<br> - `edited`<br> - `deleted`<br>
     `milestone`| - `created`<br> - `closed`<br> - `opened`<br> - `edited`<br> - `deleted`<br>
     `page_build`| |
     `project`| - `created`<br> - `updated`<br> - `closed`<br> - `reopened`<br> - `edited`<br> - `deleted`<br>
     `project_card`| - `created`<br> - `moved`<br> - `converted`<br> - `edited`<br> - `deleted`<br>
     `project_column`| - `created`<br> - `updated`<br> - `moved`<br> - `deleted`<br>
     `public`| |
     `pull_request`| - `assigned`<br> - `unassigned`<br> - `labeled`<br> - `unlabeled`<br> - `opened`<br> - `edited`<br> - `closed`<br> - `reopened`<br> - `synchronized`<br> - `ready_for_review`<br> - `locked`<br> - `unlocked`<br> - `review_requested`<br> - `review_request_removed`<br>
     `pull_request_review`| - `submitted`<br> - `edited`<br> - `dismissed`<br>
     `pull_request_review_comment`| - `created`<br> - `edited`<br> - `deleted`<br>
     `pull_request_target`| - `assigned`<br> - `unassigned`<br> - `labeled`<br> - `unlabeled`<br> - `opened`<br> - `edited`<br> - `closed`<br> - `reopened`<br> - `synchronized`<br> - `ready_for_review`<br> - `locked`<br> - `unlocked`<br> - `review_requested`<br> - `review_request_removed`<br>
     `push`| |
     `registry_package`| - `published`<br> - `updated`<br> |
     `release`| - `published`<br> - `unpublished`<br> - `created`<br> - `edited`<br> - `deleted`<br> - `prereleased`<br> - `released`<br>
     `status`| |
     `watch`| |
     `workflow_run`| - `completed`<br> - `requested`<br> 
   
   
     
 - example : 풀리퀘스트에 의한 트리거   
   
   ```
    on:
     pull_request:
      types: [assigned, opened, synchronize, reopened]
   ```
  
 - example : workflow_run에 의한 트리거  
  
   ``` 
   on:
     workflow_run:
       workflows: ["Build"]
       types: [completed]

    jobs:
      on-success:
        runs-on: ubuntu-latest
        if: ${{ github.event.workflow_run.conclusion == 'success' }}
        steps:
          ...
      on-failure:
        runs-on: ubuntu-latest
        if: ${{ github.event.workflow_run.conclusion == 'failure' }}
        steps:
          ...
   
    ```
  
  
 </p>
 </details>

<br/>
 
