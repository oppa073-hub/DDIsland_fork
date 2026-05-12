<div align="center">

# 둥둥 아일랜드

창 크기와 호수 높이를 직접 조절할 수 있는  
데스크톱 위젯형 방치 게임

</div>

---

## 프로젝트 소개

둥둥 아일랜드는 곰 캐릭터가 상태값에 따라  
낚시, 식사, 수면, 요리, 판매를 반복하는  
데스크톱 위젯형 방치 게임입니다.

플레이어는 자율행동으로 얻은 자원을 활용해  
섬과 호수를 꾸미고, 퀘스트와 저장 시스템을 통해  
자신만의 작은 공간을 만들어갈 수 있습니다.

 <img width="847" height="476" alt="image" src="https://github.com/user-attachments/assets/e295f519-9fc6-469e-8ac5-c8d3637e5907" />
 
## Links

<p align="center">
  <a href="https://www.youtube.com/watch?v=B22p13wO5OQ">
    <img src="https://img.shields.io/badge/YouTube-시연영상-red?style=for-the-badge&logo=youtube&logoColor=white"/>
  </a>
  &nbsp;
  <a href="https://devel-rocket.itch.io/doongdoongisland">
    <img src="https://img.shields.io/badge/Play-게임실행-2ea44f?style=for-the-badge&logo=unity&logoColor=white"/>
  </a>
</p>

---

## 개발 정보

- **엔진** : Unity 6000.3.5f2
- **언어** : C#
- **형태** : 포트폴리오 프로젝트
- **플랫폼** : Windows PC
- **개발 기간** : 2026.02.09 ~ 2026.04.08
- **개발 인원** : 기획: 7명  개발: 5명
- **핵심 구현** :
  - 상태패턴 기반 자율행동 AI
  - 낚시 → 창고 → 요리 데이터 파이프라인
  - 저장 데이터와 UI 표시 순서 분리
  - 퀘스트 진행도 누적 구조
  - UI / VFX 연출 구현

---

## 브랜치 전략

```mermaid
flowchart LR
    feature[feature/*<br/>기능 단위 작업] --> develop[develop<br/>통합 개발]
    develop --> release[release<br/>출시 준비]
    release --> main[main<br/>배포 기준]

    main --> mvp[MVP]
    mvp --> cbt[CBT]
    cbt --> obt[OBT]
    obt --> launch[출시]
```

- `main` : 배포 기준
- `release` : 출시 준비
- `develop` : 통합 개발
- `feature/*` : 기능 단위 작업
  
---

## 주요 기능

### 1. 자율행동 AI

상태값을 기준으로 다음 행동을 선택하도록 구성했습니다.

```mermaid
flowchart LR
    C[행동 재계획]
    C --- I[대기 상태]
    C --- M[이동 상태]
    C --- F[낚시 상태]
    C --- K[요리 상태]
    C --- E[식사 상태]
    C --- S[수면 상태]
```

- Idle / Move / Fishing / Eat / Sleep / Cook 상태 분리
- 배고픔, 스태미나, 보유 자원 조건에 따라 행동 전환
- 예외 상황에서도 루프가 끊기지 않도록 생존 흐름 유지
 
<img width="800" height="450" alt="ezgif-265a0a71318c51d1" src="https://github.com/user-attachments/assets/e7ea4aa2-091b-4e2b-964d-81d6e5d7d075" />---

---

### 2. 낚시 시스템

기본 행동 상태에서는 낚시를 반복 수행하며  
환경 조건에 따라 후보 어종을 선택합니다.

- 환경 정보를 기준으로 후보 어종을 추립니다
- 후보군에 가중치를 적용해 최종 어종을 선택합니다
- 선택된 결과는 저장 시스템으로 전달됩니다

```mermaid
flowchart LR
    A[날씨 / 계절 / 시간 / 장소<br/>현재 환경 정보]
    B[FishManager<br/>낚시 환경 정보 구성]
    C[후보 어종 필터링<br/>출현 가능한 어종 추림]
    D[가중치 랜덤 선택<br/>조건 기반 확률 반영]
    E[저장 시스템 전달<br/>낚시 결과 저장]

    A --> B
    B --> C
    C --> D
    D --> E
```

---

### 3. 창고 시스템

<img width="507" height="399" alt="image" src="https://github.com/user-attachments/assets/fbce0538-dac5-43f1-b836-4ed6abd1f62e" />

물고기와 음식은 각각 별도 구조로 관리하고,  
데이터 변경이 화면에 안정적으로 반영되도록 구성했습니다.

- 물고기 / 음식 저장 구조 분리
- 획득 데이터와 제작 결과를 단계별로 전달
- 데이터 변경 시 UI 갱신 대응

```mermaid
flowchart LR
    A[FishManager<br/>낚시 결과 생성 / 획득 결과 전달]
    B[FishStorageManager<br/>물고기 저장 / 획득 데이터 관리]
    C[CookingManager<br/>보유 재료 확인 / 제작 가능 음식 판정]
    D[FoodStorageManager / UI<br/>완성 음식 저장 / 화면 갱신]

    A --> B
    B --> C
    C --> D

```

---

### 4. 요리 시스템

<img width="495" height="399" alt="image" src="https://github.com/user-attachments/assets/51f1952a-7db9-4070-b0f7-e0b08cb487ee" />

인벤토리와 레시피 해금 상태를 기준으로  
제작 가능한 음식 후보를 판정하도록 만들었습니다.

- 재료 보유 여부 검사
- 레시피 해금 여부 확인
- 제작 가능한 음식 후보 선정
- 완성 음식은 별도 저장소에 보관

```mermaid
flowchart LR
    A[ItemManager<br/>레시피 해금 여부 확인]
    B[FishStorageManager<br/>재료 / 부재료 보유 여부 전달]
    C[CookingManager<br/>제작 가능 음식 후보 판정]
    D[FoodStorageManager<br/>완성 음식 저장]

    A --> C
    B --> C
    C --> D
```

---

### 5. 퀘스트 시스템

<img width="668" height="452" alt="image" src="https://github.com/user-attachments/assets/d780d3d0-05f3-4332-a708-a1220ee5983b" />

퀘스트 진행도는 UI와 직접 연결하지 않고  
백그라운드에서 자동 누적되도록 구성했습니다.

- 조건 키 기반 진행도 누적
- 상태 판정과 UI 표시 분리
- 보상 수령 후 완료 처리

```mermaid
flowchart LR
    A[QuestConditionKey<br/>공통 조건 키]
    B[QuestManager<br/>진행도 누적 / 상태 판정]
    C[QuestPanel<br/>퀘스트 목록 UI]
    D[QuestSlot<br/>개별 퀘스트 표시]

    A --> B
    B --> C
    C --> D
```

- **QuestConditionKey** : 퀘스트 진행 조건을 구분하는 공통 기준
- **QuestManager** : 진행도 누적, 상태 판정, 완료 처리 담당
- **QuestPanel / QuestSlot** : 누적된 결과를 UI에 표시

---

### 6. UI / VFX 연출

DOTween / Pooling 기반으로 상태 변화와 보상 획득을  
플레이어가 바로 이해할 수 있도록 시각적으로 표현했습니다.

- 상태 이모지 / 말풍선
<img width="1080" height="211" alt="image" src="https://github.com/user-attachments/assets/5d475e80-ac33-47aa-808f-ec20973a1482" />

- 낚시 바늘 연출
<img width="543" height="171" alt="image" src="https://github.com/user-attachments/assets/d6ff6a96-1458-4bfd-ac5a-8a6df68cda63" />

- 보상 수렴 이펙트
<img width="800" height="450" alt="ezgif-16766a221cf6df7c" src="https://github.com/user-attachments/assets/ef57c1f6-bacc-4942-8f57-89525eb90bf9" />
---

---

### Commit 메시지 규칙

- Feat : 새로운 기능 추가
- Fix : 버그 수정
- Design : UI 디자인 변경
- HOTFIX : 치명적인 에러 긴급 수정
- Comment : 주석 추가 / 변경
- Docs : 문서 수정
- Style : 코드 포맷팅, 세미콜론 누락 등 코드 변경 없는 수정
- Refactor : 코드 리팩토링
- Test : 테스트 코드 추가 / 수정
- Chore : 빌드 설정, 패키지 매니저 수정
- Rename : 파일 / 폴더명 수정 및 이동
- Remove : 파일 삭제만 수행한 경우

---

### 프로젝트 폴더 관리 방

- 0.Scripts : 기능별 스크립트 관리
- 1.Prefabs : 프리팹 리소스 관리
- 2.Scenes : 씬 파일 관리
- 3.Animations : 애니메이션 관련 파일 관리
- 4.Materials : 머티리얼 리소스 관리
- 6.DataTable : CSV / 데이터 테이블 관리
