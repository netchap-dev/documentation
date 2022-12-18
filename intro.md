# Overview

게시판 서비스.

## 1. 서비스 구성

![Netchap Architecture](./architecture/netchap_architecture.svg)

각 서비스 구성요소는 다음과 같다.

|서비스|사용 기술|목적 및 기능|비고|
|---|---|---|---|
|Admin|Node 16.15.0<br/>npm 8.5.5<br/>React 18.1.0|관리자 페이지 (백오피스)||
|Web|Node 16.15.0<br/>npm 8.5.5<br/>React 18.1.0|커뮤니티 웹페이지||
|API Gateway|Node 16.15.1<br/>npm 8.11.0<br/>Express 4.16.1|OAuth2 인증<br/>회원 정보 인증 및 JWT 발급 및 인증<br/>각 요청에 대해 해당 API로 프록시||
|API|Node 16.15.1<br/>npm 8.11.0<br/>Express 4.16.1|API Gateway에서 인증을 마친 후 넘어온 요청을 처리하는 서비스. 
|Filtering|Go 1.18|신규 게시물 중 부적절한 컨텐츠를 담은 내용을 감지하는 서비스||
|Notifications|Go 1.18|각 회원이 작성한 댓글 및 리액션 등에 대해 알림을 제공하는 서비스||

### 각 서비스 간 통신 프로토콜
기본적인 프로토콜은 전부 HTTP REST 기반으로 개발.

### 개발 시 활용되는 인프라

|이름|목적|비고|
|---|---|---|
|Redis|API Gateway 서비스와 연결되었으며, JWT 토큰 저장 및 인증정보 보관을 위한 in-memory DB|
|PostgreSQL|API와 연결된 각종 데이터 보관 목적의 RDBMS|
|Apache Kafka|신규 댓글 및 리액션, 게시물 등 발생시 관련 정보를 필터링 서비스로 넘겨주기 위한 데이터 스트리밍 서비스|

## 2. Pending Issues
