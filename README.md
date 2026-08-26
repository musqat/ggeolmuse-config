# GGeolmuse Config

[ggeolmuse](https://github.com/musqat/ggeolmuse) 의 Spring Cloud Config Server 중앙 설정 저장소.

코드와 분리해 둬서 cron, 수집 상한, 서킷브레이커 임계 같은 값은 재배포 없이 바꾼다.

## 레이어 (Spring 우선순위)

- `application.yml` — 전 서비스 공통 (keycloak/jwt/DB풀/kafka 등)
- `{service}.yml` — 서비스 공통
- `{service}-{dev|prod}.yml` — 환경별 (DB, 로깅, secret)
- `application-prod.yml` — prod 전용 (AWS Secrets Manager import)

## 대상 서비스 (config-server 사용)

user · trade · market-data · backtest · gateway

> chat-service(AI, Python)는 config-server 미사용 — 환경변수로 설정.

## 비밀값

이 저장소는 공개다. 실제 비밀값은 들어 있지 않다.

모든 값은 `${ENV_NAME:기본값}` 형태로, 실제 값은 주입된다.

- 운영 — AWS Secrets Manager `ggeolmuse/production` 을 `application-prod.yml` 에서 import
- 로컬 — `docker-compose/.env`

dev 프로파일의 H2 계정처럼 의미 없는 값만 그대로 적혀 있다.

## 반영 시점

서비스가 재기동할 때 읽는다.

여기만 고치고 배포를 안 하면 아무 일도 일어나지 않는다. 반대로 코드와 설정이 짝인
변경은 한쪽만 배포하면 기본값으로 돌아간다. 이미지 태그를 올릴 때 같이 나가야 한다.

## 참조 경로

config-server 가 어느 저장소의 어느 브랜치를 볼지는 환경변수로 정한다.

- `CONFIG_GIT_URI` — 기본 `https://github.com/musqat/ggeolmuse-config.git`
- `CONFIG_GIT_LABEL` — 기본 `main`

브랜치가 곧 배포 라벨이다. `main` 에 푸시하면 다음 재기동부터 운영이 그 값을 쓴다.
