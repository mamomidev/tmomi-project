

<div align="center">
  <img src="https://github.com/mamomidev/tmomi-project/assets/48711163/538d8788-67ef-49c3-9183-16f383ae066f" alt="image"/>
</div>


-------
![항해18기 앙케이트 상장 pptx (16)](https://github.com/mamomidev/tmomi-project/assets/102348866/ed745d5e-b5e4-46a0-ac19-3b61169ef71c)

# 🎟️ Tmomi

  ### <b>티모미</b>는 대용량 트래픽 및 트랜잭션 제어로 고가용성과 확장성을 확보한 티켓팅 서비스 입니다.
  ### 티켓의 예매 순서 보장 및 1천만 건의 데이터를 핸들링 하는 것이 목표입니다.
  
  </br> 
  
# 👥 팀원

| 이름          | 주소                          |
|-------------|-----------------------------|
| 👑 문혁준 (팀장) | https://github.com/mhj94    |
| 🧑🏻‍💻 김태훈 | https://github.com/TaeHoon0 |
| 🧑🏻‍💻 황영웅 | https://github.com/heroq    |

 </br> 

# 🧳 형상관리

| 이름       | 주소                                                                   |
|----------|----------------------------------------------------------------------|
| Project  | https://github.com/mamomidev/tmomi-project                           |
| Web      | https://github.com/mamomidev/tmomi.git                               |
| Producer | https://github.com/mamomidev/tmomi_producer.git                      |
| Consumer | https://github.com/mamomidev/tmomi_consumer.git                      |
| Notion   | [티모미 노션](https://tmomi.notion.site/db41f0cdd3954eac905003c2dbde633b) |

 </br> 
 
# 주요 기능 및 테스트

<details>
<summary>대기열 및 대기 번호 전달</summary>
  
- 트래픽이 집중되었을 때 Kafka를 사용하여 순서를 보장.
  
![queueTest](https://github.com/mamomidev/tmomi-project/assets/102348866/7cb25489-e92f-4945-a028-5e93c5e6b22d)
</details>

<details>
<summary>좌석 선택 시 동시성 제어</summary>
  
- 대규모 트래픽 티켓팅 서비스에서 좌석 선택 시, 동시성 이슈가 발생할 수 있음.
- Redis를 활용하여, 좌석에 대한 Lock을 통해 동시성을 제어.

![image](https://github.com/mamomidev/tmomi-project/assets/96118954/0f57a0bf-ea19-4074-abcf-8fa0765d1605)
- 좌석 획득 100개 요청 시, 1개의 성공과 99개의 실패의 결과를 확인할 수 있음.
- 1개의 성공 결과는 좌석에 대한 락을 획득하여, 나머지 99개의 실패 결과는 락을 획득하지 못하여 좌석 선택을 하지 못한 것을 확인할 수 있음.
</details>

<details>
<summary>대규모 데이터 핸들링</summary>

- 티켓 생성은 좌석 수만큼 생성.
- 현재 서비스에서, 티켓 구매는 생성이 아닌, 미리 생성 된 row에서 Update가 되는 방식.

![image](https://github.com/mamomidev/tmomi-project/assets/96118954/f5f2fbea-5c1b-4128-bd46-bd016ce71616)
- 빨간박스 안에 있는 그래프는 한 번에 데이터를 전송 했을 때, 파란색박스 안에 있는 그래프는 배치를 사용하여 데이터를 전송 했을 때 그래프.
- 사용량이 두 배정도 줄인 것을 확인.
- 흰색박스는 10만건, 50만건의 데이터를 전송해본 결과로, 각각 8s, 37s의 걸린 것을 확인.
</details>

<details>
<summary>대규모 트래픽 분산 오토 스케일링 그룹 + APM</summary>
  
- 대규모 트래픽이 집중되었을 때

![image](https://github.com/mamomidev/tmomi-project/assets/96118954/e00a3c0e-a2be-4415-9de9-64b9fcc88df1)
- 1개의 인스턴스에서, 트래픽이 집중되었을 때 Auto Scaling을 통해 부하를 줄일 수 있도록 구현.
- 위의 모니터링을 통해 인스턴스가 2개로 확장 되었고, 그래프에서 각각 분산처리 하는 것을 확인.

![image](https://github.com/mamomidev/tmomi-project/assets/96118954/dba18e06-1b0a-4567-a1b1-c9c2f02ad809)
- Auto Scaling으로 생성된 EC2의 데이터도 수집하는 것을 확인할 수 있음.
</details>

<br/>

# ERD

- Entity 및 Database 관계도
  <p float="left">
    <img src="https://github.com/mamomidev/tmomi-project/assets/102348866/b385c1a3-66a7-4c8b-a581-df070661ad42" width="480" />
    <img src="https://github.com/mamomidev/tmomi-project/assets/102348866/5f4aeb92-8177-42da-a898-81000bc9f7d2" width="480" /> 
  </p>

<br/>

# 서비스 아키텍처

![image](https://github.com/mamomidev/tmomi-project/assets/102348866/3f5566ab-12a8-4328-bf07-ae74ff616876)

<br/>

# 기술 스택

| 카테고리               | 사용 기술                                                                                               |
|--------------------|-----------------------------------------------------------------------------------------------------|
| Backend frameworks | Spring Boot, Spring JPA, Spring Security                                                            |
| TEST               | Spock, Jmeter                                                                                       |
| CI/CD              | Github Action                                                                                       |
| Database           | MySQL, Redis                                                                                        |
| Cloud services     | AWS EB, AWS EC2, AWS ALB, AWS ASG, AWS Route 53, AWS MSK, AWS CloudWatch, AWS ACM, Google Cloud SQL |
| APM                | Prometheus, Grafana                                                                                 |
| Data streaming     | Apache Kafka                                                                                        |
| Search engines     | Elastic Search                                                                                      |

<br/>

# 기술 의사 결정

| 요구사항         | 선택지                                   | 기술 선택 이유                                                                                                                                                                                                                                                                      |
|--------------|---------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 🛢️ 데이터 베이스  | MySQL<br>~~PostgreSQL~~               | - 초기에는 PostgreSQL을 사용하였지만, MySQL의 버전 업데이트가 진행되면서 대용량 데이터 처리 능력이 상당히 향상되었습니다. 이로 인해 두 데이터베이스 간의 성능 차이는 이제 거의 미미해졌습니다. <br>- 또한, MySQL은 읽기 작업에 특화되어 있어, 데이터 조회에 있어 뛰어난 효율성을 보여줍니다. 반면 PostgreSQL은 데이터를 주기적으로 정리해야 하는 'vacuum' 작업이 필요한 등, 관리 측면에서 약간의 부담이 있어 MySQL을 선택 하게 되었습니다. |
| 📈 부하 테스트    | Jmeter<br>~~nGrinder~~                | - SSE 연결 테스트를 수행하기 위해, nGrinder 대신 Jmeter를 선택하여 부하 테스트를 진행하게 되었습니다. 이는 Jmeter가 SSE 연결 테스트에 있어 더욱 우수한 성능을 보여주기 때문입니다                                                                                                                                                           |
| 📊 모니터링      | Grafana<br>Prometheus<br>~~Pinpoint~~ | - 시스템 관점에서 중요한 지표인 CPU 사용률, 메모리, 디스크 IO 등을 시각화하는 데 특화된 Prometheus를 선택하였습니다. <br>- Prometheus는 이런 지표들을 직관적으로 제공함으로써, 시스템 상태의 이해를 높이고 이상 징후를 빠르게 파악할 수 있게 도와줍니다. 또한, Prometheus의 Service Discovery 기능은 Auto scaling에 따른 동적인 시스템 변화에도 자동으로 대응하여 지표 수집을 보장하기 때문에 선택하게 되었습니다.      |
| 🛠️ 데이터 스트리밍 | Kafka<br>~~RabbitMQ~~                 | - 서비스의 특성상 일시적으로 대량의 트래픽이 몰리는 상황이 발생하므로, 이를 효과적으로 처리할 수 있는 높은 처리량이 필요했습니다. 또한, 장애 발생 시 빠른 복구와 끊임없는 서비스 가용성 역시 중요한 요구사항이었습니다. <br>- 이런 점들을 종합적으로 고려하였을 때, Kafka는 높은 처리량과 뛰어난 장애 복구 능력, 안정적인 가용성으로 선택하게 되었습니다.                                                                  |
| 🔍 검색 성능 개선  | Elasticsearch<br>~~Cache~~            | - Elasticsearch의 역 인덱스 기능은 모든 데이터를 일일이 조회하지 않고도 빠르게 검색 결과를 찾아주는 능력을 가지고 있습니다. 이는 곧바로 고성능의 실시간 검색을 가능케 하며, 서비스의 특성상 짧은 시간 내에 대량의 좌석 조회 요청이 발생하는 상황을 효율적으로 처리하기 위해, Elasticsearch를 선택하게 되었습니다.                                                                                  |
| ⚙️ CI/CD     | Github Action<br>~~Jenkins~~          | - GitHub Action은 쉽게 CI/CD를 구축할 수 있게 해주며, 별도의 서버 설치 없이도 사용 가능한 편리함을 제공합니다.<br>- 형상관리 툴인 GitHub를 사용하고 있었고, 이에 자연스럽게 사용할 수 있는 GitHub Action을 선택하게 되었습니다.                                                                                                                         |
| 🚀 소켓 통신     | SSE<br>~~WebSocket~~                  | - SSE(Server-Sent Events)를 선택한 이유는 클라이언트가 서버에 연결을 한 후, 서버로부터 데이터를 수신하는 단방향 통신 방식이기 때문입니다. <br>- 이런 특성으로 인해, Web Socket과 비교했을 때 서버에 대한 부하를 상당히 줄일 수 있을거라 판단했습니다. 따라서, 서버의 부하 감소와 효율적인 데이터 전송을 위해서 SSE를 선택하게 되었습니다.                                                             |
