# Sporty v2

> **운동할 사람과 장소를 연결하는 AI 기반 생활체육 매칭 플랫폼**  
> LG CNS AM Inspire Camp 6기 · 미니프로젝트 2 · **2조 바통터치**

Sporty는 서울시 공공 체육시설 정보를 살펴보고, 운동 모임을 만들거나 참여할 수 있는 서비스입니다. AI를 이용한 매칭 검색·초안 작성·추천 기능도 제공합니다. 시설 예약은 서울시 공공서비스예약 페이지로 연결해 안내합니다.

이번 프로젝트에서는 [1차 Sporty](https://github.com/livelykitten/inspire_6th_mini_1_sporty)의 모놀리식 구조를 서비스별로 분리하고, 서비스 간 통신과 운영 상황을 확인할 수 있는 구조로 고도화합니다.

## Sporty v2에서 만드는 것

- **운동 매칭:** 모임 생성·검색·참여와 상태 관리
- **AI 지원:** 조건 기반 검색, 모임 초안 작성, 개인화 추천과 장애 시 대체 응답
- **Kafka 알림:** 참가·모임 상태 변경 이벤트를 알림함으로 전달
- **운영 모니터링:** Micrometer·Prometheus·Grafana로 서비스 상태, 응답시간, 오류율, Kafka 지연을 관측하고 장애 시나리오를 분석
- **회원 탈퇴 Saga:** 서비스별 데이터 정리와 실패 시 보상 처리를 통해 탈퇴 과정을 관리

## 서비스 구성

| 서비스 | 주요 역할 |
| --- | --- |
| `user-service` | 인증, 회원·프로필, 회원 탈퇴 |
| `match-service` | 운동 모임, 참가, 상태 전이 |
| `facility-service` | 서울시 체육시설 데이터 조회·동기화 |
| `ai-service` | AI 검색·초안·추천 |
| `notification-service` | 이벤트 구독과 사용자 알림함 |

React 프론트엔드가 API Gateway를 통해 각 서비스에 접근합니다. 서비스 발견은 Eureka, 설정 관리는 Config Server, 동기 호출은 Feign, 비동기 이벤트는 Kafka를 사용할 계획입니다.

## 저장소

| 저장소 | 용도 |
| --- | --- |
| [platform](https://github.com/batontouch-sporty/platform) | 제품 요구사항, MSA 아키텍처, 서비스 간 계약, 통합 개발·운영 문서 |
| [backend](https://github.com/batontouch-sporty/backend) | 백엔드 서비스와 인프라 구성 |
| [frontend](https://github.com/batontouch-sporty/frontend) | 사용자 웹 화면 |
| [config-repo](https://github.com/batontouch-sporty/config-repo) | 서비스별 외부 설정 |

> **개발 진행 중:** 위 구성과 기능은 Sporty v2 구현 계획을 기준으로 합니다. 완료 범위와 실행 방법은 각 저장소의 README에 기록합니다.
