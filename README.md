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

<img width="772" height="342" alt="image" src="https://github.com/user-attachments/assets/85dc4d4f-46c0-4bde-9e11-20bb239a6536" />

- **Main** : 배포 기준
- **release** : 출시 준비
- **develop** : 통합 개발
- **feature** : 기능 단위 작업
  
---

## 주요 기능

### 1. 자율행동 AI
상태값을 기준으로 다음 행동을 선택하도록 구성했습니다.

<img width="770" height="815" alt="image" src="https://github.com/user-attachments/assets/1dcba667-0a07-4951-afbf-abf8bf6a8865" />

- Idle / Move / Fishing / Eat / Sleep / Cook 상태 분리
- 배고픔, 스태미나, 보유 자원 조건에 따라 행동 전환
- 예외 상황에서도 루프가 끊기지 않도록 생존 흐름 유지
 
<img width="800" height="450" alt="ezgif-265a0a71318c51d1" src="https://github.com/user-attachments/assets/e7ea4aa2-091b-4e2b-964d-81d6e5d7d075" />---

### 2. 낚시 시스템

기본 행동 상태에서는 낚시를 반복 수행하며  
환경 조건에 따라 후보 어종을 선택합니다.

- 환경 기반 후보군 선정
- 낚시 결과 생성
- 저장 시스템으로 결과 전달

<img width="1754" height="790" alt="image" src="https://github.com/user-attachments/assets/8d76ed4f-8b94-457f-be1c-f096201c71ad" />

---

### 3. 창고 시스템

<img width="507" height="399" alt="image" src="https://github.com/user-attachments/assets/4137a882-d78d-4445-a4d1-419914835986" />

물고기와 음식은 각각 별도 저장 구조로 관리하고,  
화면에 보이는 순서도 따로 계산하도록 구성했습니다.

- 실제 저장 배열 유지
- 정렬 결과만 화면에 표시
- 정렬 / 필터 / 선택 유지 대응

<img width="1742" height="591" alt="image" src="https://github.com/user-attachments/assets/7836bc96-73ad-4646-9ea6-c8063b67feb7" />

---

### 4. 요리 시스템

인벤토리와 레시피 해금 상태를 기준으로  
제작 가능한 음식 후보를 판정하도록 만들었습니다.

- 재료 보유 여부 검사
- 레시피 해금 여부 확인
- 제작 가능한 음식 후보 선정
- 완성 음식은 별도 저장소에 보관

<img width="1795" height="569" alt="image" src="https://github.com/user-attachments/assets/ff6b8bb9-ed5b-4129-8a41-c8cd404aa7a4" />

---

### 5. 퀘스트 시스템

퀘스트 진행도는 UI와 직접 연결하지 않고  
백그라운드에서 자동 누적되도록 구성했습니다.

- 조건 키 기반 진행도 누적
- 상태 판정과 UI 표시 분리
- 보상 수령 후 완료 처리

<img width="1726" height="738" alt="image" src="https://github.com/user-attachments/assets/fe187ac6-5a2b-4340-8efa-13a0e1477e83" />

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
