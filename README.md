# 이기안 · Unity Game Client Developer

- [About me](#about-me-wave)
- [CV](#cv-page_facing_up)
- [My projects](#my-projects-video_game)
  - PhikozzLib · Unity 공통 시스템 라이브러리
- [Experiences](#experiences-office)
  - 다락연구소 게임개발팀 팀장
  - KDT 실무형 Unity 게임개발자 양성과정 10기
- [Skills](#skills-computer)
- [Tools](#tools-wrench)
- [Education](#education-mortar_board)
- [Certificates](#certificates-trophy)
- [Contact](#contact-email)

<br>

## About me :wave:

멀티미디어학과에서 C, Java, Python 등 프로그래밍 언어를 전공하고 교양으로 영상과 그래픽 디자인을 공부했습니다. 
약 1년 동안 그래픽 디자인을 배우고 실무를 경험했습니다. 이후, 예전부터 좋아했던 게임 개발에 관심을 가졌습니다. 
**2025년 KDT 실무형 Unity 게임개발자 양성과정을 수료**하며 게임 클라이언트 개발자의 길을 걷기 시작했고, 
부트캠프에서 함께 했던 동료들과 팀을 꾸려 8개월 동안 **팀장**으로 방치형 모바일 경영 게임 개발을 이끌었습니다. 
기획·개발·아트·QA 역할을 나누어 일하며 **소통**과 **협업 능력**, **문제 해결 능력**을 키웠습니다. 
이 포트폴리오에서는 제가 게임 개발을 시작한 이후 만들어 온 프로젝트와 고민의 흔적을 공유하고자 합니다. 
저는 모르는 문제를 만나면 **끝까지 파고들어 해결하는 과정**을 즐기고, 
지금도 C++을 공부하며 꾸준히 배우고 있기 때문에 이 포트폴리오도 계속 성장할 것이라고 확신합니다.


<br>

## CV :page_facing_up:

- [이력서](https://docs.google.com/document/d/1uxPCsXqL5hqwR8u9WCTCkWsBmGaHTJDUQ0Y8ST4fz3E/edit?usp=sharing)
- [자기소개서](https://docs.google.com/document/d/1xyPpdqSHFGsqzriSjePfg78zeT5tjW-mO_A5Y12_vIY/edit?usp=sharing)

<br>

## My projects :video_game:

### ▶ 개인 프로젝트 / PhikozzLib · Unity 공통 시스템 라이브러리
> 2026.05 – 2026.10 · 1인 개발 · UPM git 패키지 v3.0.0 · Unity 6 / C#

프로젝트마다 Audio, UI, Save 매니저를 다시 만들고, 매니저마다 접근 방식이 다르고, Awake 실행 순서 때문에 null 예외가 나던 문제를 해결하려고 만든 **Service Locator + Bootstrap 기반 공통 서비스 라이브러리**입니다.

* [GitHub 저장소](https://github.com/Leekiahn/PhikozzLib)
* [포트폴리오](https://docs.google.com/presentation/d/12FSICnKrx-n7V37dvNeFoc9VyhWKlU0RiVw-PG9e_j8/edit?usp=sharing)

**구성**
* 서비스 12종 · Addressable, Audio, UI, Effect, Data, Event, Save, Scene, Time, Localization, FloatingText, Pooling
* 유틸리티 10종 · Camera, Singleton, StateMachine, Observable, Command, Stat, Drag, Feedback, DevLog, TrackedPool
* 에디터 검증 툴

**주요 구현**
* **Bootstrapper** · BeforeSceneLoad에 매니저를 생성하고 등록 → 초기화 → Ready 세 단계로 분리. 모든 `InitAsync()`를 `UniTask.WhenAll`로 동시에 기다린 뒤 `WaitUntilReadyAsync()`로 게임 코드에 준비 완료를 알림
* **Event** · `Dictionary<Type, Delegate>` 기반, owner가 파괴되면 자동으로 구독 해제, struct 제약으로 발행 시 박싱 없음
* **Addressable** · label 단위 캐시, 다운로드 크기를 먼저 확인해 필요할 때만 다운로드, 없는 키만 `WhenAll`로 병렬 로드
* **UI** · 팝업을 타입으로 관리하고 닫을 때 파괴 대신 비활성화해 재사용, 패드·키보드 포커스 복원
* **Save** · 결과를 `Success / NotFound / Corrupted`로 구분, 직렬화는 메인 스레드에서 확정하고 디스크 쓰기만 스레드 풀로
* **TrackedPool** · Unity ObjectPool에 활성 객체 추적(Stack + HashSet)을 더해 `ReleaseAll`과 이중 반납 방지
* **Stat** · Flat → PercentAdd → PercentMult 순서로 계산, 지속시간 Modifier는 UniTask로 대기 후 finally에서 반드시 제거

**트러블슈팅**
* 매니저끼리 참조할 때 Awake 순서에 따라 아직 등록되지 않은 서비스를 조회해 예외가 발생 → 등록(`IServiceRegister`)과 초기화(`IServiceInit`)를 인터페이스로 분리하고, 다른 서비스 조회는 모든 등록이 끝난 뒤 `InitAsync()`에서만 하도록 해결

<br>

## Experiences :office:
 
**다락연구소 게임개발팀 팀장** · 2025.10 – 2026.06
* 팀 프로젝트 / **꿈결 장난감 공방** · 방치형 모바일 경영 게임 개발 (8개월)
  * 기획·개발·아트·QA 역할 분담 및 개발 파이프라인 구성
  * 기획자와 협업하여 시스템 기획 지원
  * 전반적인 팝업 UGUI 및 상호작용, 애니메이션 구현
  * BG Database · Google Sheets를 통한 전반적인 Data 관리
  * Customer Pooling 및 State Machine, Override Animator Controller 구현
  * ToyStand & Customer Sorting Group 관리

<br>

**KDT 실무형 Unity 게임개발자 양성과정 10기** · 2025.04 – 2025.08
* 팀 프로젝트 / **궁야 : 폐궁의 밤** · 1인칭 공포 어드벤처 게임 개발 및 Itch.io 배포
  * **플레이어 FSM** · 제네릭 `StateMachine<T>`로 Idle·Walk·Sprint·Crouch·Jump·Dead 상태 분리
  * **이동** · 이동 속도 등 수치를 ScriptableObject로 분리, Raycast로 머리 위 장애물 인식
  * **UI** · 메뉴·설정·인벤토리 등 전반적인 UGUI 패널 전환
  * **사운드** · Raycast로 바닥 머티리얼을 감지해 재질별 Footstep 사운드 재생
  * [Itch.io에서 플레이](https://phikozz.itch.io/nightpalace) · [플레이 영상](https://www.youtube.com/watch?v=2b0pwozoTho) · [GitHub 저장소](https://github.com/Leekiahn/NightPalace)
* 팀 프로젝트 / **Project Starfall** · 탑다운 우주 생존 게임 개발
  * **주야 변화** · 게임 내 시간에 따라 낮·밤 상태를 State 패턴으로 전환, 조명 세기와 Fog of War 농도를 부드럽게 보간
  * **엔딩 분기** · `IEnding` 인터페이스로 엔딩별 조건과 연출을 분리, 생존 일수에 따라 3가지 엔딩으로 분기 및 엔딩 영상 재생
  * [플레이 영상](https://www.youtube.com/watch?v=zdOKez8kJ-A)

<br>

## Skills :computer:

* [UniTask](https://github.com/Cysharp/UniTask) - async/await 기반 비동기 처리
* Addressables - label 단위 리소스 로드·해제와 원격 번들 다운로드
* BG Database - 구글 스프레드시트와 연동해 기획 데이터를 코드 수정 없이 반영
* ScriptableObject - 아이템 등 게임 데이터 에셋 관리
* [Odin Inspector](https://odininspector.com/) - 인스펙터 확장으로 에디터 작업 효율화
* Input System - 키보드·게임패드 입력 처리와 UI 포커스 제어
* UGUI - 팝업 UI와 상호작용 구현
* Animator - 2D·3D 애니메이션 상태 전환, Override Animator Controller로 애니메이션 교체
* Cinemachine - 상황에 맞는 카메라 전환과 추적 제어
* [Feel](https://feel.moremountains.com/) - 사운드, 파티클, 카메라 흔들림, 애니메이션 등 게임 피드백 연출
* FMOD for Unity - 적응형 오디오 구현
* Localization - 다국어 텍스트와 에셋 관리
* MCP for Unity - Claude Code와 Unity 에디터 연동

**개인 학습 저장소**
> 자료구조, 알고리즘, 네트워크, 디자인 패턴을 개인적으로 학습하며 직접 구현하고 정리한 저장소입니다.
 
* [Unity-Design-Patterns](https://github.com/Leekiahn/Unity-Design-Patterns) - Singleton, State, Strategy, Template Method, Observer, Factory Method, Facade, Dependency Injection, Decorator, Command, Adapter 11가지 패턴을 Unity 예제로 구현
* [SortingAlgorithm](https://github.com/Leekiahn/SortingAlgorithm) - 버블·삽입·선택·퀵·병합·힙 정렬 6종을 오름차순·내림차순으로 구현하고, 무작위 정수 10,000개로 소요 시간 비교
* [Graph-Data-Structure](https://github.com/Leekiahn/Graph-Data-Structure) - 인접 행렬, 인접 리스트, 가중치 그래프 구현 (방향·무방향 지원, 정점 범위 검증 유틸 분리)
* [Pathfinding-Algorithm](https://github.com/Leekiahn/Pathfinding-Algorithm) - DFS(스택), BFS(큐), Dijkstra(우선순위 큐), A*(휴리스틱 함수 주입) 경로 탐색 구현
* [TCP-IP-Programming](https://github.com/Leekiahn/TCP-IP-Programming) - TcpListener와 TcpClient로 서버-클라이언트 메시지 송수신 구현


<br>

## Tools :wrench:
 
* Unity - 게임 엔진
* C# - 주 개발 언어
* C++ - 서브 개발 언어
* Visual Studio Code · Rider · Visual Studio 2022 - 코드 작성과 디버깅
* Notion - 개발 일정 관리와 기획 문서 정리
* Figma - 팀원과 함께 화면 구성과 기획 협업
* Slack · Discord · ZEP - 팀 커뮤니케이션
* Git - 소스 코드 버전 관리
* GitHub - 원격 저장소 관리와 협업, UPM 패키지 배포
* Claude Code - AI 코딩 도구로 개발 생산성 향상

<br>

## Education :mortar_board:

* 숭실대학교 글로벌미래교육원 멀티미디어학과 졸업 (전문학사) · 2022.12
* 아현산업정보학교 방송영상과 수료 · 2019.02
* 남강고등학교 졸업 · 2019.02

<br>

## Certificates :trophy:

* 컴퓨터활용능력 2급 · 2023.05
* 네트워크관리사 2급 · 2020.01
* 정보기술자격(ITQ) · 2018.08
* 그래픽기술자격(GTQ) 1급 · 2018.06

<br>

## Contact :email:
 
* Email · kiahn2000@gmail.com
* Blog · [https://phikozz.tistory.com/](https://phikozz.tistory.com/)
