# Football Player Market Value Prediction

## Project Overview
This project focuses on predicting and analyzing the market value of football players in the English Premier League using multi-season performance statistics. By integrating advanced match data, market valuation data, feature engineering, and graph-based modeling, the project aims to explore the relationship between on-field performance, team context, and player market value.

The project is designed as a data-driven group assignment and emphasizes reproducible data processing, transparent feature construction, and extensible modeling workflows.

---

## Data Sources
The dataset is constructed from publicly available football statistics and market valuation data:

- **FBref**: Team- and player-level advanced performance statistics
- **Transfermarkt**: Player market value data

Data collection and preprocessing are primarily implemented using the R packages **worldfootballR** and **worldfootballRdata**.

---

## Data Coverage
- **League**: English Premier League (Premier League)
- **Seasons**:
  - Team-level data: 2019–2024
  - Player-level data: 2020–2024

---

## Data Files

### 1. Team-Level Dataset
**File**: `teams_preprocessed.csv`

- Granularity: Team × Season
- Source: FBref
- Description: Aggregated season-level performance statistics for Premier League teams

**Key Variables**:
- Match outcomes: `MP`, `W`, `D`, `L`
- Offensive output: `Gls`, `Ast`, `G_plus_A`
- Expected metrics: `xG`, `xAG`, `xG_plus_xAG`
- Non-penalty metrics: `npxG`, `npxG_plus_xAG_Expected`
- Per-90-minute efficiency metrics (e.g. `Gls_Per_90`, `xG_Per_90`)

All variables with the suffix `Per_90` are normalized per 90 minutes of play.

---

### 2. Player-Level Dataset
**File**: `players_preprocessed_cleaned.csv`

- Granularity: Player × Season
- Source: FBref + Transfermarkt
- Description: Individual season-level player performance merged with market value data

**Key Variables**:
- Player information: `Player`, `Squad`, `Pos`, `Age`, `Year`
- Playing time: `MP`, `Starts`, `Min`, `Mins_Per_90_Playing`
- Performance: `Gls`, `Ast`, `G_plus_A`, `xG`, `xAG`
- Efficiency: `Gls_Per_90`, `Ast_Per_90`, `xG_Per_90`, `xAG_Per_90`
- Market value: `market_value_euro`

Only players with complete market value information are retained.

---

## Feature Engineering

### Player-Level Derived Features
- **Identity Features**:
  - `is_eng`: English nationality indicator
  - `is_big6_team`: Indicator for Premier League Big 6 clubs

- **Age-Related Features**:
  - `age_group`: Age bins (18–22, 23–26, 27–30, 31+)
  - `age_x_market_value`
  - `log_market_value`

- **Performance & Efficiency**:
  - `goal_per90`, `assist_per90`
  - `xG_per90`, `xAG_per90`

- **Relative-to-Team Metrics**:
  - `Gls_to_team_mean`
  - `Ast_to_team_mean`
  - `xG_Expected_to_team_mean`
  - `xAG_Expected_to_team_mean`

- **Team Role Indicators**:
  - `goal_contrib`
  - `xG_contrib`
  - `is_attack_core` (defined as contribution > 20%)

The engineered player feature dataset is saved as `players_features_sy.csv`.

---

### Team-Level Derived Features
- **Aggregated Statistics** (mean, standard deviation, max, sum):
  - Goals, assists, expected goals, expected assists
  - Market value

- **Ratio-Based Features**:
  - `attack_core_ratio`
  - `eng_player_ratio`

The engineered team feature dataset is saved as `teams_features.csv`.

---

## Modeling

The project includes exploratory modeling approaches, including:
- Traditional regression and feature-based analysis
- Graph-based modeling using player–team interaction networks (see `GNN.ipynb`)

Feature construction and modeling notebooks are provided for transparency and reproducibility.

---

## Project Structure

```
├── data/
│   ├── teams_preprocessed.csv
│   ├── players_preprocessed_cleaned.csv
│   ├── players_features_sy.csv
│   └── teams_features.csv
├── notebooks/
│   ├── feature_engineering.ipynb
│   └── GNN.ipynb
├── README.md
└── LICENSE
```

---

## Environment & Dependencies

### R (Data Collection)
- R ≥ 4.2.0
- Packages:
  - worldfootballR
  - worldfootballRdata
  - dplyr
  - chromote

### Python (Modeling & Analysis)
- pandas
- numpy
- scikit-learn
- PyTorch / PyTorch Geometric (for GNN models)

---

## License
This project is released under the **MIT License**, unless otherwise specified.

---

## Acknowledgements
- FBref.com for advanced football statistics
- Transfermarkt.com for player market value data
- worldfootballR by Jase Ziv for data access and preprocessing support

