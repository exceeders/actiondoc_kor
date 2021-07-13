# Workflow 파일 구조

#### 1. 워크 플로우는 저장소 root 디렉토리의 .github/workflows 디렉토리에 저장. (.yaml, .yml 파일)

#### 2. 워크 플로우는 "Job"과, Job내부의 개별 task들을 수행하는 step들로 구성됩니다. 
![image](https://user-images.githubusercontent.com/40287191/122013912-9bd65d80-cdf9-11eb-8a4a-68410a42b116.png)

#### 3. 워크 플로우는 GitHub event에 의해 시작되거나, 외부 event 또는 스케쥴에 맞춰 시작 가능

![image](https://user-images.githubusercontent.com/40287191/122313123-993a4c00-cf50-11eb-9e0c-e51ff8aad9c3.png)


#### 4. 워크 플로우는 하나이상의 job을 포함하고 있으며, 각 job은 개별적으로 독립적인 '러너'에서 실행됩니다. (하나의 '러너'는 동시에 '한개'의 Job만을 수행할 수 있습니다)

![image](https://user-images.githubusercontent.com/40287191/122313244-d4d51600-cf50-11eb-808c-84814e8740dc.png)


#### 5. 워크플로우내의 Job들은 기본적으로 "동시"에 병렬로 실행되나, Job내의 'Step'들은 "순차적"으로 실행됩니다. 

  ![image](https://user-images.githubusercontent.com/40287191/122321582-0c4abf00-cf5f-11eb-8cda-d07403edaa2c.png)


#### 6. 저장소의 admin 권한 및 쓰기권한이상의 사용자가 Actions를 생성하고 검토하고 수정할 수 있음

- Actions 탭
![image](https://user-images.githubusercontent.com/40287191/122313379-0f3eb300-cf51-11eb-9cb5-96d976bdc1c2.png)

- 왼쪽 사이드바에서 확인하고 싶은 워크플로우
![image](https://user-images.githubusercontent.com/40287191/122313383-14036700-cf51-11eb-98c8-e8b399a15420.png)

![image](https://user-images.githubusercontent.com/40287191/122313467-3ac19d80-cf51-11eb-8065-8869095b5ced.png)

![image](https://user-images.githubusercontent.com/40287191/122313495-490fb980-cf51-11eb-8d2d-56bd517a3724.png)

#### 7. 워크 플로우 파일 기본 예제

```
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      
      - name: Check out repository code
        uses: actions/checkout@v2
      
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      
      - run: echo "🍏 This job's status is ${{ job.status }}."
```




