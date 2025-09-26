# Guachi 활용 사례 가이드

이 문서는 Guachi 설정 관리 라이브러리의 다양한 실제 활용 사례를 설명합니다.

## 1. 웹 애플리케이션 설정 관리

데이터베이스 연결, API 키, 서비스 설정 등을 관리합니다.

```python
# 데이터베이스 및 API 설정 예시
conf = ConfigMapper("/app/config/db")
db_settings = conf.stored_config()

DATABASE_URL = f"postgresql://{db_settings['user']}:{db_settings['password']}@{db_settings['host']}"
API_KEY = db_settings.get('api_key')
```

## 2. 다중 환경 설정 관리

개발, 테스트, 프로덕션 환경별 설정을 관리합니다.

```ini
[DEFAULT]
environment = development

[development]
debug = True
database_url = sqlite:///dev.db
log_level = DEBUG

[production]
debug = False
database_url = postgresql://user:pass@host/db
log_level = WARNING
```

## 3. 사용자 기본 설정 관리

데스크톱 애플리케이션의 사용자 설정을 관리합니다.

```ini
[USER_PREFERENCES]
theme = dark
language = ko
auto_save = true
window_size = 1920x1080
```

```python
user_conf = ConfigMapper("~/.myapp/preferences")
prefs = user_conf.stored_config()
```

## 4. 분산 시스템 설정

여러 서버나 마이크로서비스 간의 공유 설정을 관리합니다.

```ini
[MICROSERVICES]
service_discovery_url = http://discovery:8500
max_retries = 3
timeout = 30
```

## 5. 로깅 및 모니터링 설정

애플리케이션의 로깅 설정을 관리합니다.

```ini
[LOGGING]
log_format = json
log_path = /var/log/myapp
retention_days = 30
sentry_dsn = https://...
```

## 6. 기능 플래그 관리

특정 기능의 활성화/비활성화를 관리합니다.

```ini
[FEATURES]
new_ui = true
beta_features = false
maintenance_mode = false
```

## 7. 백업 및 복구 설정

시스템 백업 관련 설정을 관리합니다.

```ini
[BACKUP]
backup_path = /backup
schedule = 0 0 * * *
retention_count = 7
compress = true
```

## 8. 다국어 지원 설정

언어 및 지역화 관련 설정을 관리합니다.

```ini
[I18N]
default_language = ko
available_languages = en,ko,ja
date_format = YYYY-MM-DD
timezone = Asia/Seoul
```

## 주요 장점

- **즉시 반영**: 설정 변경이 즉시 저장되고 모든 컴포넌트에 반영됩니다.
- **단순한 형식**: INI 형식으로 이해하기 쉽고 관리가 용이합니다.
- **기본값 지원**: 누락된 설정에 대한 안전한 처리가 가능합니다.
- **영속성**: SQLite 기반으로 설정의 영속성이 보장됩니다.
- **실시간 갱신**: 프로그램 재시작 없이 설정 변경이 가능합니다.

## 구현 예시

각 사례별 상세한 구현 방법은 `examples` 디렉토리의 예제 코드를 참조하세요.