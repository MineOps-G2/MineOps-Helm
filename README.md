# MineOps Minecraft server

MineOps 프로젝트의 Helm파일을 모아놓은 repository입니다.

현재 minecraft -> kafka -> fluent-bit 순으로 실행해야 합니다.

## minecraft

itzg의 minecraft server helm을 참고하여 생성한 helm입니다.

```shell
helm install ./minecraft -f /minecraft/values.yaml
```

## kafka

bitnami의 kafka helm을 그대로 사용합니다.

```shell
heml install ./kafka -f ./kafka/values.yaml
```

## fluent-bit

fluent의 fluent-bit helm에서 조금 변경한 Chart입니다.
마인크래프트 pvc에서 log를 가지고 오기 위해 마인크래프트 helm과 같은 namespace에서 실행해야 합니다.

```shell
heml install ./fluent-bit -f ./fluent-bit/values.yaml
```