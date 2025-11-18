# GGeolmuse Config

Spring Cloud Config Server 중앙 설정 저장소

## 파일 구조

```
├── application.yml              # 전체 서비스 공통 설정
├── {service}.yml                # 서비스별 공통 설정
├── {service}-dev.yml            # 개발 환경 설정
└── {service}-prod.yml           # 운영 환경 설정
```

## 서비스

- user-service
- trade-service
- market-data-service
- backtest-service
- gateway-server
