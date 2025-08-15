# FPFVG Automated Charting Script

## Overview

This script is designed for identifying and visualizing the first presented Fair Value Gaps (FVGs) in the futures market after New York Open. It is inspired by ICT concepts and incorporates session-based logic, previous day levels, and midnight open.

## Features

- **Session Construction:**  
  Automatically builds US futures trading sessions (18:00 prior day to 16:59 current day) for each date in your dataset.

- **Session Data Filtering:**  
  Merges session info with price data, ensuring all analysis is session-aware.

- **Previous Day Levels:**  
  Calculates and plots previous day high (PD BSL) and low (PD SSL) for each session.

- **00:00 Open Annotation:**  
  Marks the midnight open price for each session.

- **FVG Detection (BISI/SIBI):**  
  Detects the first Fair Value Gap after 09:30 (US open) in each session:
  - **BISI:** Buyside Imbalance Sellside Inefficiency (green box)
  - **SIBI:** Sellside Imbalance Buyside Inefficiency (red box)
  - Annotates the FVG with `"F.P. BISI"` or `"F.P. SIBI"` centered in the box.

- **Opposite FVG Annotation:**  
  If a second FVG of the opposite orientation appears in the session, it is also boxed and annotated.

- **Interactive Candlestick Charts:**  
  Generates Plotly HTML charts for each session, showing price action, levels, and FVGs.

- **Data Export:**  
  Stores all detected FPFVG events in a DataFrame for further analysis.

## How It Works

1. **Load Data:**  
   Reads a CSV file containing minute-level NQ futures data.

2. **Build Sessions:**  
   Constructs session start/end times for each trading day.

3. **Merge & Filter:**  
   Merges session info with price data, filters to session times.

4. **Calculate Previous Day Levels:**  
   For each session, computes previous day's high and low.

5. **Detect FVGs:**  
   For each session, scans after 09:30 for the first FVG (BISI or SIBI) and, if present, the next opposite FVG.

6. **Visualize:**  
   Plots candlestick chart with:
   - Session background
   - PD BSL/SSL lines
   - 00:00 open line
   - FVG rectangles and annotations

7. **Export:**  
   Saves charts as HTML and F.P. FVG events as a DataFrame.

## Usage

1. **Configure File Paths:**  
   Update the CSV path and output directory as needed.

2. **Run the Script:**  
   Execute in a Jupyter Notebook or Python environment.

3. **View Charts:**  
   HTML charts will be saved and displayed for each session.

4. **Analyze Data:**  
   Use the exported DataFrame (`fpfvg_df`) for further research or strategy development.

## Requirements

- Python 3.x
- pandas
- numpy
- plotly
- IPython (for display in notebooks)

## Notes

- The script is designed for minute-level futures data with columns: `time`, `open`, `high`, `low`, `close`.
- All session logic is based on US Eastern Time.
- FVG detection is based on ICT-style logic:  
  - BISI: Next candle's low > previous candle's high  
  - SIBI: Next candle's high < previous candle's low

## Customization

- You can adjust session times, FVG logic, or add more annotations as needed.
- The script is modular and can be extended for other markets or timeframes.

---

---

**Author:** livefreeordie_t (https://x.com/livefreeordie_t)
**Last updated:** August 2025
