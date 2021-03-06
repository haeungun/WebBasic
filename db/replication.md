# 복제
복제는 네트워크로 연결된 여러 장비들에서 동일한 데이터의 복사본을 유지하는 것이다. 
복제를 통해 다름과 같은 이점을 얻을 수 있다.
- 지리적으로 사용자와 가깝게 데이터를 유지하여 지연 시간을 줄임
- 시스템 일부에 장애가 발생해도 지속적으로 동작할 수 있데 해서 가용성을 높임
- 읽기 질의를 처리하는 장비 수를 확장해서 읽기 처리량을 늘림

## 복제 vs 파티셔닝
### 복제
- 같은 데이터의 복사본을 다른 위치에 있는 여러 노드에 유지
- 중복성
- 성능향상
### 파티셔닝
- 큰 데이터베이스를 파이션이라는 작은 서브셋으로 나누고 각 파티션을 서로 다른 노드에 할당
- 샤딩

> 노드: 데이터베이스 소프트웨어를 수행하는 각 장비나 가상 장비

일반적으로 많이 사용되는 복제 알고리즘은 크게 세 가지로 볼 수 있다. 
1. 단일 리더 복제
2. 다중 리더 복제
3. 리더 없는 복제

## 단일 리더 복제
레플리카는 동일한 데이터를 유지해야 하기 때문에 데이터베이스의 쓰기는 모든 레플리카에서 처리되어야 한다. 레플리카 중 하나를 리더로 지정하고, 
클라이언트가 데이터베이스에 쓰기를 할 때 클라이언트는 요청을 리더에게 보낸다. 요청을 받은 리더는 로컬 저장소에 새로운 데이터를 기록하고, 그 때마다 
데이터 변경을 **레플리카 로그*나 **변경 스트림**의 일부로 팔로워에게 전송한다. 각 팔로워가 리더로부터 로그를 받아 리더가 처리한 것과 동일한 순서로 
모든 쓰기를 적용하여 데이터베이스릐 로컬 복사본을 갱신단다.
> 쓰기는 리더에게만 허용되고, 읽기는 리더 or 임의의 팔로워에게 질의 가능

### 동기 vs 비동기식 복제
- 동기식 
  - 리더는 팔로워가 쓰기를 수신했는지 확인될때까지 대기
  - 팔로워가 리더와 일관성있는 최신 데이터 복사본을 가지는 것을 보장
  - 동기 팔로워가 응답하지 않는다면 쓰기 처리 불가능
  
- 비동기
  - 리더는 메시지 전송 루 팔로워의 응답을 기다리지 않음
  - 빠른 처리가 가능하고, 완전 비동기식 설정은 모든 팔로워가 잘못되더라도 리더가 쓰기를 계속할 수 있음
  - 내구성 약화(리더가 잘못되고 복구할 수 없으면 팔로워에 아직 복제되지 않은 모든 쓰기 유실)
  - 그럼에도 불구하고 팔로워가 많거나, 지리적으로 분산되어있다면 비동기를 많이 사용하기는 함 .. 
  
- 반동기
  - 팔로워 하나를 동기식으로 설정하고 나머지는 비동기로 설정
  - 적어도 두 노드에 최신 데이터 복사본이 있는 것을 보장
  
### 복제 로그 구현
> 리더 기반 복제의 실제 내부 동작
#### 구문 기반 복제
#### WAL 로그 shipping
#### 논리적(로우 기반) 로그 복제
#### 트리거 기반 복제

## 다중 리더 복제
## 리더 없는 복제
