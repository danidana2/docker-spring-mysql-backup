# Shell Script를 활용한 Docker Compose 기반 스프링 부트 & MySQL 자동 백업 솔루션

## 🚦 목차

1. [📒 개요](#overview)
   - [프로젝트 목표 🎯](#project-goals)
   - [주요 기능 🌟](#features)
2. [📖 프로젝트 설명](#project-description)
   - [구성 요소 📌](#components)
   - [워크플로우 🔁](#workflow)
3. [🚀 활용 기술](#technologies)

4. [🏗️⚙️ 구현 및 실행](#implementation)
   - [파일 및 디렉토리 구조 📁](#directory-structure)
   - [구성 파일 및 스크립트 설명 📝](#config-and-scripts)
   - [사전 요구사항 및 실행 방법 ▶️](#requirements-and-usage)
5. [🔫 트러블슈팅](#troubleshooting)

6. [💡 고찰 및 개선점](#improvements)

---

## <a id="overview"></a>📒 개요
이 프로젝트는 **Docker**와 **Docker Compose**를 활용하여 Spring Boot 기반 애플리케이션과 MySQL 데이터베이스를 **컨테이너화**하여 쉽고 효율적인 배포 환경을 구축하는 것을 목표로 합니다. 또한, MySQL 데이터베이스의 **주기적 백업 자동화**를 통해 데이터 보호와 복구에 대비할 수 있는 시스템을 구현하였습니다.

### <a id="project-goals"></a>프로젝트 목표 🎯
- **컨테이너화된 배포 환경 구축**  
  Docker와 Docker Compose를 사용하여 애플리케이션과 데이터베이스를 각각 독립된 컨테이너로 배포 및 관리합니다.

- **자동 백업 시스템 구현**  
  주기적으로 MySQL 데이터베이스의 데이터를 백업함으로써 데이터 손실 위험에 대비하고, 신속한 복구가 가능하도록 합니다.

- **유지보수 및 확장성 확보**  
  환경 변수 관리, 헬스 체크, 의존성 설정 등 구성 파일과 스크립트를 통한 체계적인 관리로 프로젝트 유지보수와 향후 확장을 용이하게 합니다.

### <a id="features"></a>주요 기능 🌟
- **Docker 기반 실행:**  
  Dockerfile과 docker-compose.yml을 통해 애플리케이션 및 MySQL 데이터베이스 컨테이너를 손쉽게 구축하고 실행합니다.

- **헬스 체크 기능:**  
  컨테이너 내부에서 주기적으로 애플리케이션의 상태를 확인하여 서비스 정상 운영 여부를 모니터링합니다.

- **데이터베이스 백업 자동화:**  
  backup.sh 스크립트와 crontab 설정을 이용해 MySQL 데이터베이스의 정기적인 백업을 자동으로 수행합니다.

- **환경 변수 및 설정 관리:**  
  .env 파일을 통해 데이터베이스 및 서버 관련 설정을 중앙 집중식으로 관리하여 다양한 환경에 유연하게 대응할 수 있습니다.

- **서비스 간 의존성 관리:**  
  docker-compose의 `depends_on`과 헬스 체크를 활용하여 서비스 간 의존성을 효과적으로 제어합니다.

---

## <a id="project-description"></a>📖 프로젝트 설명

### <a id="components"></a>구성 요소 📌

### <a id="workflow"></a>워크플로우 🔁

---

## <a id="technologies"></a>🚀 활용 기술

---

## <a id="implementation"></a>🏗️⚙️ 구현 및 실행

### <a id="directory-structure"></a>파일 및 디렉토리 구조 📁

### <a id="config-and-scripts"></a>구성 파일 및 스크립트 설명 📝

### <a id="requirements-and-usage"></a>사전 요구사항 및 실행 방법 ▶️

---

## <a id="troubleshooting"></a>🔫 트러블슈팅

---

## <a id="improvements"></a>💡 고찰 및 개선점
