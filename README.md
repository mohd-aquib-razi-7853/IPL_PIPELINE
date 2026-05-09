# 🏏 IPL 2025 — Data Engineering & Analysis Pipeline

A complete **data engineering pipeline** that ingests, cleans, loads, queries, and visualizes **IPL 2025** batting and bowling statistics using **Python**, **Pandas**, **PostgreSQL**, and **Matplotlib**.

---

## 📌 Overview

This project demonstrates a full end-to-end data workflow:

1. **Ingest** raw CSV datasets (batters & bowlers)
2. **Explore & Clean** column names and data types for database compatibility
3. **Load** into a local **PostgreSQL** database via SQLAlchemy
4. **Query** using SQL to extract insights
5. **Visualize** key metrics with Matplotlib

---

## 🗂️ Project Structure

```
ipl_de/
├── IPL2025Batters.csv      # Raw batting stats (156 players, 14 columns)
├── IPL2025Bowlers.csv      # Raw bowling stats (108 players, 13 columns)
├── Ipl.ipynb               # Jupyter notebook — full pipeline
├── sixes_by_team.png       # Generated chart: Sixes by Team
└── README.md
```

---

## 📊 Datasets

### Batters (`IPL2025Batters.csv`)
| Column | Description |
|--------|-------------|
| Player Name | Batter name |
| Team | IPL franchise (GT, MI, RCB, etc.) |
| Runs | Total runs scored |
| Matches | Matches played |
| Inn | Innings batted |
| No | Not outs |
| HS | Highest score |
| AVG | Batting average |
| BF | Balls faced |
| SR | Strike rate |
| 100s | Centuries |
| 50s | Half-centuries |
| 4s | Fours hit |
| 6s | Sixes hit |

### Bowlers (`IPL2025Bowlers.csv`)
| Column | Description |
|--------|-------------|
| Player Name | Bowler name |
| Team | IPL franchise |
| WKT | Wickets taken |
| MAT | Matches played |
| INN | Innings bowled |
| OVR | Overs bowled |
| RUNS | Runs conceded |
| BBI | Best bowling in innings |
| AVG | Bowling average |
| ECO | Economy rate |
| SR | Strike rate |
| 4W | 4-wicket hauls |
| 5W | 5-wicket hauls |

---

## 🔧 Pipeline Steps (Notebook)

### 1. Data Ingestion
```python
batter = pd.read_csv("IPL2025Batters.csv")
bowler = pd.read_csv("IPL2025Bowlers.csv")
```

### 2. Data Cleaning
- Column names normalized to `snake_case` for PostgreSQL compatibility
- Renamed ambiguous columns (`100s` → `hundreds`, `50s` → `fifties`, `4s` → `fours`, `6s` → `sixes`, `4w` → `four_wickets`, `5w` → `five_wickets`)
- Verified **zero missing values** in both datasets

### 3. Load to PostgreSQL
```python
engine = create_engine('postgresql://postgres:***@localhost/ipl_2025')
batter.to_sql('batters', engine, if_exists='replace', index=False)
bowler.to_sql('bowlers', engine, if_exists='replace', index=False)
```

### 4. SQL Analysis Queries
| # | Query | Key Finding |
|---|-------|-------------|
| Q1 | Top 5 run scorers | Sai Sudharsan (GT) — 759 runs |
| Q2 | Top 5 wicket takers | Prasidh Krishna (GT) — 25 wickets |
| Q3 | Most runs by team | PBKS — 3,000 runs |
| Q4 | Players with 500+ runs | 11 players crossed the 500-run mark |
| Q5 | Most sixes by team | PBKS — 173 sixes |
| Q6 | Most economical bowlers (10+ wkts) | Jasprit Bumrah (MI) — 6.67 eco |
| Q7 | Highest avg strike rate by team | PBKS — 144.91 |
| Q8 | All-rounders (JOIN query) | Players appearing in both batters & bowlers tables |

### 5. Visualization

![IPL 2025 — Total Sixes by Team](sixes_by_team.png)

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Python 3** | Core language |
| **Pandas** | Data ingestion, cleaning, transformation |
| **SQLAlchemy** | ORM / DB connection engine |
| **PostgreSQL** | Relational database for structured storage |
| **Matplotlib** | Data visualization |
| **Jupyter Notebook** | Interactive development environment |

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- PostgreSQL installed and running locally
- A database named `ipl_2025`

### Setup
```bash
# Clone the repository
git clone https://github.com/mrazi/ipl_de.git
cd ipl_de

# Install dependencies
pip install pandas sqlalchemy psycopg2-binary matplotlib jupyterlab

# Create the database
createdb ipl_2025

# Launch the notebook
jupyter lab Ipl.ipynb
```

---

## 📈 Key Insights

- **Orange Cap contender**: Sai Sudharsan (GT) led with **759 runs** at a 54.21 average
- **Purple Cap contender**: Prasidh Krishna (GT) topped with **25 wickets**
- **Most explosive team**: PBKS smashed the most sixes (**173**) and had the highest avg strike rate (**144.91**)
- **Most economical**: Jasprit Bumrah maintained an incredible **6.67** economy rate

---

## 📄 License

This project is for **educational and analytical purposes only**. IPL data belongs to its respective owners.

---

## 🤝 Contributing

Feel free to fork, open issues, or submit pull requests to extend the analysis!
