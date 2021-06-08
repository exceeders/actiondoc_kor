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

# GHES Actions/Packages 구성요소
<details><summary> </summary>
<p>
  - GitHub Enterprise Server with version 3.0 or higher
  - Self-hosted Runner
     - 실제 Job을 수행할 환경 (Linux/Window/Mac)
     - GitHub-hosted runner는 현재 GitHub Enterprise Cloud에서만 가능 (GitHub Enterprise Server는 향후지원예정)
  - S3 compatible blob storage
     - Actions 로그 및 Packages 저장용
     - AWS, Azure
     - 순수 온프렘을 위해서는 MinIO NAS Gateway
  
</p>
</details>

# GHES Actions/Packages 설정
<details><summary> </summary>
<p>
  ### 1. Instance에서 Actions/Packages 활성화 및 S3 blob storage 설정
    ![image](https://user-images.githubusercontent.com/40287191/121130254-1edf3d00-c869-11eb-92a9-c257de7c6905.png)

    ![image](https://user-images.githubusercontent.com/40287191/121130276-256db480-c869-11eb-98b1-3abc986daf9b.png)

    
  ### 2. GitHub Enterprise 레벨에서의 조직별 활성화/비활성화 설정 
  
  ### 3. GitHub Enterprise 레벨에서의 Actions 허용 정책 설정
  
  ### 4. Org 레벨에서의 Actions 허용 정책 설정
  
  ### 5. Repo 레벨에서의 Actions 허용 정책 설정

</p>
</details>
