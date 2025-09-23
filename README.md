# football-transfer-data-analysis

`notebooks/football_transfer_analysis.ipynb` 노트북은 축구 선수 이적시장 데이터를 기반으로 선수·클럽 가치와 주요 스탯을 탐색하는 분석 워크플로우입니다. 데이터 로딩부터 시각화, 웹 스크래핑을 통한 스탯 보강까지 전 과정을 한 파일에서 재현할 수 있도록 구성되어 있습니다.

## 데이터셋
- `data/players.csv`: 선수 기본 정보 (소속, 포지션, 생년월일 등)
- `data/player_valuations.csv`: 선수별 연도·시즌별 시장가치 기록
- `data/clubs.csv`: 클럽 메타 정보와 시즌별 지표 (스쿼드 규모, 평균 연령 등)
- `data/competitions.csv`: 대회(리그) 메타 정보

노트북은 `data/` 또는 상위 디렉터리의 `data/` 폴더를 자동 감지해 파일을 불러옵니다.

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

## 주요 분석 하이라이트
- 연령대별 평균 시장가치를 히스토그램과 주석으로 확인하고, 특정 나이의 최고가 선수를 표시합니다.
- 포지션/세부 포지션별 시장가치가 시즌에 따라 어떻게 변화하는지 라인차트로 추적합니다.
- 국가·리그·클럽 단위에서 선수 수와 총 시장가치를 비교해 강력한 시장을 식별합니다.
- 상관행렬을 통해 시장가치와 강하게 연관된 스탯을 추출하고, 상위 5개 지표 vs. 시장가치를 포지션별로 시각화합니다.
- 특정 선수(예: Kylian Mbappé)를 중심으로 비슷한 시장가치 구간의 선수들과 주요 스탯을 비교합니다.

## 실행 방법
1. Python 3.9+ 가상환경을 권장합니다.
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install --upgrade pip
   pip install jupyter pandas numpy matplotlib seaborn plotly selenium beautifulsoup4
   ```
2. Jupyter Lab/Notebook 실행 후 노트북을 엽니다.
   ```bash
   jupyter lab
   ```
3. Plotly 시각화는 기본적으로 브라우저 렌더러(`renderer="browser"`)를 사용하므로, 실행 환경에 기본 브라우저가 열릴 수 있습니다.
4. Selenium 스크래핑 셀을 실행하려면 ChromeDriver 등 브라우저 드라이버를 설치하고, 경로를 환경 변수에 등록해야 합니다. 네트워크 접속이 필요한 셀이므로 환경에 맞춰 허용 여부를 확인하세요.

## 폴더 구조
```
football/
├─ data/
├─ figures/
└─ notebooks/
   └─ football_transfer_analysis.ipynb
```

## 참고
- 노트북 실행 전 `data/` 디렉터리와 CSV가 최신 상태인지 확인하세요.
- Plotly 및 Selenium 셀은 대화형/외부 의존성이 있어 자동 배포 환경에서는 건너뛰어도 됩니다.
- 분석을 재현하면서 발견한 추가 인사이트나 개선 사항은 Pull Request로 자유롭게 공유해 주세요.
