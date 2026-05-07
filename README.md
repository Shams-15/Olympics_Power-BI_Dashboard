# Olympics_Power-BI_Dashboard
<div align="center">

<img width="322" height="156" alt="download" src="https://github.com/user-attachments/assets/1f811692-c683-45c2-996d-729e71b68cdf" />


# 🏅 Olympic Games Analytics Dashboard

### *A Power BI report uncovering medal patterns, athlete performance & global dominance across Olympic history*

<br/>

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Data Analytics](https://img.shields.io/badge/Data%20Analytics-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)](/)
[![Sports Data](https://img.shields.io/badge/Domain-Sports%20Analytics-E30613?style=for-the-badge)](/)
[![Status](https://img.shields.io/badge/Status-Active-00C49F?style=for-the-badge)](/)

---

> **"Faster, Higher, Stronger — Smarter."**  
> An interactive analytics dashboard that transforms Olympic records into actionable insights across countries, sports, age groups, and genders.

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Dashboard Preview](#-dashboard-preview)
- [KPIs at a Glance](#-kpis-at-a-glance)
- [Visuals & Components](#-visuals--components)
- [Data Model](#-data-model)
- [Key Insights & Patterns](#-key-insights--patterns)
- [Filters & Interactivity](#-filters--interactivity)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Data Source](#-data-source)
- [Contributing](#-contributing)

---

## 🌍 Overview

The **Olympic Games Analytics Dashboard** is a single-page, fully interactive Power BI report built to answer critical questions about the Olympics:

- Which countries dominate in total medals and gold medals?
- What age groups produce the most medals?
- How does performance split across genders and sports?
- Who are the top-performing athletes of all time?

Built with a clean, dark-themed aesthetic using the **Olympic logo**, medal icons (Gold 🥇, Silver 🥈, Bronze 🥉), and a global **Shape Map** — this dashboard is as visually compelling as it is analytically powerful.

---

## 🖥️ Dashboard Preview

> *(Screenshot from Power BI Desktop — Page 1)*

```
┌─────────────────────────────────────────────────────────────────────────┐
│  🏅 OLYMPIC GAMES DASHBOARD              [Year] [Team] [Medal] [Sport]  │
│                                          [Sex]  [Age Bucket]            │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │  Total Medals │  🥇 Gold  │  🥈 Silver  │  🥉 Bronze │  Athletes  │ │
│  │    [KPI Card — Multi-Metric Card Visual]                           │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                                                                         │
│  ┌──────────────────────┐   ┌───────────────────────────────────────┐  │
│  │  🗺️ Shape Map         │   │  📊 Medals by Country (Clustered Bar) │  │
│  │  (Country choropleth) │   │  Gold | Silver | Bronze per country  │  │
│  └──────────────────────┘   └───────────────────────────────────────┘  │
│                                                                         │
│  ┌──────────────────────┐   ┌───────────────────────┐   ┌───────────┐ │
│  │  🥇 Gold Medal by     │   │  📈 Total Medal by Age │   │  🏆 Top 5  │ │
│  │  Country & Gender    │   │  (Column Chart)        │   │  Athletes │ │
│  │  (Stacked Bar)       │   │                        │   │  (Table)  │ │
│  └──────────────────────┘   └───────────────────────┘   └───────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 KPIs at a Glance

The **Multi-Metric Card Visual** at the top of the dashboard surfaces five headline KPIs that update dynamically based on active slicer selections:

| KPI | Description | Visual Icon |
|-----|-------------|-------------|
| 🏅 **Total Medals** | Aggregate count of all medals (Gold + Silver + Bronze) across selected filters | `Total_Medal.png` |
| 🥇 **Gold Medals** | Count of Gold medals won by the filtered selection | `Gold.png` |
| 🥈 **Silver Medals** | Count of Silver medals won | `Silver.png` |
| 🥉 **Bronze Medals** | Count of Bronze medals won | `Bronze.png` |
| 🧑‍🤝‍🧑 **Total Athletes** | Number of unique athletes in the filtered dataset | `Athelete.png` |

> All five metrics are powered by DAX measures from the `Measure_` table and respond instantly to any slicer change.

---

## 📈 Visuals & Components

### 1. 🗺️ Shape Map — *Global Medal Distribution*
- **Type:** `shapeMap`
- **Fields:** `athlete.Team` (country), `COUNT(athlete.Medal)`
- **Purpose:** A choropleth world map color-coded by total medal count — instantly revealing dominant nations.
- **Insight:** Darker shading = more medals. Hover for country-specific breakdowns.

---

### 2. 📊 Clustered Column Chart — *Medals by Country*
- **Type:** `clusteredColumnChart`
- **Fields:** `athlete.Team` (X-axis), `Gold`, `Silver`, `Bronze` (Y-axis, stacked by measure)
- **Purpose:** Side-by-side comparison of medal composition across the top-performing nations.
- **Insight:** Reveals whether a country's strength is driven by Gold dominance vs. broad medal collection.

---

### 3. 📉 Stacked Bar Chart — *Gold Medals by Country & Gender*
- **Type:** `barChart`
- **Fields:** `athlete.Team`, `Measure_.Gold`, `athlete.Sex`
- **Purpose:** Shows the gender split within gold medal performance by country.
- **Insight:** Identifies countries with strong female or male athletic programs in Gold-medal events.

---

### 4. 📈 Column Chart — *Total Medals by Age Bucket*
- **Type:** `columnChart`
- **Fields:** `athlete.Age Bucket` (X-axis), `Measure_.Total Medal` (Y-axis)
- **Purpose:** Reveals which age ranges produce the most Olympic medals.
- **Insight:** Typically peaks in the 20–30 age range, with sport-specific outliers (e.g., gymnastics vs. shooting).

---

### 5. 📋 Table — *Top 5 Athletes*
- **Type:** `tableEx`
- **Fields:** `athlete.Name`, `athlete.Team`, `athlete.Medal`
- **Purpose:** Surfaces the top-performing individual athletes with their country and medal type.
- **Insight:** Identifies multi-medal legends and historical champions across different Olympics.

---

### 6. 📦 Bar Chart — *Athletes by Sport*
- **Type:** `barChart`
- **Fields:** `athlete.Sport`, `COUNT(athlete.Name)`
- **Purpose:** Shows which sports have the highest athlete participation.
- **Insight:** Larger sports (e.g., Athletics, Swimming) dominate volume but medal efficiency varies.

---

## 🗃️ Data Model

The report is built on a single primary table: **`athlete`**

| Column | Type | Description |
|--------|------|-------------|
| `Name` | Text | Athlete's full name |
| `Team` | Text | Country / NOC code |
| `Medal` | Text | Gold, Silver, Bronze, or NA |
| `Sport` | Text | Olympic sport category |
| `Sex` | Text | M / F |
| `Age` | Number | Athlete's age at time of event |
| `Age Bucket` | Text | Binned age groups (e.g., 18–22, 23–27...) |
| `Year` | Number | Olympic year |

**Supplementary table:**

| Table | Purpose |
|-------|---------|
| `Measure_` | All DAX measures (Total Medal, Gold, Silver, Bronze, Total Athletes) |

**Custom Resources:**
- `Country.json` — GeoJSON mapping for Shape Map
- Medal icon PNGs — Used in KPI cards for visual flair

---

## 🔍 Key Insights & Patterns

```
📌 Pattern 1 — National Dominance
────────────────────────────────────────────────────────────────────
The USA, Russia, Germany, and Great Britain consistently appear 
among the top medal-winning nations. The Medals by Country clustered 
chart reveals who dominates Gold vs. accumulating Silver/Bronze.

📌 Pattern 2 — Age & Peak Performance
────────────────────────────────────────────────────────────────────
The "Total Medal by Age" column chart shows a clear bell curve 
peaking in the 22–28 range, with a sharp drop-off after age 35. 
Sport-specific slicers can reveal exceptions (e.g., equestrian or 
shooting athletes winning well into their 40s+).

📌 Pattern 3 — Gender Distribution in Gold Medals
────────────────────────────────────────────────────────────────────
The stacked bar "Gold Medal by Country & Gender" highlights which 
nations punch above their weight in women's sports programs. 
Countries with strong gender parity often have more diversified 
medal portfolios.

📌 Pattern 4 — Sport Participation vs. Medal Efficiency
────────────────────────────────────────────────────────────────────
High-athlete-count sports don't always correlate with high medal 
counts. Filtering by sport reveals niche disciplines where smaller 
nations punch well above their weight class.

📌 Pattern 5 — Athlete Legends in Top 5 Table
────────────────────────────────────────────────────────────────────
The Top 5 Athletes table surfaces multi-medal performers across 
editions. Filtering by Year uncovers era-specific legends while 
filtering by Sport reveals discipline-specific GOATs.
```

---

## 🎛️ Filters & Interactivity

The dashboard features **6 dynamic slicers** that cross-filter every visual simultaneously:

| Slicer | Field | Filter Type |
|--------|-------|-------------|
| 📅 **Year** | `athlete.Year` | Timeline / Dropdown |
| 🌍 **Team / Country** | `athlete.Team` | Multi-select |
| 🏅 **Medal Type** | `athlete.Medal` | Single / Multi-select |
| ⚥ **Sex** | `athlete.Sex` | Toggle (M / F) |
| 🏋️ **Sport** | `athlete.Sport` | Dropdown |
| 🔢 **Age Bucket** | `athlete.Age Bucket` | Range / Multi-select |

> **Tip:** Use the **Action Button** on the canvas to reset all filters to default — clearing slicer selections with a single click.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Report development & visual design |
| **DAX** | Calculated measures (Total Medal, Gold, Silver, Bronze, Total Athletes) |
| **Power Query (M)** | Data transformation & age bucketing |
| **Shape Map Visual** | Geo-spatial medal distribution |
| **Custom PNG Icons** | Medal & athlete imagery in KPI cards |
| **GeoJSON** | Country boundary mapping for Shape Map |
| **CY26SU02 Theme** | Base Power BI theme applied |

---

## 🚀 Getting Started

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (latest version recommended)
- Windows OS (Power BI Desktop is Windows-only)

### Steps

```bash
# 1. Clone this repository
git clone https://github.com/your-username/olympic-dashboard.git

# 2. Navigate to the project directory
cd olympic-dashboard

# 3. Open the dashboard file
start Dashboard.pbix
```

> Power BI Desktop will open the `.pbix` file directly. No additional configuration needed — the data model is embedded.

### Optional: Refresh Data
If you have a live data source connected:
1. Go to **Home → Transform Data → Data Source Settings**
2. Update the file path or connection string
3. Click **Refresh** to pull updated data

---

## 📁 File Structure

```
olympic-dashboard/
│
├── Dashboard.pbix                  # Main Power BI report file
├── README.md                       # This file
│
└── assets/                         # (Optional: exported resources)
    ├── icons/
    │   ├── Gold.png
    │   ├── Silver.png
    │   ├── Bronze.png
    │   ├── Total_Medal.png
    │   └── Athelete.png
    ├── Country.json                # GeoJSON for Shape Map
    └── screenshots/
        └── dashboard_preview.png
```

---

## 📂 Data Source

The underlying dataset is based on historical **Olympic Games athlete records**, including:

- **Summer & Winter Olympics** participation data
- **120 years of Olympic history** (depending on source range)
- **Key fields:** Athlete Name, NOC/Country, Sport, Event, Medal, Sex, Age, Year

> **Recommended Source:** [Kaggle — 120 Years of Olympic History](https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results)

---

## 📐 DAX Measures Reference

```dax
-- Total Medals
Total Medal = COUNTROWS(FILTER(athlete, athlete[Medal] <> "NA"))

-- Gold Medals
Gold = COUNTROWS(FILTER(athlete, athlete[Medal] = "Gold"))

-- Silver Medals
Silver = COUNTROWS(FILTER(athlete, athlete[Medal] = "Silver"))

-- Bronze Medals
Bronze = COUNTROWS(FILTER(athlete, athlete[Medal] = "Bronze"))

-- Total Athletes
Total Athletes = DISTINCTCOUNT(athlete[Name])
```

---

## 🤝 Contributing

Contributions, ideas, and improvements are welcome!

1. **Fork** this repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add: your feature description'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a **Pull Request**

### Ideas for Enhancement
- [ ] Add trend lines for medal growth by decade
- [ ] Host-country advantage analysis
- [ ] Drill-through pages per country/athlete
- [ ] Winter vs. Summer Olympics toggle
- [ ] Mobile-optimized layout

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with ❤️ and Olympic spirit**

⭐ *If this dashboard inspired you, please give it a star!* ⭐

</div>
