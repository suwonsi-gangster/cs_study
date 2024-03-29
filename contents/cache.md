### 캐싱, 캐시
- **캐싱**은 애플리케이션의 처리를 빠르게 해주는 아키텍처 패턴이다.</br>
이미 가져온 데이터나 계산된 결과의 복사본을 저장하여 처리 속도를 높인다.</br>
반복적으로 서버에서 동일한 결과를 받는 경우에 사용하면 좋다.

- **캐시**는 이 복사본을 저장하는 임시 장소를 의미한다.

원하는 데이터가 캐시에 존재할 경우 해당 데이터를 반환하는 것을 Cache Hit이라고 하고, 캐시에 존재하지 않아 DBMS 또는 서버에 요청하는 것을 Cache Miss라고 한다.

`아키텍처 패턴: 문제점을 해결하기 위한 일반화된 재사용 가능한 솔루션`

---

### Local Cache, Global Cache

- **Local Cache**</br>
Local 장비 내에서만 사용된다.</br>
속도가 빠르다.</br>
다른 서버와 데이터 공유가 어렵다.

- **Global Cache**</br>
여러 서버에서 Cache Server에 접근하여 사용한다.</br>
분산된 서버에서 데이터를 저장하고 조회할 수 있다.</br>
네트워크를 통해 데이터를 가져오므로, Local Cache에 비해 상대적으로 느리다.</br>
서버 간의 데이터 공유가 쉽다.

---

### 웹 캐시
**웹 캐시**는 브라우저가 웹 서버에게 받아온 이미지, HTML, CSS 등의 복사본을 특정 위치에 저장하는 것이다.

#### 웹 캐시의 장점
- 불필요한 네트워크 통신을 줄인다.</br>
클라이언트가 서버에 문서를 요청할 때, 서버는 해당 문서를 클라이언트에게 응답한다. 캐시를 이용하면 문서 사본이 캐시에 보관되고, 클라이언트가 똑같은 문서를 요청할 경우 캐시된 사본을 응답하면 되기 때문에, 중복하여 트래픽을 주고받는 네트워크 통신을 줄일 수 있다.

- 거리로 인한 네트워크 지연을 줄여준다.</br>
만약 보스턴과 샌프란시스코에서 네트워크 통신을 한다면 그 거리는 4,400km이고, 신호의 속도를 빛의 속도(300,000km/sec)로 가정하면 편도는 약 15ms, 왕복은 30ms가 걸린다. 캐시는 이러한 거리를 수천 km에서 수십 m로 줄일 수 있다.

- 갑작스러운 요청 쇄도(Flash Crowds)에 대처 가능하다.</br>
원 서버로의 요청을 줄이기 때문에 갑작스러운 요청 쇄도에 대처할 수 있다.

`이처럼 캐시는 장점이 다양하지만, 만료되지 않은 캐시로 인해 업데이트된 파일을 새로 받아오지 않아 이슈가 발생하는 것을 주의해야 한다.`

#### 캐시 사용법
캐시는 Cache-Control이라는 HTTP Header로 설정할 수 있다.

no-store : 캐시에 리소스를 저장하지 않는다.
no-cache : 캐시 만료기간에 상관하지 않고 항상 원 서버에게 리소스의 재검사를 요청한다.
must-revalidate : 캐시 만료기간이 지났을 경우에만 원 서버에게 리소스의 재검사를 요청한다.
public : 해당 리소스를 캐시 서버에 저장한다.
private : 해당 리소스를 캐시 서버에 저장하지 않는다. 개인정보성 리소스이거나 보안이 필요한 경우 사용한다.
max-age : 캐시의 만료 기간(초단위)를 설정한다.

`재검사(Revalidation)는 신선도 검사라고도 하며, 캐시가 갖고 있는 사본이 최신 데이터인지를 서버를 통해 검사하는 작업을 말한다. 최신 데이터인 경우 304 Not Modified 응답을 받으며, 이는 '캐시에 있는 사본 데이터가 최신이며, 수정되지 않았다.'를 의미한다.`


> 작성중... 
