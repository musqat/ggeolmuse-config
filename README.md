# GGeolmuse 설정 저장소

GGeolmuse 마이크로서비스를 위한 Spring Cloud Config 설정 파일 저장소입니다.

## 구조

- `{서비스명}.yml`: 서비스의 기본 설정 (공통)
- `{서비스명}-{프로파일}.yml`: 환경별 설정 (프로파일 override)

## 서비스 목록

- **gateway-server**: API Gateway 서버
- **user-service**: 사용자 관리 서비스
- **trade-service**: 거래 관리 서비스
- **market-data-service**: 시장 데이터 서비스
- **backtest-service**: 백테스팅 서비스

## 프로파일

- **dev**: 개발 환경 (H2 DB, DEBUG 로깅, Yahoo Finance)
- **prod**: 운영 환경 (PostgreSQL, INFO 로깅, Alpha Vantage)

## 설정 로드 방식

Config Server가 Git backend를 통해 이 저장소를 읽습니다.

### 예시

**서비스명**: `gateway-server`
**프로파일**: `dev`
→ 로드되는 파일: `gateway-server.yml` + `gateway-server-dev.yml`

Spring은 기본 설정(.yml)과 프로파일별 설정(-{profile}.yml)을 병합하며,
프로파일 설정이 기본 설정을 override합니다.

## 주요 차이점

### Dev 프로파일
- H2 인메모리 데이터베이스
- show-sql: true
- DEBUG 레벨 로깅
- H2 콘솔 활성화
- Yahoo Finance (무료)

### Prod 프로파일
- PostgreSQL 데이터베이스
- show-sql: false
- INFO/WARN 레벨 로깅
- H2 콘솔 비활성화
- Alpha Vantage (유료 API)
