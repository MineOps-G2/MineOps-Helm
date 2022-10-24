# MineOps Minecraft server

MineOps 프로젝트의 Minecraft관련 Helm파일을 모아놓은 repository입니다.

Minecraft 로그를 kafka로 받기 위해서 minecraft -> kafka -> fluent-bit 순으로 실행해야 합니다. kafka topic은 `minelogs`입니다.

## minecraft

itzg의 minecraft server helm을 참고하여 생성한 helm입니다.

```shell
helm install mine-release ./minecraft -f ./minecraft/values.yaml
```

서버 데이터 백업을 위해 `mc-backup`을 사용합니다. 기본 상태는 `false`입니다.
데이터 백업을 위한 pvc는 aws eks의 기본 storageClass (gp2)를 이용합니다.

monitoring을 위해 promethus에 metric정보를 보내기위해 `mc-monitor`를 사용합니다.

- `minecraft_status_healthy`
- `minecraft_status_response_time_seconds`
- `minecraft_status_players_online_count`
- `minecraft_status_players_max_count`

## kafka

bitnami의 kafka helm을 그대로 사용합니다.

```shell
heml install kafka ./kafka -f ./kafka/values.yaml
```

## fluent-bit

fluent의 fluent-bit helm에서 조금 변경한 Chart입니다.
마인크래프트 pvc에서 log를 가지고 오기 위해 마인크래프트 helm과 같은 namespace에서 실행해야 합니다.

```shell
heml install fluent-bit ./fluent-bit -f ./fluent-bit/values.yaml
```