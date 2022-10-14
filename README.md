# Minecraft

[Minecraft](https://minecraft.net/)

## Introduction

해당 Helm chart는 마인크래프트 서버를 실행하는 chart입니다.
- 마인크래프트 서버를 실행
- 서버 운영진의 관리를 위한 RCON-web 서버 실행
- 서버상태 확인을 위한 서비스 제공

## Installing the Chart

Chart를 설치하기전 [Minecraft EULA](https://account.mojang.com/documents/minecraft_eula) 라이센스를 확인하세요.

```shell
helm install minecraft [minecraft helm path] -f [minecraft helm path]/values.yaml
```

## Uninstalling the Chart

```shell
helm delete minecraft
```
Chart와 연결된 모든 Kubernetes구성요소를 삭제합니다.

## Configuration

[itzg/minecraft-server](https://hub.docker.com/r/itzg/minecraft-server/) Docker image.

chart를 install할때 매개변수값을 따로 지정할 수 도 있지만 values.yaml 파일을 사용하는게 좋습니다.

```shell
helm install minecraft -f [minecraft helm path]/values.yaml [minecraft helm path]
```

## Persistence

[itzg/minecraft-server](https://hub.docker.com/r/itzg/minecraft-server/) 이미지는 저장된 게임과 모드는 `/data`에 저장합니다.
persistence.dataDir.enabled이 true로 설정되면 PVC가 생성됩니다.
emptyDir Volume은 Pod가 노드에 할당될 때 처음 성생성되며 Pod가 실행되는 동안 존재합니다.
만일 Pod가 제거된다면 영원히 삭제됩니다.
