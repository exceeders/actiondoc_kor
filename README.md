
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

# GHES Actions/Packages 를 구성하기 위해 필요한 것? 🤔
<details><summary> </summary>
<p>
 
  ![image](https://user-images.githubusercontent.com/40287191/121131031-2f43e780-c86a-11eb-8bb0-e81b496cc3d1.png)
  1. GitHub Enterprise Server with version 3.0 or higher
    - 3.0 with Actions : Actions의 사용을 위해 하드웨어 리소스 증가 필요 [Link](https://docs.github.com/en/enterprise-server@3.1/admin/installation/setting-up-a-github-enterprise-server-instance/installing-github-enterprise-server-on-azure#hardware-considerations)
    - CPU/메모리 별 최대 throughput을 나타내는 Job 갯수 : [GitHub 내부 테스트 설명 Link](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/getting-started-with-github-actions-for-github-enterprise-server)
  
  2. [ Self-hosted Runner](https://docs.github.com/en/enterprise-server@3.1/actions/hosting-your-own-runners)
     - 실제 Job을 수행할 환경 (Linux/Window/Mac)
     - GitHub-hosted runner는 현재 GitHub Enterprise Cloud에서만 가능 (GitHub Enterprise Server는 향후지원예정)
  
  3. S3 compatible blob storage
     - Actions 로그 및 Packages 저장용
     - [Azure blob storage](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-azure-blob-storage), [AWS](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-amazon-s3-storage)
     - 순수 온프렘을 위해서는 [MinIO NAS Gateway](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enabling-github-actions-with-minio-gateway-for-nas-storage)



</p>
</details>

# GHES Actions/Packages 설정 🛠️

<details><summary> </summary>
<p>
  
  ### 1. Instance에서 Actions/Packages 활성화 및 S3 blob storage 설정
  ![image](https://user-images.githubusercontent.com/40287191/121130254-1edf3d00-c869-11eb-92a9-c257de7c6905.png)

  ![image](https://user-images.githubusercontent.com/40287191/121130276-256db480-c869-11eb-98b1-3abc986daf9b.png)

    
  ### 2. GitHub Enterprise 레벨에서의 조직별 활성화/비활성화 설정 및 사용할 Actions 허용정책 설정
   - Enterprise 설정 > Policies > Actions [메뉴](https://docs.github.com/en/enterprise-server@3.1/admin/github-actions/enabling-github-actions-for-github-enterprise-server/enforcing-github-actions-policies-for-your-enterprise) 
   - 'Enable for all organizations' 또는 허용할 조직 선택
   - 허용할 Actions 타입 선택
     - Allow all actions : 모든 Actions 허용
     - Allow local actions only : Enterprise 내부의 저장소에 정의된 Actions들만 허용
     - Allow select actions : 선택된 Actions들만 허용
   
   - Private folk로 부터의 Actions 허용
 
  ### 4. Org 레벨에서의 Actions 허용 정책 설정
    - Org 설정 > Actions [메뉴](https://docs.github.com/en/enterprise-server@3.1/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization)
  
  ### 5. Repo 레벨에서의 Actions 허용 정책 설정
    - Repo 설정 > Actions 메뉴

</p>
</details>

# 


** 본 문서는 GitHub Enterprise Server 버젼 3.1을 기준으로 작성되었습니다. 
