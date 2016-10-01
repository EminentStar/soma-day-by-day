# Consistent Hashing

## [핵심정리]  
Consistent Hashing의 핵심은 노드와 key가 같은 id의 공간을 가진다는 것이다.  
예를 들어,  
노드의 IP를 해시펑션의 input으로 넣어 ID를 만들고,  
데이터의 key를 해시펑션의 input으로 넣어 ID를 만들어 가은 ID 공간에 저장한다.  
그리고 각 노드들의 ID를 기준으로 해서, 데이터의 key의 ID가 반시계방향으로 가장 가까운 ID의 노드에 데이터가 저장된다. 

(그런데 Consitent Hashing은 Uniform distribution이라는 전제가 깔려있어야 하는듯?하다? Load balance라는 이점이  있으려면?)  

-----

### Consistent hashing은 매우 간단하다. 
데이터베이스의 cluster나 웹 캐시의 클러스터에서 수많은 노드들이 있을때, 특정한 키의 데이터가 어느 cluster에 가야하는지를 알아낼때 key에 hash function을 쓴다. 이것이 Consistent hashing의 전부임.  
같은 키는 같은 해시값을 만들기때문에, 일단 이용가능한 노드들 사이에서 key range를 어떻게 설정했는지 파악한다면, 키에 대한 hash값을 통해 올바른 노드를 찾을 수 있다.  
Consistent hashing은 샤딩을 매우 우아하게 적용시키도록 시도하는 문제를 해결해준다.  
Range 방식으로 디비를 샤딩하면 일정 구간의 range는 같은 노드안에 저장되게된다. 그러나 cluster에서의 위치를 해시값으로 결정하면, 사전적으로 밀접한 두개의 키가 서로 다른 노드에 들어갈 가능성이 더 높게된다. 그래서 부하는 좀더 균등하게 분배되는데, 이는 우리가 키의 순서를 잃게 되는 단점이라고 볼 수 있다.  

---

### Consistent Hashing은 partitioning을 가능하게 한다.   
> Consistent hashing을 하게 되면 모든 것이 파티션처럼 보인다.  
> Consitent hashing은 keyspace를 형성한다. (keyspace??)  
> 노드가 cluster에 들어오게되면서 랜덤 숫자를 고르게되고, 이 숫자는 책임이 있는 데이터??를 결정하게 된다. 이 숫자와 다른 노드에 의해 이전에 선택된 바로 옆의 숫자간의 모든 것은 같은 노드에 속해있다. partition은 이론적으로 사이즈가 다양할 수 있다.  

Consistent hashing 구현에서 또 문제가 있는데, 램덤 range의 키를 고르는 노드가 하나의 노드에서 다른 노드들 보다 훨씬 큰 keyspace를 잠재적으로 가져오는 것을 일으킨다는 것이다. 그러므로 이는 여전히 hotspot을 만든다.  
  
그러나 구현은 정말 간단하다. 해시 함수는 최대치의 결과셋을 가지는데, sha1의 경우는 2^160의 값을 가진다. 랜덤 키를 고르는 대신에 노드는 정해진 파티션의 집합으로부터 선택할 수 있다. 이 파티션들은 동등하게 분산된다. 파티션 넘버는 앞단에서 선택되고 cluster가 존재하는한 절대 바뀌지 않는다.  
  
같은 크기의 정해진 숫자의 파티션과 함께, 새로운 노드를 추가하는 것은 consistent hashing과 함께 덜 부담을 주게 되었다. 이전과 같이, 얼마나 많은 데이터가 새로운 노드의 범위에서 소유되기 위해 전송되어야할지를 아는 것은 힘들다. 한가지 확실한 것은 이것은 이전의 데이터를 샤딩하는 방법보다 덜 수고스럽다는 것이 이미 증명되었다는 것이다.  
  
파티셔닝과 함께 노드는 간단하게 파티션을 얻고, explicitly 하거나 implicitly하게 현재 주인에게 데이터를 가져갈 것인지 묻는다. 파티션이 오직 수많은 키들을 포함할 수 있으면서, randomness는 다소 훨씬 데이터의 확장을 보장한다. 또 한, 위치가 옮겨질 필요가 있는 데이터에 대한 예측불가성은 더 줄어들게 되었다.  
Consistent hashing은 오직 key에 대해서만 집중한다.  

---

### Consistent Hashing과 partitioning은 replication을 가능하게 한다.  

  또한 Consistent Hashing은 여러대 노드간의 데이터의 replication을 수월하게 만든다.   

**(?????)**  
> 고정된 파티션의 집합과 함께, 새로운 노드는 책임이 있는 노드를 선택 할 수도 있고, 그리고 또다른 파티션의 스택(replica가 될 예정인)을 고를 수도 있다. 이것에 대해 생각해봤을 때, 두개의 과정은 똑같다(??) consistent hashing의 아름다움은 어떤 데이터의 조각에 대해서도 마스터가 될 필요가 없다는 것이다. 모든 노드는 간단하게 파티션들중에서의 replica가 된다.  
  
이와 함께 replication은 hotspot을 줄여주는데, request의 load를 분산함으로써 가능하다. 이와 함께 cluster에 더많은 노드를 추가하면서, consistent hashing은 수용력의 측면에서 좀더 우아한 선형증가를 가능하게 한다.  

---

### Consistent Hashing은 Scalability와 Availability를 가능하게 한다.
> Consistent Hashing은 스케일 확장 축소를 쉽게하고 가용성을 더쉽게 보장한다. 데이터를 replicate하는 더 쉬운 방법은 더 나은 가용성과 장애극복을 가능하게 한다. 노드들이 움직일때 데이터를 다시 섞는 좀더 쉬운 방법은 스케일 확장 축소를 더 간단히 할 수 있다는 의미가 된다.
