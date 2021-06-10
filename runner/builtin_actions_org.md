# GHES를 설치하면 'actions' 라는 조직이 자동으로 생성되어 있습니다.

 - GHES 인스턴스가 설치되면 자동으로 내부에 'actions'라는 Org가 생성되어 있고, 이 Org에 다양한 Action들이 포함되어 있습니다. 이 Actions들은 https://github.com/actions 에 있는 Actions들이 GitHub Enterprise 설치 버젼에 포함된 것입니다(해당버젼이 빌드될 때의 특정시점). 

   ![image](https://user-images.githubusercontent.com/40287191/121540180-3a9d3b80-ca41-11eb-9516-2b81dd8b5751.png)

 
 
 - 워크 플로우에서 사용할 Action을 선언할 때 `uses: actions/setup-node@v1` 과 같이 선언하면 기본적으로 빌트인된 'actions' Org에 있는 Actions들을 사용하게 됩니다.
 
 - 이와 같이, Actions는 먼저 GHES내부에 있는 '조직명/저장소명'을 가진 Actions를 먼저 찾고, 만약 없다면, 설정된 GitHub Connect를 통해 외부의 Actions를 찾습니다. 
 
  ![image](https://user-images.githubusercontent.com/40287191/121542232-f14deb80-ca42-11eb-9c1d-c0252d4749d5.png)

 
 - GHES 인스턴스에 포함된 Actions들은 https://github.com/actions 의 내용이 업데이트 되어도 자동으로 동기화 되지 않습니다. 
 
 - 이 Actions들에 대한 최신 업데이트된 내용을 사용하기 위해서는 아래와 같이 **두가지 방법**이 있습니다. 
 
    - GHES내부에 빌트인된 'actions' 조직의 저장소를 삭제 
    
       - 'actions' 조직의 저장소를 삭제하기 위해서는 'actions' 조직의 owner가 되어야 하며, 'actions' 조직의 owner는 default로 `actions_admin` 이라는 기본 owner가 있으나, [site admin이 추가로 owner를 지정](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/managing-access-to-actions-from-githubcom/manually-syncing-actions-from-githubcom#prerequisitesadmin)할 수 있습니다. 
   
    - 또는 아래 3.항에서 설명되는 `Actions-sync tool`을 사용
 
