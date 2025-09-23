
# football-transfer-data-analysis

`notebooks/football_transfer_analysis.ipynb` 노트북은 축구 선수 이적시장 데이터를 기반으로 선수·클럽 가치와 주요 스탯을 탐색하는 분석 워크플로우입니다.
데이터 로딩부터 시각화, 웹 스크래핑을 통한 스탯 보강까지 전 과정을 한 파일에서 재현할 수 있도록 구성되어 있습니다.

## 데이터셋
- `data/players.csv`: 선수 기본 정보 (소속, 포지션, 생년월일 등)
- `data/player_valuations.csv`: 선수별 연도·시즌별 시장가치 기록
- `data/clubs.csv`: 클럽 메타 정보와 시즌별 지표 (스쿼드 규모, 평균 연령 등)
- `data/competitions.csv`: 대회(리그) 메타 정보

## 노트북 구성
1. **Import Data**: CSV 파일을 로드하고 기본 DataFrame을 준비합니다.
2. **Dataset Information**: `info()`, `head()`, 결측치/고유값/기초 통계량으로 데이터 품질과 스케일을 파악합니다.
3. **Handling DataFrame**: 선수-가치 데이터를 병합해 `players_with_val`을 만들고, 연도(`dateyear`)와 나이(`age`) 계산, 2022 시즌 필터링, 시장가치 순위 산출 등 전처리를 수행합니다.
4. **Visualization**: Matplotlib와 Plotly로 다음을 시각화합니다.
   - 전체 시장가치 분포(Boxplot) 및 나이대별 평균 가치
   - 포지션·세부 포지션별 연도별 가치 추이
   - 국가별 선수 수 및 가치 분포, 영국 도시 기준 지리적 분포 애니메이션
   - 2022 시즌 클럽별 총 시장가치 Treemap/Bar/Box 차트
5. **Data Scrapping**: Selenium과 BeautifulSoup으로 WhoScored.com 상위 5대 리그 스탯 테이블을 수집해 공격/미드필더/수비수 DataFrame과 매칭, 상관분석 및 Plotly 산점도·트렌드라인, 선수 비교 시각화까지 확장합니다.


