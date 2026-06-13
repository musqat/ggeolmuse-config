# GGeolmuse Config

Spring Cloud Config Server 중앙 설정 저장소.

## 레이어 (Spring 우선순위: 아래가 위를 덮음)

- `application.yml` — 전 서비스 공통 (keycloak/jwt/DB풀/kafka 등)
- `{service}.yml` — 서비스 공통
- `{service}-{dev|prod}.yml` — 환경별 (DB, 로깅, secret)
- `application-prod.yml` — prod 전용 (AWS Secrets Manager import)

## 대상 서비스 (config-server 사용)

user · trade · market-data · backtest · gateway

> chat-service(AI, Python)는 config-server 미사용 — 환경변수로 설정.
