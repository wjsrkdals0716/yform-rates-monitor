# dashboard

공동 작업물이 들어가는 폴더이다. keeper만 수정한다. 지금은 비어 있고, 요청서가 반영되면서 아래 구조로 채워진다.

## 목표 구조

| 경로 | 역할 |
|---|---|
| `index.html` | 화면. 브라우저로 바로 열거나 GitHub Pages로 본다. |
| `assets/` | 화면용 CSS와 JavaScript |
| `build.py` | 공개 데이터를 받아 계산하고 `data/`에 결과를 쓴다. |
| `settings.py` | 비교 기간, 임계값 같은 설정값 |
| `tabs/` | 탭마다 한 파일의 계산식(`tab1_curve.py` 등) |
| `data/` | `build.py`의 결과. `index.html`이 `<script>` 태그로 읽으므로 `fetch` 없이 파일로 열어도 동작해야 한다. |
| `requirements.txt` | Python 패키지 목록 |

## 탭 구성 (연구계획서 기준)

| 탭 | 이름 |
|---|---|
| 1 | Yield Curve Monitor |
| 2 | Yield Decomposition |
| 3 | Treasury Auction Monitor |
| 4 | Treasury Supply & Fed Balance Sheet |
| 5 | Monetary Policy & Money Market |
| 6 | Curve Positioning & RV |
| 7 | Portfolio & Risk Analytics |
| 공통 | Market Event Calendar |

단위와 데이터 원칙은 `RULES.md` 8장을 따른다.
