# 🎯스팟파이어 핵심 구성 요소

`원본 데이터에서 필요한 것만 추려서 시각화한다`

## 1. 데이터 테이블

데이터의 원본

## 2. 필터 및 마킹

시각화에 사용할 데이터의 범위 지정

## 3. 집계 및 시각화

대표값을 산출하고 시각화

### 3.1 집계함수들

- **집계 방식** : color, marker, trelis 등 사용된 축들을 모두 모아 구성된 그룹별로 집계함.
  Catergorial과 continous : --설명 추가하기--
- **주요 집계 함수들** : Average, Median, Stddev, Percentile, Max, Min, Count, First, Last, Concat, UniqueConcatenate

# 📑 각 요소 별 핵심 기능 및 사용법

## 1. 데이터 테이블

### 1.1 데이터 로드

- **데이터 소스** : local file, EDM, clipboard, 타 데이터 테이블
- **행 속성 지정** : name row, type row, data row (다중 컬럼 지원, refresh 눌러서 업데이트)
- **열 이름 변경 및 타입 지정**
  - `데이터 타입 지정` : 텍스트, 숫자, 날짜
  - `열 이름` : 상단 더블 클릭 후 수정

### 1.2 데이터 파이프라인

- **행 추가** : 컬럼 매치, 추가할 컬럼, origin 컬럼
- **열 추가** : key column 선택, join 방법 선택, 추가할 컬럼 선택
  - `Left outer join` : 왼쪽 데이터 테이블 기준, 다중 행 있을 시 확장
  - `Left single match join` : 왼쪽 데이터 테이블 기준, 첫번째 매치 행만 반영
  - `Right outer join` : 오른쪽 데이터 테이블 기준, 다중 행 있을 시 확장
  - `Right single match join` : 오른쪽 데이터 테이블 기준, 첫번째 매치 행만 반영
  - `Inner join` : 양쪽 데이터 테이블에 모두 존재하는 데이터, 다중 행 있을 시 확장
  - `Full outer join` : 양쪽 데이터 테이블에 모두 존재하는 데이터, 각각 상대에서 없는 행일 경우 그쪽은 비워두고 확장
- **데이터 변환**
  파이프라인 내에서 원본 데이터를 수정할 수 있음
  - `기존 컬럼 변환`
  - `새로운 컬럼` : Column Properties와의 차이점은 **다른 파이프라인에서 참조 가능**
  - `타입 변경`
  - `컬럼 이름 변경`
  - `Pivot`
  - `Unpivot`

## 2. 필터 및 마킹

- **필터** : 데이터 테이블의 데이터를 필터링하는 기능, `Add Filter`를 클릭하여 필터 추가, 드롭다운 메뉴에서 `Add Filter`를 클릭하여 필터 추가
  - `Fitering Scheme` : 필터 조건을 저장할 수 있는 기능. 대시보드 시 페이지 별 필터 분기 가능
  - `Organize Filters` : 필터링 스킴에 표시할 컬럼들 지정 가능
  - `Active Filters` : 현재 사용 중인 필터
- **마킹** : 데이터 테이블의 데이터를 마킹하는 기능, `Add Marking`을 클릭하여 마킹 추가, 드롭다운 메뉴에서 `Add Marking`을 클릭하여 마킹 추가
-
