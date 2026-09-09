# Spotify Track Analytics

Exploratory and comparative analysis of **898,694 Spotify tracks**, examining how audio
characteristics such as energy, danceability, tempo, valence, acousticness, and
instrumentalness relate to track popularity.

The project follows a 3-phase analytics pipeline:

**Clean → Explore → Compare**

A dashboard preview is included alongside the analysis assets.

> **Data source:** The exact source/citation for `tracks.csv` is not documented in the
> supplied project files. Add the original dataset name and source URL here before
> publishing the repository. Do not claim a source that cannot be verified.

---

## Project structure

```text
spotify-track-analytics/
├── data/
│   ├── raw/                      # source tracks.csv (not committed)
│   └── processed/                # spotify_cleaned.csv / spotify.db (not committed)
├── notebooks/
│   ├── import_to_sql.ipynb
│   ├── Phase_1_Data_Cleaning.ipynb
│   ├── Phase_2_EDA.ipynb
│   └── Phase_3_Advanced_Analysis.ipynb
├── dashboard/
│   ├── Spotify_PowerBI_DataModel.xlsx
│   ├── Spotify_Dashboard_Theme.json
│   └── Spotify_Dashboard_BuildGuide.docx
├── Spotify_Dashboard_Preview.html
├── requirements.txt
├── .gitignore
└── README.md
```

---

## Dataset

**898,694 tracks · 16 columns**

| Column | Description |
|---|---|
| `track_id` | Track identifier |
| `name` | Track name |
| `track_artists` | Artist field |
| `genres` | Genre label(s) associated with the track |
| `popularity` | Track popularity score |
| `tempo` | Tempo in BPM |
| `energy` | Perceived intensity/activity |
| `key` | Musical key |
| `mode` | Major/minor modality |
| `time_signature` | Estimated time signature |
| `speechiness` | Presence of spoken words |
| `danceability` | Suitability for dancing |
| `valence` | Musical positivity |
| `acousticness` | Confidence the track is acoustic |
| `liveness` | Likelihood of a live recording |
| `instrumentalness` | Likelihood of containing no vocals |

---

## Pipeline

| Phase | Notebook | Purpose |
|---|---|---|
| 0 | `import_to_sql.ipynb` | Loads the cleaned dataset into SQLite |
| 1 | `Phase_1_Data_Cleaning.ipynb` | Checks duplicates/missing values, standardizes types, and handles nulls |
| 2 | `Phase_2_EDA.ipynb` | Explores distributions, correlations, and popularity/category patterns |
| 3 | `Phase_3_Advanced_Analysis.ipynb` | Compares audio profiles across popularity tiers |

### Recommended execution order

```text
Phase_1_Data_Cleaning.ipynb
        ↓
import_to_sql.ipynb
        ↓
Phase_2_EDA.ipynb
        ↓
Phase_3_Advanced_Analysis.ipynb
```

---

## Key findings

- **No individual audio feature strongly explains popularity.** The strongest observed
  linear relationship is instrumentalness with popularity at **r = -0.174**.
- **Energy and danceability are positively associated with popularity**, although their
  correlations are still weak (approximately **r = 0.114** and **r = 0.113**).
- **Instrumentalness and acousticness are negatively associated with popularity**
  (approximately **r = -0.174** and **r = -0.125**).
- **Tempo has almost no linear relationship with popularity** (**r = 0.021**).
  The 140–160 BPM range has the highest average popularity among the displayed tempo bands,
  but the differences are small.
- **Minor-key tracks have slightly higher average popularity** than major-key tracks
  (22.28 vs. 21.65), a small difference that should not be interpreted as a strong effect.
- In the genre analysis, some **less-common genre combinations** have higher average
  popularity after applying a 100-track minimum. Because the dataset stores combined genre
  labels, these results describe **genre combinations/labels**, not clean single genres.

> **Important:** Correlation and group averages describe association, not causation and
> should not be presented as evidence that an audio feature causes popularity.

---

## Data quality and limitations

The following issues are intentionally documented rather than hidden:

- **`track_artists` is `unknown` for 88.9% of rows** (798,856 of 898,694). Artist-level
  conclusions are therefore unreliable until the upstream artist join is investigated.
- **19.8% of tracks have no usable genre tag** (`[]` or `unknown`).
- **25.4% of tracks have `popularity = 0`** (228,488 rows). This materially affects overall
  popularity averages and should be considered when interpreting results.
- The dataset contains **no release-date or duration field**, so release trends and
  duration-based analysis are outside the current scope.
- `genres` is stored as **combined label lists** (for example,
  `"['hip hop', 'rap']"`). Genre rankings therefore represent exact stored combinations
  unless the data is normalized/exploded first.
- The dashboard's artist and genre views should be interpreted in light of these data-quality
  limitations.

---

## Dashboard

`Spotify_Dashboard_Preview.html` is an **HTML/Chart.js preview** of the planned dashboard
experience. It is not the Power BI `.pbix` report itself.

The planned Power BI dashboard contains four analytical areas:

1. **Overview** — dataset KPIs, popularity distribution, tempo, musical mode, and top tracks.
2. **Audio Features** — correlations, feature distributions, and feature/popularity
   relationships.
3. **Genre Insights** — common genre labels/combinations and average popularity.
4. **Advanced Analysis** — low-vs-high popularity audio-profile comparisons and key findings.

The repository also references the Power BI data model, theme, and build guide under
`dashboard/`.

---

## Reproducibility

The large source/processed datasets are intentionally excluded from Git.

1. Obtain the original `tracks.csv` from the verified source cited at the top of this README.
2. Place it at:

```text
data/raw/tracks.csv
```

3. Run the notebooks in the order shown in the **Pipeline** section.
4. Use relative project paths such as `data/raw/tracks.csv` and
   `data/processed/spotify_cleaned.csv` rather than machine-specific paths.

> If an existing notebook still contains a path such as `F:\Project\Spotify\...`, replace it
> with a project-relative path before sharing the notebook.

---

## Setup

```bash
git clone <your-repo-url>
cd spotify-track-analytics

python -m venv venv
```

### Windows PowerShell

```powershell
venv\Scripts\Activate.ps1
```

### macOS / Linux

```bash
source venv/bin/activate
```

Then install dependencies:

```bash
pip install -r requirements.txt
jupyter notebook
```

---

## Tech stack

**Python** · **pandas** · **NumPy** · **Matplotlib** · **Jupyter** · **SQLite** ·
**Power BI** · **Chart.js (dashboard preview)**

---

## Future improvements

- Trace and repair the artist-join gap.
- Normalize/explode genre labels into individual genres.
- Add a predictive model such as Random Forest regression and report feature importance.
- Add release-date data for time-trend analysis.
- Add a verified data-source citation and repository/demo links.
- Add a dashboard screenshot or GIF to the repository README.

---

## Author

**Mathavan M**

BCA Student | Aspiring Data Analyst | Python | SQL | Data Visualisation | Web Development
