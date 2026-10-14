/daily-files로 받은 최신 기준일 폴더의 xlsx 2개에서 Stellest 지표를 계산해 보고한다.

입력 폴더: %USERPROFILE%\Documents\Stellest_Daily\YYYY-MM-DD\ 중 기준일이 가장 최근인 폴더 (인자로 날짜를 주면 그 폴더)
- Daily Order InTake Report _YYYY_MM(공유용).xlsx -> 주문 기준
- Daily Sales Report_YYYY_MM(공유용).xlsx -> 인보이스(순매출) 기준

## 공통 규칙
- 나는 Stellest 매니저다. 두 파일 모두 Stellest 제품 수량만 본다. 제품/브랜드 구분 컬럼을 찾아 Stellest만 필터하고, 어떤 컬럼·값으로 필터했는지 보고한다.
- 두 파일은 월 단위 일별 누적본이다. 기준일은 파일의 마지막 데이터 날짜이며 폴더명과 같은지 확인한다.
- 기간 표기는 YTD / MTD / 1Q·2Q·3Q·4Q를 쓴다. 이 보고는 MTD(해당 월 1일~기준일)다.
- 컬럼 구조가 처음 보는 형태이거나 위 필터·집계를 확정할 수 없으면 추측하지 말고 컬럼 목록과 샘플 3행을 보여 주고 나에게 물어본다.

## 계산할 지표
1. 이달 Stellest 수량 달성률 (MTD)
   - 달성률 = 세일즈 파일의 MTD Stellest 순매출 수량 / 월 목표 수량
   - 일별 누적 수량 추이도 함께 만든다 (월 목표선과 비교용).
2. 수량 대비 목표
   - MTD 실적(pcs), 월 목표(pcs), 잔여 수량(pcs) = 월 목표 - MTD 실적
   - 월말 마감 예상 = MTD 실적 / 경과 영업일 x 해당 월 영업일. 근거 수식을 같이 적는다.
3. 오더링 어카운트
   - 정의: 해당 월(MTD)에 Stellest를 한 번이라도 주문한 고객 계정 수 (중복 제거).
   - 추출 파일: 박정은 부장이 보낸 Daily Order InTake Report xlsx (SIS 값에 의존하지 않고 이 파일에서 직접 센다).
   - 고객 계정 식별 컬럼(고객코드 등)을 보고하고, 주문 수량이 0 이하(취소 등)인 행은 제외한다.
   - 전일 대비 증가분도 함께 적는다.

## 월 목표 (2026, pcs, 인보이스·순매출 기준 — SIS 대시보드 월별 상세 표의 「목표」 열)
| 1월 | 2월 | 3월 | 4월 | 5월 | 6월 | 7월 | 8월 | 9월 | 10월 | 11월 | 12월 | 연간 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 3,240 | 4,320 | 4,860 | 4,320 | 4,860 | 3,780 | 4,320 | 5,400 | 5,400 | 4,320 | 4,320 | 4,860 | 54,000 |

- 목표는 인보이스(순매출) 기준이다. 주문 수량과 비교하지 않는다. 달성률은 반드시 세일즈 파일 수량으로 계산한다.
- SIS 대시보드: https://claude.ai/artifact/Vurr6Aavqh6ht8U48W35yM (상단 「순매출」 카드와 「매출 추이」 > 「월별 상세」 표에서 확인)
- 원본은 Master 엑셀의 「목표 진척률(2026)」 시트다. 목표가 바뀌었을 수 있으니 SIS 대시보드의 월별 상세 표 값과 다르면 SIS 값을 따르고 알려 준다.

## 출력
1. 위 세 지표를 표로 보고한다 (결론을 먼저, 근거를 나중에). 공식적인 톤으로 쓴다.
2. 같은 기준일 폴더에 summary.csv로 저장한다. 컬럼: date, stellest_sales_pcs_mtd, monthly_target_pcs, achievement_rate, remaining_pcs, projected_month_end_pcs, stellest_order_pcs_mtd, ordering_accounts_mtd
3. 파일을 삭제하거나 덮어써야 하면 먼저 나에게 물어본다.
4. 출근 대시보드(https://claude.ai/artifact/7VqUbbsUgP3rkLxX2WBHx8) 자동 반영은 아직 연결 전이다. 이 명령은 summary.csv 저장까지만 한다.
