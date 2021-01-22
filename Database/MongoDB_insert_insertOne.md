## MongoDB_insert, insertOne, insertMany

### 도큐먼트 생성

insert, insertOne, insertMany는 모두 MongoDB에서 도큐먼트를 생성하는 명령어이다.

insertOne은 단일 도큐먼트를 생성하고 insertMany는 다수의 도큐먼트를 생성한다.

insert와 insertOne의 차이는 무엇일까?



### insert vs insertOne

**insert**는 단일 도큐먼트 생성, 다수 도큐먼트 생성을 모두 지원한다. 도큐먼트를 생성하고 단일 도큐먼트일 경우 WriteResult 개체를 반환하며 다수 도큐먼트일 경우 BulkWriteResult 개체를 반환한다. 

**insertOne**은 단일 도큐먼트를 생성하고 다음과 같은 결과를 반환한다.

```javascript
{
    "acknowledged" : true, // 입력이 성공했는지
    "insertedId" : <ObjectedId> // 성공한 도큐먼트의 ObjectID 값
}
```

**insert**는 주요 드라이버에서 더 이상 사용되지 않기 때문에 단일 도큐먼트를 생성할 경우 **insertOne**을, 다수 도큐먼트를 생성할 경우 **insertMany**를 사용해야 한다. 

**insert**가 더 이상 사용되지 않는 이유는 위에서 언급한 명령 실행 후 반환되는 개체 때문이다. **insertOne**이나 **insertMany**의 경우 도큐먼트 생성을 실패했을 경우 **WriteError**가 발생하며 **errmsg**필드에 에러 메시지를 반환한다. 하지만 **insert**는 성공과 실패 모두 개체를 반환하기 때문에 처리가 비교적 어렵다.



