# delta-for-dummies
delta lake tutorial

## Q&A
### 1. `PySpark` 실행을 위해서 `configure_spark_with_delta_pip` 명령 수행시에 `Java gateway process exited` 오류
* 해당 명령어 수행시에 외부 `maven` 접속을 통해서 `io.delta#delta-core_2.12;2.0.0` 등을 다운로드 받기위해 접속하게 됩니다
* 이 때에 호스트 장비에서는 외부로 접근이 가능하지만(불가능한 경우도 있고), 컨테이너 내부에서는 불가능한 경우가 있습니다
* 즉, 네트워크가 별도로 구성되어 있기 때문에 DNS 등의 환경이 다르기 때문에 접근이 안되므로 `local` 네트워크를 통해 접근이 가능합니다
  * 아래와 같이 설정하되 `port` 및 `hostname` 등의 설정 또한 모두 제거되어야만 합니다
```yaml
version: '3.8'

services:
  notebook:
    container_name: notebook
    image: psyoblade/data-engineer-notebook:1.7.5
    network_mode: host
```

### 2. 이슈 사항
* ARM 계열의 PC에서 컨테이너 실행 오류?
* 실행 시마다 외부 접근을 하는 문제?
* 최신 스파크 및 델타 적용 가능한가?
* 아파치 스쿱 최신 바이너리 이슈?