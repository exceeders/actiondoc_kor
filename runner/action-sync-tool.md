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
  
