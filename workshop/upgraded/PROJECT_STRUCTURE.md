# Guachi 프로젝트 구조

이 문서는 Guachi 프로젝트의 파일 구조와 각 구성 요소의 역할을 설명합니다.

## 핵심 파일 및 디렉토리

### 루트 레벨 파일
- `setup.py`: 프로젝트의 설치 및 배포 설정 파일
- `MANIFEST.in`: 패키지에 포함될 추가 파일 목록
- `README.rst`: 프로젝트 문서화 (reStructuredText 형식)
- `distribute_setup.py`: Python 패키지 배포를 위한 설정 스크립트
- `distribute-0.6.10.tar.gz`: 배포 도구 패키지

### 주요 소스 코드 (`guachi/`)
- `__init__.py`: 패키지 초기화 및 주요 `ConfigMapper` 클래스 정의
- `config.py`: 설정 파일 처리 및 매핑 관련 코드
- `database.py`: 데이터베이스 상호작용을 위한 코드
- `tests/`: 테스트 스위트
  - `test_configmapper.py`: ConfigMapper 클래스 테스트
  - `test_configurations.py`: 설정 관리 테스트
  - `test_database.py`: 데이터베이스 기능 테스트
  - `test_integration.py`: 통합 테스트

### 문서화 (`docs/`)
- `source/`: 문서 소스 파일
  - `index.rst`: 메인 문서 페이지
  - `getting_started.rst`: 시작 가이드
  - `example_usage.rst`: 사용 예제
  - `changelog.rst`: 변경 이력
  - `other_uses.rst`: 기타 사용 사례
  - `conf.py`: Sphinx 문서 생성 설정
- `build/`: 생성된 문서 파일
  - `html/`: HTML 형식의 문서
  - `doctrees/`: 문서 생성을 위한 중간 파일

### 메타데이터 (`guachi.egg-info/`)
- `PKG-INFO`: 패키지 메타데이터
- `SOURCES.txt`: 소스 파일 목록
- `dependency_links.txt`: 의존성 다운로드 링크
- `top_level.txt`: 최상위 패키지 정보

## 주요 기능별 구조

1. **설정 관리**
   - `guachi/__init__.py`: ConfigMapper 클래스
   - `guachi/config.py`: 설정 파일 파싱 및 매핑

2. **데이터 저장**
   - `guachi/database.py`: 데이터베이스 상호작용

3. **테스트**
   - `guachi/tests/`: 단위 테스트 및 통합 테스트

4. **문서화**
   - `docs/source/`: 사용자 문서
   - `docs/build/`: 생성된 문서

## 업그레이드 대상

이 프로젝트는 Python 2.5용으로 작성되었으며, 다음 영역에서 현대화가 필요합니다:

1. Python 3 호환성
2. 현대적인 패키징 도구 사용 (setup.py 현대화)
3. 테스트 프레임워크 업데이트
4. 문서화 시스템 업데이트
5. 데이터베이스 처리 방식 개선