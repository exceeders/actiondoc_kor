# [Workflow 파일 템플릿 : 조직내 워크플로우 공유](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/sharing-workflows-with-your-organization)

### 1. 조직내 `.github` 이름을 가진 저장소를 생성하고 여기에 워크플로우를 조직내에서 공유할 수 있습니다. 
   
  - Public/Private 저장소 모두 가능

### 2. 템플릿 생성 방법 🎛️

  - 조직내 `.github` 저장소 생성
  
  - `workflow-template` 이라는 디렉토리 생성하고, 이 디렉토리에 워크플로우 파일과 metadata파일 생성
      - 워크플로우를 사용할 각 저장소의 default branch는 `$default-branch`로 참조
      
  - metadata 파일 생성
      - metadata파일은 `.properties.json` 확장자
      - metadata파일 이름은 workflow 파일이름과 동일해야 함
      - metadata파일 구조
      
       ```
       {
        "name": "Octo Organization Workflow",
        "description": "Octo Organization CI workflow template.",
        "iconName": "example-icon",
        "categories": [
            "Go"
        ],
        "filePatterns": [
            "package.json$",
            "^Dockerfile",
            ".*\\.md$"
        ]
       }
       ```
   
   
       - `name` : **Required**
       - `description` : **Required**
       - `iconName` : **Required**
       - `categories` : Optional
       - `filePatterns` : Optional
 
 ### 3. 사용
 
   - Organization내 저장소에서 'Action' 탭
   - 'New workflow' 메뉴
   - Organization의 템플릿으로 공유된 워크플로우는 'Workflows created by _organization name_' 섹션에 위치해 있음
    
   ![image](https://user-images.githubusercontent.com/40287191/122319178-3a2e0480-cf5b-11eb-8a7a-2f913e363b62.png)

   
