# NoSQL

>많은 양의 데이터를 단순히 저장할 때 사용. 의미가 있을지 모름.
>
>비정형 데이터 모델



서버의 수는 세대 이상인 홀수. 분산저장 (shard)

하나의 서버를 두개정도 더 복제해놓음 (replica)

시스템 확장이 간단함. 병령형태 확장 (scale-out)

단점: 서버가 꺼졌을 때 바로 알아차리지 못함 > 그동안 저장하지 못하여 데이터 소실



redis: 메모리기반의 데이터베이스





## MongoDB

> 많이 쓰는 툴: Robo 3T

json형태의 데이터 (key, value)

join 불가능

메모리 의존적

금융, 결제 등 트랜잭션이 중요한 서비스에는 부적합.

수정이나 삭제가 거의 없는 작업에 사용.



`mongod --port 20000 --dbpath c:/data/s1`: (원하는 포트번호로) mongoDB 실행시키기

`mongo --port 20000`: 해당 포트에 실행되는 mongoDB 접속



환경은 자바스크립트.

`show dbs`

`use [collection명]`



update(): 수정이라는 개념이 없음. 덮어쓰기.

​	$set 해당 요소만 추가/수정



관계형은 key에게 index를 주는 것이 일반적



### 파이썬

`conda install pymongo`: pymongo 설치



## ReplicaSet & Sharding

> 백업과 분산을 수월하게 하려고.
>
> replica: 복제 / shard: 분산저장



### 1) ReplicaSet

복제해놓는 것. 보통 세 개.

heartbeat를 이용하여 다른 노드가 동작하는지 주기적으로 검사

그러나 잠시 죽어있는 동안에는 데이터 저장 X (데이터소실)



### 2) Sharding

config: sharding을 위한 메타 데이터 저장.

mongos: client의 요청처리. config 서버의 메타 데이터를 이용하여 각 MongoDB의 데이터에 접근.


