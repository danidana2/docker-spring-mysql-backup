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
이 프로젝트는 **Docker**와 **Docker Compose**를 활용하여 Spring Boot 기반 애플리케이션과 MySQL 데이터베이스를 **컨테이너화**하여 쉽고 **효율적인 배포 환경**을 구축하는 것을 목표로 합니다. 또한, MySQL 데이터베이스의 **주기적 백업 자동화**를 통해 **데이터 보호와 복구**에 대비할 수 있는 시스템을 구현하였습니다.

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
이 프로젝트는 Docker와 Docker Compose를 활용하여 Spring Boot 애플리케이션과 MySQL 데이터베이스를 효과적으로 **컨테이너화한 배포 환경**을 제공합니다. 이를 통해 배포 및 관리 과정에서 환경 설정의 차이로 발생할 수 있는 문제를 줄이고, 운영 작업을 보다 간편하게 수행할 수 있습니다. 또한, 자동화 스크립트(run.sh, backup.sh)와 crontab 연동을 통해 **애플리케이션 빌드, 실행, 모니터링, 데이터베이스 백업 등의 주요 작업을 자동화**하여 시스템 관리를 효율적으로 지원합니다.

### <a id="components"></a>구성 요소 📌
- **Spring Boot 애플리케이션**  
  Java 기반의 Spring Boot 애플리케이션으로, Dockerfile을 통해 OpenJDK 17-slim 이미지를 기반으로 빌드됩니다. REST API 엔드포인트와 헬스 체크 기능을 제공하여 서비스의 상태를 모니터링합니다.

- **MySQL 데이터베이스**  
  MySQL 8.0을 사용하여 애플리케이션 데이터를 저장합니다. docker-compose.yml 파일에서 정의된 볼륨을 통해 데이터의 지속성을 보장하며, 환경 변수로 데이터베이스 설정을 관리합니다.

- **Dockerfile 및 Docker Compose**  
  - **Dockerfile**  
    애플리케이션 실행 환경을 구성하고, 필요한 패키지(curl 등)를 설치하며, JAR 파일을 컨테이너 이미지에 복사하여 실행합니다.
  - **docker-compose.yml**  
    Spring Boot 애플리케이션과 MySQL 데이터베이스 컨테이너를 정의하고, 네트워크, 볼륨, 환경 변수 및 서비스 간 의존성을 설정합니다.

- **환경 변수 파일 (.env)**  
  데이터베이스 연결 정보와 서버 설정 등을 중앙에서 관리하여, 다양한 환경에서 동일한 구성을 재사용하고 필요에 따라 쉽게 변경할 수 있습니다. 이를 통해 설정 관리의 일관성과 효율성을 높입니다.

- **백업 및 실행 스크립트**  
  - **backup.sh**  
    MySQL 데이터베이스 컨테이너 내에서 `mysqldump` 명령어를 실행해 정기적으로 데이터를 백업하며, 생성된 백업 파일은 지정된 디렉토리에 저장됩니다.
  - **run.sh**  
    프로젝트 실행 전 Docker와 Docker Compose 설치 여부를 확인하고, 기존 컨테이너를 정리한 후 새로운 컨테이너를 빌드 및 시작하는 자동화 스크립트입니다.

- **크론 작업**  
  crontab을 통해 backup.sh 스크립트를 주기적으로 실행하여, 데이터베이스의 백업 작업을 자동화합니다.


### <a id="workflow"></a>워크플로우 🔁
1. **환경 설정 및 준비:**  
   - 프로젝트 루트에 위치한 `.env` 파일을 통해 데이터베이스 및 애플리케이션 환경 변수를 설정합니다.
   - Dockerfile, docker-compose.yml, run.sh, backup.sh, 애플리케이션 JAR 파일 등 필요한 파일과 디렉토리를 준비합니다.

2. **프로젝트 실행:**  
   - 터미널에서 프로젝트 루트로 이동 후 `./run.sh` 스크립트를 실행합니다.
   - 스크립트가 Docker와 Docker Compose 설치 여부를 확인하고, 기존 컨테이너를 정리한 후 새로운 컨테이너를 빌드 및 실행합니다.
   - 두 컨테이너는 네트워크를 통해 서로 연결되며, MySQL 데이터베이스는 볼륨을 사용해 데이터를 지속적으로 저장합니다.

3. **애플리케이션 동작 확인:**  
   - curl 명령어 등을 사용하여 애플리케이션의 헬스 체크 엔드포인트(`/check`)와 데이터 처리 엔드포인트(`/save`, `/one`)의 정상 동작 여부를 확인합니다.
   - Docker 명령어(`docker ps`, `docker images` 등)를 통해 컨테이너와 이미지 상태 등을 모니터링합니다.

4. **데이터베이스 백업:**  
   - crontab에 등록된 주기적 작업을 통해 backup.sh 스크립트가 실행되어 MySQL 데이터베이스의 데이터를 SQL 파일로 백업합니다.
   - 백업 파일은 지정된 `backup` 디렉토리에 저장되며, 백업 로그를 통해 작업 결과를 확인할 수 있습니다.

---

## <a id="technologies"></a>🚀 활용 기술
| 분류  | 활용 기술 |
| ----- | -------- |
| **가상화**   | <img src="https://img.shields.io/badge/VirtualBox-183A61?style=flat-square&logo=virtualbox&logoColor=white" alt="VirtualBox" />  |
| **컨테이너**  | <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker" /> <img src="https://img.shields.io/badge/Docker%20Compose-009CE6?style=flat-square&logo=docker-compose&logoColor=white" alt="Docker Compose" /> <img src="https://img.shields.io/badge/ui--for--docker-FF9900?style=flat-square&logo=docker&logoColor=white" alt="ui-for-docker" /> |
| **백엔드**  | <img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white" alt="Spring Boot" /> <img src="https://img.shields.io/badge/Java-007396?style=flat-square&logo=java&logoColor=white" alt="Java" />  |
| **데이터베이스**   | <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL" />  |
| **데이터베이스 도구**  | <img src="https://img.shields.io/badge/DBeaver-003087?style=flat-square&logo=dbeaver&logoColor=white" alt="DBeaver" />  |
| **스크립팅 & 자동화**  | <img src="https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white" alt="Bash" /> <img src="https://img.shields.io/badge/Cron-000000?style=flat-square&logo=cron&logoColor=white" alt="Cron" />  |


---

## <a id="implementation"></a>🏗️⚙️ 구현 및 실행

### <a id="directory-structure"></a>파일 및 디렉토리 구조 📁

### <a id="config-and-scripts"></a>구성 파일 및 스크립트 설명 📝

### <a id="requirements-and-usage"></a>사전 요구사항 및 실행 방법 ▶️

---

## <a id="troubleshooting"></a>🔫 트러블슈팅

---

## <a id="improvements"></a>💡 고찰 및 개선점
