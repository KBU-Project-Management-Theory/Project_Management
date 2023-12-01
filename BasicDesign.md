# 기본설계


1. 아키텍처 설계
    * 서브시스템 분할:
    * 교육 신청 처리 서브시스템: 직원의 교육 신청 및 취소 관리.
    * 교육 관리 서브시스템: 교육 매니저가 교육 과정을 관리하고, 외부 교육 기관과의 연계 처리.
* 하드웨어 및 네트워크 요구 사항: 클라우드 기반 서버, 안정적인 네트워크 연결.
* SW 구성 요소: 데이터베이스 관리 시스템, 백엔드 프로세싱 서버, 프론트엔드 인터페이스.
2. UI 설계
    * 화면 레이아웃:
    * 직원용 인터페이스: 교육 과정 목록, 신청 및 취소 기능.
    * 교육 매니저 인터페이스: 교육 과정 관리, 신청서 처리, 외부 교육 기관 연동 기능.
* 화면 관계 및 전환: 직관적인 탭 및 메뉴 구성으로 사용자가 쉽게 기능을 이용할 수 있도록 함.
* 인쇄물 레이아웃: 신청서, 증명서 등의 인쇄물에 대한 레이아웃 설계.
3. 데이터 설계
4. 외부 인터페이스 설계
* 연동 데이터 형식: JSON, XML 등의 표준화된 데이터 형식 사용.
* 호출 방식: RESTful API를 통한 서비스 연동 및 데이터 교환.

1. 아키텍처 설계
   서브시스템 분할 및 기능 목록
* 교육 신청 처리 서브시스템
    * 기능:
    * 교육 과정 목록 조회
    * 교육 신청 및 취소
    * 신청 현황 조회
* 교육 관리 서브시스템
    * 기능:
    * 교육 과정 등록, 수정, 삭제
    * 신청서 관리 및 처리
    * 외부 교육 기관 연동 관리

시스템 구성 요소
* 클라이언트 계층 (Front-end)
  * 사용자 장치: 직원과 교육 매니저가 시스템에 접속하는 PC, 노트북, 태블릿, 스마트폰.
  * 웹 브라우저: 사용자 인터페이스를 렌더링하는 소프트웨어, 예를 들어 Chrome, Safari, Firefox.
* 애플리케이션 계층 (Application Layer)
  * 웹 서버: 클라이언트 요청을 처리하는 서버, 예를 들어 Apache, Nginx.
  * 애플리케이션 서버: 비즈니스 로직을 처리하고, 웹 서버와 데이터베이스 서버 사이의 인터페이스를 담당, 예를 들어 Tomcat, Node.js.
* 데이터 계층 (Data Layer)
  * 데이터베이스 서버: 교육과정, 사용자 정보, 신청 내역 등의 데이터를 관리하는 시스템, 예를 들어 MySQL, PostgreSQL.
  * 네트워크 인프라
  * 인터넷: 클라이언트와 서버 간의 연결을 담당.
  * 내부 네트워크: 기업 내부 네트워크, VPN을 통한 안전한 접속 환경.
  * 관계 및 상호작용
  * 사용자 ↔ 클라이언트 장치: 사용자는 웹 브라우저를 통해 시스템에 접속
  * 클라이언트 장치 ↔ 웹 서버: 웹 브라우저는 사용자의 요청을 웹 서버로 전송하고, 서버의 응답을 받음
  * 웹 서버 ↔ 애플리케이션 서버: 웹 서버는 애플리케이션 서버로 요청을 전달하고, 처리된 결과를 받음
  * 애플리케이션 서버 ↔ 데이터베이스 서버: 애플리케이션 서버는 데이터베이스 서버와 상호작용하여 데이터를 조회하거나 변경함.

### 상호작용 순서:
1. 사용자가 웹 브라우저를 통해 교육 신청 시스템에 접속함
2. 웹 서버가 사용자의 요청을 받아 애플리케이션 서버로 전달함
3. 애플리케이션 서버는 데이터베이스 서버와 통신하여 필요한 데이터를 조회하거나 변경함
4. 결과는 다시 애플리케이션 서버를 통해 웹 서버로, 그리고 사용자의 브라우저로 전달됨


## 데이터 설계

엔티티 및 속성:
* Employee (직원)
  * 속성:
  * EmployeeID: int (고유 식별자, 기본 키)
  * Name: string (직원 이름)
  * Email: string (직원 이메일)
  * Department: string (부서)
  * Position: string (직급)
* TrainingManager (교육 매니저)
  * 속성:
  * ManagerID: int (고유 식별자, 기본 키)
  * Name: string (매니저 이름)
  * Email: string (매니저 이메일)
  * Department: string (부서)
* ExternalTrainingInstitute (외부 교육 훈련 기관)
  * 속성:
  * InstituteID: int (고유 식별자, 기본 키)
  * InstituteName: string (기관명)
  * ContactInfo: string (연락처)
  * Address: string (주소)
* Course (교육과정)
  * 속성:
  * CourseID: int (고유 식별자, 기본 키)
  * CourseName: string (과정명)
  * Description: string (설명)
  * Duration: string (기간)
  * Cost: decimal (비용)

(연결 테이블):
* Registration (등록)
  * 속성:
  * RegistrationID: int (고유 식별자, 기본 키)
  * EmployeeID: int (직원 ID, 외래 키)
  * CourseID: int (교육과정 ID, 외래 키)
  * Status: string (등록 상태)
* TrainingRequest (교육 신청서)
  * 속성:
  * RequestID: int (고유 식별자, 기본 키)
  * ManagerID: int (교육 매니저 ID, 외래 키)
  * InstituteID: int (외부 교육 훈련 기관 ID, 외래 키)
  * CourseID: int (교육과정 ID, 외래 키)
  * RequestDate: date (신청 날짜)
  * Status: string (신청 상태)

  * 관계:
  * Employee와 Course 사이의 다대다 관계는 Registration 연결 테이블. Employee는 Registration에 대해 1대다 관계를 가지며, Course도 Registration에 대해 1대다 관계를 가짐.
  * TrainingManager와 Course 사이의 일대다 관계는 TrainingManager가 관리하는 여러 Course가 있음. (연결 테이블 x)
  * TrainingManager와 ExternalTrainingInstitute 사이의 다대다 관계는 TrainingRequest 연결 테이블로. TrainingManager는 TrainingRequest에 대해 1대다 관계를 가지고, ExternalTrainingInstitute도 TrainingRequest에 대해 1대다 관계
    <br>
    
* Registration (등록)
    * EmployeeID는 Employee의 EmployeeID에 대한 외래 키.
    * CourseID는 Course의 CourseID에 대한 외래 키.
    * 이 테이블은 각각의 등록 상태와 다른 필요한 메타데이터를 추적.
      ————
* TrainingRequest (교육 신청서)
    * ManagerID는 TrainingManager의 ManagerID에 대한 외래 키.
    * InstituteID는 ExternalTrainingInstitute의 InstituteID에 대한 외래 키.
    * CourseID는 신청된 Course의 CourseID에 대한 외래 키.

외부 인터페이스 설계
* 연동 데이터 형식: JSON, XML 등의 표준화된 데이터 형식 사용.
* 호출 방식: RESTful API를 통한 서비스 연동 및 데이터 교환.

최종 클래스 다이어그램

시퀀스 다이어그램
다이어그램 참조

교육 신청 관리 시스템 클래스 명세서 (상세):
* Employee (직원)
  * 속성:
  * EmployeeID: int (고유 식별자)
  * Name: string (직원 이름)
  * Email: string (직원 이메일)
  * Department: string (부서 이름)
  * Position: string (직급)
  * 메소드:
  * ApplyForCourse(CourseID): void (교육 과정에 신청)
  * CancelApplication(ApplicationID): void (신청한 교육 취소)
* TrainingManager (교육 매니저)
  * 속성:
  * ManagerID: int (고유 식별자)
  * Name: string (매니저 이름)
  * Email: string (매니저 이메일)
  * Department: string (부서 이름)
  * 메소드:
  * ApproveApplication(ApplicationID): void (교육 신청 승인)
  * RecommendCourse(EmployeeID): Course[] (직원에게 교육 과정 추천)
  * AddCourse(Course): void (새로운 교육 과정 추가)
  * UpdateCourse(CourseID, Course): void (교육 과정 정보 업데이트)
  * DeleteCourse(CourseID): void (교육 과정 삭제)
* ExternalTrainingInstitute (외부 교육 훈련 기관)
  * 속성:
  * InstituteID: int (고유 식별자)
  * InstituteName: string (기관 이름)
  * ContactInfo: string (연락처 정보)
  * Address: string (주소)
  * 메소드:
  * ReceiveApplication(Application): void (교육 신청서 수신)
  * ProcessCourseOrder(CourseID): void (교육 과정 주문 처리)
* Course (교육과정)
  * 속성:
  * CourseID: int (고유 식별자)
  * CourseName: string (교육 과정명)
  * Description: string (과정 설명)
  * Duration: string (기간)
  * Cost: decimal (비용)
  * 메소드:
  * RegisterEmployee(EmployeeID): void (직원을 과정에 등록)
  * UnregisterEmployee(EmployeeID): void (직원을 과정에서 등록 취소)
* Application (교육 신청서)
  * 속성:
  * ApplicationID: int (고유 식별자)
  * EmployeeID: int (신청 직원 ID)
  * CourseID: int (신청한 과정 ID)
  * Status: string (신청 상태)
  * 메소드:
  * Submit(): void (신청서 제출)
  * Cancel(): void (신청 취소)
## 최종 클래스 다이어그램 (상세 설명):
* Employee
* 여러 개의 Application 객체와 연결/  직원이 여러 교육 과정을 신청할 수 있음
* TrainingManager
* Course 객체의 생명주기를 관리함. 즉, 과정을 추가, 수정, 삭제할 수 있음.
* ExternalTrainingInstitute
* Application 객체를 수신하여 교육 과정의 주문을 처리합니다. 이는 외부 기관이 여러 교육 신청을 받고 처리할 수 있음.
* Course
* 직원이 등록할 수 있는 여러 Application 객체와 연결됨
* Application
* Employee와 Course 사이의 관계를 나타내며, 신청의 생명주기를 관리함.
———-클래스 관계
* Employee
    * Application: 직원은 여러 교육 신청서를 가질 수 있으므로, Employee와 Application 사이에 1대다 관계가 있습니다. 각 Application 인스턴스는 하나의 Employee에 매핑.
* TrainingManager
    * Course: 교육 매니저는 여러 교육 과정을 관리할 수 있으므로, TrainingManager와 Course 사이에 1대다 관계.
    * Application: 교육 매니저가 신청서를 검토하고 승인할 수 있으므로, TrainingManager와 Application 사이에 1대다 관계.
* Course
    * Application: 한 과정에 대해 여러 신청서가 제출될 수 있으므로, Course와 Application 사이에 1대다 관계.
* Application
    * Employee와 Course: Application은 Employee와 Course 사이의 다대다 관계/ 실제 데이터베이스 구현에서는 Application 테이블이 두 엔티티 사이의 연결 테이블. Application 클래스는 EmployeeID와 CourseID 외래 키를 가짐.
      하여 가지는 관계는 =>
* Employee 클래스는 Application 클래스로 가는 화살표를 가지며, 이는 "has many" 관계.
* TrainingManager 클래스는 Course 클래스로 가는 화살표를 가지며, 이는 "manages" 관계.
* Course 클래스는 Application 클래스로 가는 화살표를 가지며, 이는 "has many" 관계.
* Application 클래스는 Employee 클래스와 Course 클래스로 각각 화살표를 가지며, 이는 "belongs to" 관계.


교육 신청 관리 시스템 기본 설계서
<제 4–5> 기본 설계서의 항목
기본 설계서
문서관리 정보
* 문서명: 교육 신청 관리 시스템 기본 설계서
* 문서번호: EDU-MGMT-2023-001
* 작성일: 2023-11-29
* 작성자: 시스템 설계 팀
* 검토: QA 팀
* 승인: 프로젝트 관리자
  개요
* 목적: 조직 내 직원들이 필요한 교육을 쉽게 신청하고 추적할 수 있는 시스템을 구축하기 위함
* 유스케이스명: 교육 신청
* 액터명: 직원, 교육 매니저, 외부 교육 훈련 기관
  기능
* 주요 기능: 교육 신청, 신청 확인, 교육 과정 관리
* 선택 기능: 교육 과정 추천, 신청 취소, 교육 목록 수정 및 삭제
  UI
* 조작 방법: 웹 인터페이스를 통한 사용자 상호작용
* 관리 포털: 교육 매니저가 교육 과정을 관리하는 관리자 인터페이스
  시스템 구성
* 전체 구성: 클라이언트-서버 아키텍처
* SW 구성: 교육 신청 처리 모듈, 교육 과정 관리 모듈
* HW 구성: 서버 인프라, 사용자 접속을 위한 컴퓨팅 디바이스
  네트워크 구성
* 인터넷 접속: 조직 내부 네트워크 및 외부 인터넷 연결
* 보안 프로토콜: HTTPS, VPN을 통한 안전한 데이터 전송
  시스템 인터페이스
* 파일 교환: 데이터 교환을 위한 XML, JSON 파일 포맷
* 데이터 교환 스펙: RESTful API를 통한 클라이언트와 서버 간의 통신

