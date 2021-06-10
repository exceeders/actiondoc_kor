# Action-sync-tool

 - `actions-sync` tool을 사용하여 인터넷이 가능한 곳에서 Actions를 다운 받은 뒤, 온프렘의 저장소로 push할 수 있습니다. 
 - GitHub.com으로 부터의 Pull과 내부로의 Push를 동시에 할 수도 있고 (`action-sync sync`), Pull이후에 별도로 Push를 진행 할 수도 있습니다(`action-sync pull`, `action-sync push`). 
 
   ```
   ./actions-sync sync \
   --cache-dir "cache" \
   --destination-token "aabbccddeeffgg" \
   --destination-url "https://my-ghes-instance" \
   --repo-name "docker/build-push-action:synced-actions/docker-build-push-action"  
   ``` 
 
  - 동시에 여러 저장소를 Sync하려면, `--repo-name` 부분을 아래와 같이 변경하면 됩니다. 
    - `repo-name-list` : 컴마(,)로 저장소 명칭을 구분하여 여러개 나열
    - `repo-name-list-file`: 저장소들의 이름을 가진 파일 경로
  

[🔙](https://github.com/exceeders/Actions_gettingStarted/blob/main/README.md#3-connect-%EC%84%A4%EC%A0%95-%EB%B0%8F-self-hosted-%EB%9F%AC%EB%84%88%EC%9D%98-%EC%9D%B8%ED%84%B0%EB%84%B7-%EC%97%B0%EA%B2%B0%EC%9D%B4-%EB%B6%88%EA%B0%80%ED%95%9C-%EA%B2%BD%EC%9A%B0-action-sync-tool-%EC%82%AC%EC%9A%A9)
