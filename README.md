# Career Readiness, Skill Development & Challenges Faced by SEE and +2 Graduates in Nepal

A survey-based data science project analyzing how career-ready Nepali students feel after completing their SEE or +2 exams — what skills they're building, how they build them, what's holding them back, and what actually predicts "readiness."

![Dashboard](figures/phase6_dashboard.png)

## Overview

Every year, hundreds of thousands of students in Nepal finish their SEE or +2 exams and face a pivotal transition — further study, skill-building, or the job market — often with little structured guidance. This project surveyed 171 recent graduates (167 after cleaning) to find out:

1. **What skills** are SEE/+2 graduates developing, and through what channels?
2. **What challenges** do they face becoming career-ready — and does it vary by province or stream?
3. **How career-ready** do they feel overall, and what factors best predict that?

The full pipeline: **survey design → data cleaning → EDA → a custom Career Readiness Score → machine learning modeling → reporting.**

## Key Findings

- **Financial constraints, lack of mentorship, and lack of networking** — not lack of interest or GPA — are the dominant barriers to career readiness.
- Programming/Coding, Data Science, and AI/ML are the most popular skills being learned, but **~22% of respondents aren't learning any skill yet**.
- GPA and weekly skill-hours correlate only weakly with how career-ready students *feel* — effort alone doesn't predict confidence.
- A Random Forest model found that **GPA, perception of the education system, and learning channel** (institute/paid course vs. free YouTube content) predict readiness better than demographics alone (R² = 0.12 vs. -0.26 for Linear Regression).
- The average Career Readiness Score is **50.5/100** — most students sit in the "Medium" band: engaged, but not yet confidently prepared.

Full findings, methodology, and limitations are in [`Career_Readiness_Report.docx`](Career_Readiness_Report.docx).

## Repository Structure

```
├── Career_Readiness_Analysis.ipynb    # Full analysis notebook (cleaning → EDA → scoring → ML → dashboard)
├── Career_Readiness_Report.docx       # Final written report
├── Career_Readiness_Presentation.pptx # 23-slide presentation deck
├── cleaned_data.csv                   # Cleaned survey data (167 rows × 66 cols)
├── cleaned_data_with_score.csv        # Cleaned data + engineered readiness_score
├── figures/                           # All chart PNGs, including the final dashboard
└── README.md
```

> **Note on raw data:** the original raw Google Forms export (`uncleaned_data.csv`) is not included in this repo to protect respondent privacy. The notebook is written to fall back gracefully to `cleaned_data.csv` when the raw file isn't present, so it still runs end-to-end for anyone who clones this repo.

## Methodology

**Survey:** 23-question Google Form, distributed primarily via Instagram, mid-2026. 171 raw submissions → 167 analyzed after dropping non-consenting/blank responses.

**Data cleaning:** renamed Google Forms' long question-text headers to short snake_case names, converted bucketed answers (age, GPA, weekly hours) to numeric midpoints, and exploded 4 multi-select checkbox questions into 34 binary columns.

**Career Readiness Score:** a transparent, weighted 0–100 composite built from 4 self-reported Likert measures (career clarity, market awareness, education support, confidence), skill-building hours, skill breadth, and inverse challenge frequency. Weights are stated explicitly in the notebook — it's the one place in the pipeline that isn't purely mechanical.

**Machine learning:** Linear Regression and Random Forest were trained to predict the readiness score using only **context** features (demographics, learning habits, career interest) — deliberately excluding the Likert questions that built the score, to avoid circular prediction. 75/25 train-test split, fixed random seed.

**Known limitations:** convenience sample skewed toward Bagmati province and digitally-active students (Instagram distribution); self-reported attitude measures; n=167 is small for ML, so results are directional, not nationally generalizable; cross-sectional data (single point in time, mid-2026).

## Tech Stack

- **Python:** pandas, numpy, matplotlib, seaborn, scikit-learn
- **Environment:** Jupyter Notebook
- **Reporting:** Microsoft Word, PowerPoint

## Running It Yourself

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook Career_Readiness_Analysis.ipynb
```

Run all cells — the notebook automatically detects that the raw file is absent and picks up from `cleaned_data.csv`.

## Author

**Sandip Subedi**
Data science / applied social research, Nepal.

If you use this dataset or methodology, a link back to this repo is appreciated.

## License

This project's code is available for learning and reference. The survey data reflects real (anonymized) respondent input — please don't redistribute it outside this repo without attribution.
