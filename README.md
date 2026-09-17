# 홈런 클래시2 모작 (HomeRunClashCopy)

『홈런 클래시 2』를 모작한 캐주얼 야구 액션 게임

**Unreal Engine 5.5** · C++ · Blueprint<br>
UE 클라이언트 3인 · 개발 기간 4주 · 약 20명 대상 빌드 플레이테스트

[시연 영상](https://youtu.be/WMB95wu5jro) · [Notion](https://app.notion.com/p/349e6578029f800e9a24c25058154ff1)

## 게임 소개

투수가 던진 공을 타격해 홈런을 노리는 홈런더비 방식의 캐주얼 야구 게임입니다.
타이밍과 히팅 포인트에 따라 타구의 발사각과 비거리가 달라지고, 홈런 성공 횟수와
잔여 공에 따라 스테이지 클리어와 실패가 결정됩니다.

## 주요 구현

**공 시뮬레이션 · 맵 기믹 · 랭킹** — [@Jiwoong617](https://github.com/Jiwoong617)

- 중력 · 마그누스 효과 · 공기저항을 합산한 공 이동과 반사 벡터 기반 충돌 처리
- Straight · Curve · Slider · Fork · ChangeUp · Knuckle 6종 구종 시뮬레이터
- Fracture 기반 홈런 구조물(조각상 · 전광판) 파괴 연출과 관중 함성 사운드
- Firebase REST API 연동 온라인 랭킹과 닉네임 입력

**타격 판정 · 인게임 카메라** — [@ykd-yang](https://github.com/ykd-yang)

- 타이밍 · 히팅 포인트(상하 · 좌우) · 파워로 발사각과 타구 속도 · 방향 결정
- atan2 기반 각도 계산과 ±43° Clamp를 적용한 파울 방지 보정
- 스윗스팟 임계값 기반 크리티컬 판정과 임팩트 순간 시간 감속 연출
- CameraRigRail과 레벨 시퀀스를 이용한 타구 추적 인게임 카메라
- Fresnel을 활용한 캐릭터 외곽선 강조

**게임 시스템 · UI** — [@yeomin-yoon](https://github.com/yeomin-yoon)

- 공기저항의 속도 제곱 비례 특성을 참고해 단순화한 Curve 기반 감속 함수 (C++ · Blueprint에서 사용)
- GameMode 상태 전환 기반 경기 진행 흐름과 점수 산정
- GameInstance를 경유한 메인메뉴 아이템 선택 정보의 인게임 전달
- 미션 · 콤보 · 예고홈런 · 타격 판정 · 비거리 · 승패 UI와 애니메이션, 인트로 카메라 연출

## 개발 환경

Unreal Engine 5.5 · C++ · Blueprint · Firebase (Realtime Database REST API)

## 프로젝트 열기

1. Unreal Engine 5.5와 C++ 빌드 환경을 준비합니다.
2. Git LFS를 설치한 환경에서 저장소를 복제하고 `git lfs pull`로 LFS 에셋을 내려받습니다.
3. `HomeRunClashCopy.uproject`에서 Visual Studio 프로젝트 파일을 생성하고, 생성된 솔루션을 `Development Editor` 구성으로 빌드합니다.
4. 프로젝트를 열고 `Content/Map/GameLevel/StartLevel`에서 플레이합니다.

엔진 버전과 시작 맵은 저장소 설정을 기준으로 작성했습니다. 새 환경에서의 빌드·실행과 외부 Firebase 서비스의 현재 동작 여부는 별도로 검증하지 않았습니다.
