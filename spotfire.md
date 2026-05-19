# 🎯스팟파이어 핵심 구성 요소

`원본 데이터에서 필요한 것만 추려서 시각화한다`

## 1. 데이터 테이블

데이터의 원본

## 2. 필터 및 마킹

시각화에 사용할 데이터의 범위 지정

## 3. 집계 및 시각화

대표값을 산출하고 시각화

### 3.1 집계함수들

#### 집계 방식

color, marker, trelis 등 사용된 축들을 모두 모아 구성된 그룹별로 집계함.

- Catergorial과 continous : --설명 추가하기--

#### 주요 집계 함수들

- Average, Median, Stddev, Percentile, Max, Min, Count, First, Last, Concat, UniqueConcatenate

---

# 📑 각 요소 별 핵심 기능 및 사용법

## 1. 데이터 테이블

### 1.1. 데이터 로드

#### 데이터 소스 : local file, EDM, clipboard, 타 데이터 테이블

#### 행 속성 지정 : name row, type row, data row (다중 컬럼 지원, refresh 눌러서 업데이트)

#### 열 이름 변경 및 타입 지정

- `데이터 타입 지정` : 텍스트, 숫자, 날짜
- `열 이름` : 상단 더블 클릭 후 수정

### 1.2. 데이터 파이프라인

#### 행 추가 : 컬럼 매치, 추가할 컬럼, origin 컬럼

#### 열 추가 : key column 선택, join 방법 선택, 추가할 컬럼 선택

- `Left outer join` : 왼쪽 데이터 테이블 기준, 다중 행 있을 시 확장
- `Left single match join` : 왼쪽 데이터 테이블 기준, 첫번째 매치 행만 반영
- `Right outer join` : 오른쪽 데이터 테이블 기준, 다중 행 있을 시 확장
- `Right single match join` : 오른쪽 데이터 테이블 기준, 첫번째 매치 행만 반영
- `Inner join` : 양쪽 데이터 테이블에 모두 존재하는 데이터, 다중 행 있을 시 확장
- `Full outer join` : 양쪽 데이터 테이블에 모두 존재하는 데이터, 각각 상대에서 없는 행일 경우 그쪽은 비워두고 확장

#### 데이터 변환 : 파이프라인 내에서 원본 데이터를 수정할 수 있음

- `기존 컬럼 변환`
- `새로운 컬럼` : Column Properties와의 차이점은 **다른 파이프라인에서 참조 가능**
- `타입 변경`
- `컬럼 이름 변경`
- `Pivot`
- `Unpivot`

## 2. 필터 및 마킹

### 2.1. 필터

데이터 테이블의 데이터를 필터링하는 기능, `Add Filter`를 클릭하여 필터 추가, 드롭다운 메뉴에서 `Add Filter`를 클릭하여 필터 추가

- `Fitering Scheme` : 필터 조건을 저장할 수 있는 기능. 대시보드 시 페이지 별 필터 분기 가능
- `Organize Filters` : 필터링 스킴에 표시할 컬럼들 지정 가능
- `Active Filters` : 현재 사용 중인 필터

### 2.2.마킹

데이터 테이블의 데이터를 마킹하는 기능, `Add Marking`을 클릭하여 마킹 추가, 드롭다운 메뉴에서 `Add Marking`을 클릭하여 마킹 추가

# Spotfire 1일차 교육 교안: 반도체 공정 데이터 분석 기초

> **코스 가이드:** 본 과정은 반도체 공정 엔지니어를 대상으로, Spotfire의 인메모리 아키텍처와 데이터 흐름을 이해하고, 현업에서 가장 핵심이 되는 마킹, 필터링 스키마 및 산점도(Scatter Plot)의 고급 집계 메커니즘을 마스터하는 것을 목표로 합니다.

---

## 📅 [1부] 데이터 탑재 및 빠른 플롯 시뮬레이션 (20분)

### 1. Spotfire UI 아키텍처 및 인메모리 개념

- **인메모리(In-Memory) 분석 플랫폼:** 원천 데이터(Excel, CSV, DB 등)를 직접 수정하지 않고, 데이터를 메모리에 통째로 올려 가상으로 가공 및 탐색합니다. 수백만 건의 대용량 데이터도 끊김 없이 실시간으로 제어할 수 있는 기반이 됩니다.
- **핵심 인터페이스 구조:**
  - **왼쪽 Data Panel:** 원천 데이터를 가져오고 컬럼의 성격(데이터 타입)을 규정하는 곳.
  - **가운데 Main Canvas:** 시각화(Plot)들이 배치되고 인터랙션이 일어나는 분석 공간.
  - **오른쪽 Filter Panel:** 데이터의 차원을 실시간으로 깎아내고 걸러내는 제어판.

### 2. 메인 공정 데이터 로드 및 타입 검증

1. `Files and data` (＋ 버튼) ➡️ `Browse local files` 클릭 후 `Main_Process_Data.csv` 선택.
2. **Import Settings 데이터 타입 검증 (필수):**
   - 문자형(String): `WAFER_ID`, `EQUIP_ID`, `CHAMBER_NO`
   - 숫자형(Real/Integer): `STEP_TIME`, `THICKNESS_UNI`, `YIELD`
3. 상단 `Data Canvas` 아이콘을 눌러 데이터가 최초 소스로부터 유입되는 시각적 파이프라인(History Line) 확인.

### 3. 초간단 Base Plot 생성 및 배치

- **목적:** 데이터 시각적 베이스캠프를 신속히 확보하여 Spotfire의 유기적 연동을 실험할 준비를 합니다.

1. 왼쪽 시각화 메뉴에서 **Scatter Plot**과 **Bar Chart**를 각각 클릭하여 화면을 분할 배치합니다.
2. **Scatter Plot 축 설정:** X축 = `STEP_TIME`, Y축 = `THICKNESS_UNI`
3. **Bar Chart 축 설정:** X축 = `EQUIP_ID`, Y축 = `Avg(YIELD)`

---

## 📅 [2부] 마킹 및 정교한 필터링 제어 (35분)

### 1. 데이터 마킹(Marking)의 본질

- **개념:** 마킹은 특정 데이터 집합을 '선택'하여 하이라이트하거나 다른 차트와 상호작용하게 만드는 Spotfire의 핵심 메커니즘입니다.
- **실습:** Scatter Plot에서 혼자 우상향으로 크게 튀어 있는 아웃라이어 점들(`THICKNESS_UNI` $\ge$ 4.5)을 마우스로 드래그합니다. 그 순간, 옆의 Bar Chart에서 해당 불량 웨이퍼들이 어느 설비(`EQUIP_ID`)에 분포되어 있는지 형광색으로 실시간 하이라이트(Details Visualization)되는 연동성을 눈으로 확인합니다.

### 2. 필터 정리 (Organize Filters)

- **개념:** 대용량 공정 데이터일수록 컬럼 수가 많아 필터 패널이 복잡해집니다. 분석에 직결되는 핵심 조건만 남겨 가독성을 확보해야 합니다.

1. 필터 패널 빈 곳 우클릭 ➡️ `Organize Filters` 선택.
2. 고유 키값인 `WAFER_ID` 등 불필요한 필터의 체크박스를 해제하여 숨김 처리합니다.
3. 마우스 드래그를 통해 주요 공정 조건 필터(`EQUIP_ID`, `CHAMBER_NO`)를 최상단으로 정렬합니다.

### 3. 고급 제어: Filtering Scheme 분리

- **개념:** 기본적으로 모든 페이지와 차트는 필터를 공유합니다. 그러나 "A 차트는 전체 흐름을 보고, B 차트는 특정 조건만 고정해서 대조"하고 싶다면 독립된 필터 시스템(Scheme)을 생성해야 합니다.

1. `File` ➡️ `Document Properties` ➡️ `Filtering Schemes` 탭으로 이동하여 `New` 버튼을 클릭, **"Chamber_C_Fixed"** 스키마를 생성합니다.
2. 화면의 **Bar Chart 우클릭** ➡️ `Properties` ➡️ `Data` 메뉴로 이동합니다.
3. `Filtering scheme` 항목을 방금 만든 **"Chamber_C_Fixed"**로 변경합니다.
4. 이제 오른쪽 필터 패널에서 해당 스키마를 선택해 `CHAMBER_NO = CH_C`로 고정하면, Scatter Plot은 전체 데이터를 보여주지만 Bar Chart는 오직 C 챔버의 수율 데이터만 독립적으로 투영합니다.

---

## ☕ [쉬는 시간] Refresh (10분)

---

## 📅 [3부] Scatter Plot의 집계 원리와 OVER 함수 심화 (45분)

### 1. Scatter Plot 집계 원리: 망원경 vs 현미경

Spotfire의 Scatter Plot은 축(Axis)에 집계 함수가 포함되었는지 여부와 `Marker By` 옵션에 따라 데이터를 완전히 다르게 표현합니다.

- **망원경 모드 (그룹화/집계 관점):**
  - `Marker By = EQUIP_ID` (범주형 컬럼 지정)
  - X축 / Y축에 `Avg()` 함수가 적용되는 순간, 데이터 테이블은 설비 단위로 `Group By`되어 화면에 점이 딱 설비 개수인 **3개**만 찍힙니다. (거시적 모니터링에 유용)
- **현미경 모드 (원천 행 관점):**
  - `Marker By = (Row Number)` (개별 행 지정)
  - 축에 집계 함수가 걸려 있더라도 무조건 원천 레코드 단위를 유지하므로, 숨겨져 있던 **18개의 점이 모두** 살아납니다. (미시적 이상치 추적에 유용)

### 2. 시각적 속성(Color, Shape) 추가 시 '세포 분열' 주의보

- **연산 우선순위 룰:** `Marker by` $\ge$ `Color by` = `Shape by`
- **주의사항:** 망원경 모드(`Marker By = EQUIP_ID`)로 인해 점이 3개로 뭉쳐진 상태에서 `Color by = CHAMBER_NO`를 지정하면, 점의 개수가 $3 \times 3 = 9\text{개}$로 불어납니다. Spotfire 내부 엔진이 색상을 다르게 칠하기 위해 그룹을 더 잘게 쪼개어 평균을 다시 계산하기 때문입니다.
- **해결책:** 의도치 않은 통계 왜곡이나 데이터 분열을 방지하려면 **`Marker by = (Row Number)`로 고정하고 분석을 시작**하는 것이 안전합니다.

### 3. 현업 치트키: Row 모드와 OVER 함수의 결합

- **분석 시나리오:** 점은 18개 웨이퍼 낱장으로 다 풀어서 보되, Y축 높이는 **"자신이 진행된 설비 및 챔버의 중앙값(Baseline)"**을 차감하여 각 챔버 고유의 편차를 정규화(Normalization)하고 싶을 때.
- **설정 방법:** `Marker by = (Row Number)` 지정 후 Y축에 아래의 사용자 지정 수식 입력:
  ```text
  [THICKNESS_UNI] - Median([THICKNESS_UNI]) OVER ([EQUIP_ID],[CHAMBER_NO])
  ```
