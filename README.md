# AVaOut: Avatar Out — QA 추적 저장소

**AVaOut: Avatar Out** (UE 5.6 / Listen Server / 최대 4인 협동 멀티플레이) 게임의 QA 버그 추적 및 패치 관리 저장소다.  
게임 소스 코드는 별도 저장소에서 관리하며, 이 저장소는 QA 테스트 케이스 목록과 버그별 수정 패치 파일을 보관한다.

---

## 저장소 구성

| 파일/디렉토리 | 설명 |
|---------------|------|
| `QAListup.md` | 전체 QA 테스트 케이스 목록 (18개 카테고리) |
| `CLAUDE.md` | AI 코드 어시스턴트용 프로젝트 가이드 |
| `*.patch` | 버그별 수정 diff 파일 |

---

## 패치 파일 목록

### 인게임 버그 (B-XXX)

| ID | 패치 파일 | 설명 |
|----|-----------|------|
| B-001 | `B-001_CreateSessionBtn_NotWork.patch` | CreateSession 버튼이 동작하지 않는 현상 수정 |
| B-002 | `B-002_Cannot_Jump.patch` | Jump가 되지 않는 현상 수정 |
| B-003 | `B-003_Cannot_Crouch.patch` | Crouch가 되지 않는 현상 수정 |
| B-004 | `B-004_Cannot_Sprint.patch` | Sprint가 현재 스태미너와 상관없이 불가능한 현상 수정 |
| B-005 | `B-005_ItemPickup_Crash.patch` | 아이템이 4개인 상태에서 아이템 습득 시 크래시 수정 |
| B-006 | `B-006_TrainDoor_NotWork.patch` | TrainDoor가 상호작용 되지 않는 현상 수정 |
| B-007 | `B-007_Monster_Cannot_Attack.patch` | 몬스터가 플레이어를 인식했음에도 공격하지 않는 현상 수정 |
| B-008 | `B-008_Cannot_Hit_After_Hit.patch` | 플레이어가 피격 후 영구적으로 피격이 되지 않는 현상 수정 |
| B-009 | `B-009_Cannot_Death.patch` | 플레이어가 HP가 0이 되어도 사망하지 않는 현상 수정 |
| B-010 | `B-010_Multi_Cannot_Interact.patch` | 멀티플레이에서 상호작용이 되지 않는 현상 수정 |
| B-011 | `B-011_PlayerDeathCount_Different_Rarely.patch` | 간헐적으로 사망 시 다른 클라이언트에 사망 카운트가 반영되지 않는 현상 수정 |
| B-012 | `B-012_Monster_FootStepSound_CannotHear.patch` | 몬스터 이동 시 발자국 사운드가 들리지 않는 현상 수정 |
| B-013 | `B-013_Multi_Cannot_Customize.patch` | 로비에서 캐릭터 외형을 변경해도 적용되지 않는 현상 수정 |
| B-014 | `B-014_Multi_CannonShoot_No_Sound&Effect.patch` | 대포 발사 시 이펙트/사운드가 클라이언트에서 보이지 않는 현상 수정 |
| B-015 | `B-015_Multi_Cannot_Play_InteractAnimMontage.patch` | 상호작용 시 애니메이션 몽타주가 재생되지 않는 현상 수정 |

### 에디터 전용 버그 (E-XXX)

| ID | 패치 파일 | 설명 |
|----|-----------|------|
| E-001 | `E-001_EditorOnly_Crash.patch` | PIE Join 시 동작 안 함 및 간헐적 크래시 현상 수정 |
| E-002 | `E-002_EditorOnly_EternalLoading_Map.patch` | E-001 적용 이후 메인 맵 이동 시 무한 로딩 현상 수정 |

---

## 패치 적용 방법

게임 소스 저장소 루트에서 아래 명령을 실행한다.

```bash
# 패치 적용
git apply <패치파일경로>

# 예시
git apply ../QA_Project/B-011_PlayerDeathCount_Different_Rarely.patch
```

---

## 버그 ID 및 커밋 규칙

**파일명**: `<ID>_<짧은_설명>.patch`

**커밋 메시지**:
```
fix: B-011 간헐적으로 플레이어 사망 시 다른 클라이언트에 사망 카운트가 반영되지 않는 현상 수정
```

| 접두사 | 대상 |
|--------|------|
| `B-XXX` | 인게임 버그 |
| `E-XXX` | 에디터 전용(PIE/Editor) 버그 |

---

## QA 테스트 케이스

`QAListup.md`에서 18개 카테고리, 우선순위(P1~P4) 기준 전체 테스트 케이스를 확인할 수 있다.

| 카테고리 | 주요 내용 |
|----------|-----------|
| 세션 / 온라인 매칭 | 방 생성·참가·호스트 이탈 처리 |
| 음성 채팅 | 뮤트, 레벨 이동 후 유지 |
| 캐릭터 이동 & 트래버설 | 걷기/달리기/크라우치/파쿠르 동기화 |
| GAS — 플레이어 어빌리티 | 어빌리티 발동, 쿨다운, 속성 동기화 |
| 전투 | 근접 히트 판정, 사망 처리 |
| 인벤토리 & 아이템 | 습득·사용·드롭·레벨 이동 유지 |
| 패시브 아이템 | 패시브 효과 중첩 및 초기화 |
| 연료(Train) 시스템 | 연료 추가·감소·동기화 |
| 상호작용 시스템 | 동시 상호작용, Hold 취소 |
| 퍼즐 시스템 | OneTime/Toggle/HoldToggle, 협동 퍼즐 |
| AI 행동 (StateTree) | 탐지·추적·공격·특수 AI 행동 |
| 부활 시스템 | 부활 횟수 차감, 전원 사망 처리 |
| 게임 흐름 & 레벨 이동 | Stage → Rest → 결과 흐름 |
| 커스터마이징 (Mutable) | 멀티플레이 외형 동기화 |
| UI | HUD, 인벤토리, 스펙테이터 위젯 |
| 게임 설정 | 그래픽·음량·키 바인딩 저장 |
| 벤딩머신 / 상점 | 구매, 재화 부족, 동시 구매 |
| 네트워크 엣지 케이스 | 레이턴시, 패킷 손실, 호스트 이탈 정책 |
