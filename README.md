# End-to-End Ulcer Health Risk Analysis Dashboard in Power BI

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Modeling-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Healthcare Analytics](https://img.shields.io/badge/Healthcare-Data_Analytics-2E8B57?style=for-the-badge)

An interactive, end-to-end **Healthcare Data Analytics Dashboard** built in **Microsoft Power BI** to evaluate peptic ulcer disease progression, clinical risk factors, symptom patterns, and treatment outcomes across 500 patient records.

---

## Problem Statement

Peptic ulcer disease poses significant clinical challenges, ranging from mild dyspepsia to life-threatening gastrointestinal bleeding (hematemesis and melena) requiring emergency hospitalization or surgical intervention. Healthcare providers and clinical decision-makers often struggle to:
- **Identify high-risk patient profiles** early across varying demographic groups (age, sex, BMI) and lifestyle habits (smoking, alcohol consumption).
- **Assess the impact of *Helicobacter pylori* (*H. pylori*) infection and prolonged medication use** (such as NSAIDs and aspirin) on ulcer severity, lesion size, and depth.
- **Monitor key hematological indicators** (such as hemoglobin depletion and occult blood in stool) alongside clinical staging to optimize treatment pathways (medical, endoscopic, or surgical) and improve patient recovery rates.

This project addresses these challenges by transforming raw clinical patient records into a centralized, interactive **Power BI Decision-Support Dashboard** that enables rapid risk stratification and evidence-based healthcare insights.

---

## Dataset Details

The project utilizes two structured datasets located in the repository:

### 1. Primary Clinical Dataset (`Ulcer Dataset (1).csv`)
Contains **500 patient records** and **23 clinical & demographic attributes** spanning diagnoses from **2016 to 2025**:

| Category | Columns / Attributes | Description |
| :--- | :--- | :--- |
| **Demographics** | `patient_id`, `age`, `sex`, `bmi`, `Date of Diagnosis` | Unique identifier, patient age (26–77 years), gender (250 Male / 250 Female), Body Mass Index, and diagnosis date. |
| **Medical & Lifestyle History** | `h_pylori_status`, `ulcer_history`, `med_type`, `med_duration(Monthly)`, `smoking_status`, `alcohol_intake_level` | *H. pylori* test status (`positive`/`negative`), prior ulcer history (`none`, `previous`, `recurrent`), medication regimen (`NSAIDs`, `aspirin`, `none`), duration in months, smoking status (`never`, `former`, `current`), and alcohol intake (`none`, `moderate`, `heavy`). |
| **Clinical Symptoms & Labs** | `pain_severity`, `pain_pattern`, `gi_symptoms`, `bleeding_symptoms`, `hemoglobin_g_dl`, `stool_ob` | Pain score (1–9 scale), timing (`postprandial`, `fasting`, `nocturnal`, `mixed`), GI symptoms (`dyspepsia`, `nausea_vomiting`, `alarm_symptoms`), bleeding (`none`, `hematemesis`, `melena`), hemoglobin level (g/dL), and stool occult blood test (`positive`/`negative`). |
| **Pathology & Outcomes** | `ulcer_size_mm`, `ulcer_depth`, `Ulcer_stage`, `treatment_category`, `hospitalization_required`, `ulcer_outcome` | Ulcer lesion size (2–36 mm), anatomical depth (`erosion`, `superficial`, `deep`, `very deep`), clinical stage (`Stage 1` to `Stage 4`), intervention type (`medical`, `endoscopic`, `surgical`), hospitalization status (`yes`/`no`), and recovery outcome (`healed`/`persistent`). |

### 2. Visual Staging Reference (`Ulcer Image Dataset (1).csv`)
Maps each clinical stage (`Stage 1` through `Stage 4`) to dynamic anatomical illustrations (`Image_Url`) and custom stage icons (`Icon_Url`) for interactive visual filtering inside Power BI.

---

## Approach

The project was executed using an end-to-end Business Intelligence workflow:

1. **Data Cleaning & Transformation (Power Query):**
   - Validated data types across all 23 clinical attributes, standardized date hierarchies (`Year`, `Quarter`, `Month`, `Day`), and verified zero missing or duplicate patient records.
2. **Data Modeling:**
   - Established a relational model linking the primary clinical dataset (`Ulcer Dataset`) with the visual reference table (`Ulcer Image Dataset`) via `Ulcer_stage` (Many-to-One relationship).
3. **DAX Measures & Calculated Columns (`Formulas.txt`):**
   - **Dynamic Benchmark KPIs:** Engineered DAX measures (`Vs Avg Age`, `VS Avg Ulcer Size`, and `VS Avg Pain Severity`) using `CALCULATE`, `ALL`, and `UNICHAR(9650/9660)` directional indicators (`▲` / `▼`) to compare filtered cohorts against overall population averages in real time.
   - **Demographic Bucketing:** Created a custom `Age Group` calculated column utilizing `SWITCH(TRUE(), ...)` logic to segment patients into 5-year age brackets (`26+`, `31+`, ..., `76+`).
4. **Interactive Dashboard Design & Custom Visuals:**
   - Designed a modern, medical-themed UI layout (`Background. (1).png`) featuring KPI summary cards with trend sparklines, a **Chiclet Slicer** with stage icons, dynamic anatomical stage imagery, and comparative charts for ulcer depth, medication usage, pain patterns, and patient history.

---

## Results

Analysis of the **500-patient cohort** surfaced the following key clinical findings:

- **Cohort & Baseline Metrics:**
  - **Total Patients:** 500 (50% Male, 50% Female) with an average age of **52.0 years**, average BMI of **27.45**, and average hemoglobin level of **11.55 g/dL**.
  - **Average Ulcer Size & Pain:** Mean lesion size is **15.26 mm** (ranging from 2 mm to 36 mm) with an average pain severity score of **5.56 / 9**.
- **Etiology & Risk Factors:**
  - **High *H. pylori* Prevalence:** **62.8%** of patients (314) tested positive for *H. pylori*, confirming it as the primary infectious driver.
  - **Medication Exposure:** **65.8%** of patients were actively taking ulcerogenic medications—**41.6% on NSAIDs** (208 patients) and **24.2% on Aspirin** (121 patients).
  - **Recurrence History:** **66.6%** of patients had a prior history of ulcers (**41.2% previous**, **25.4% recurrent**), while **33.4%** presented as first-time cases.
- **Clinical Severity & Staging:**
  - **Stage Distribution:** **Stage 1** accounts for **34.0%** (170), **Stage 2** for **25.8%** (129), **Stage 3** for **24.2%** (121), and **Stage 4** for **16.0%** (80).
  - **Ulcer Depth & Bleeding:** **35.4%** of lesions are classified as `deep` (177) and **10.0%** as `very deep` (50). Overall, **40.0%** of patients experienced acute GI bleeding (**25.0% hematemesis**, **15.0% melena**), and **65.8%** tested positive for stool occult blood.
  - **Symptom Patterns:** Postprandial pain is the most common presentation (**34.2%**), followed by fasting (**25.8%**), nocturnal (**24.2%**), and mixed pain (**15.8%**).
- **Treatment & Patient Outcomes:**
  - **Interventions:** **64.6%** of patients were managed medically (323), **17.8%** endoscopically (89), and **17.6%** required surgery (88).
  - **Hospitalization & Recovery:** **40.0%** of cases (200 patients) required inpatient hospitalization. Overall, **70.0%** of patients (350) achieved complete healing (`healed`), while **30.0%** (150) exhibited `persistent` ulcers requiring ongoing clinical follow-up.

---

## About This Repository

```text
├── Ulcer health risk analysis.pbix   # Interactive Power BI Dashboard file (PBIX)
├── Ulcer Dataset (1).csv             # Primary clinical dataset (500 rows, 23 columns)
├── Ulcer Image Dataset (1).csv       # Stage-to-Image/Icon mapping dataset
├── Formulas.txt                      # Documented DAX measures and calculated columns
├── Background. (1).png               # Custom UI background asset used in the dashboard
└── README.md                         # Project documentation and findings
```

### How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/ahmedmahmoudkhalifa300/End-to-End-Ulcer-Health-Risk-Dashboard.git
   ```
2. Open **`Ulcer health risk analysis.pbix`** using [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).
3. If prompted to update data source paths, point Power BI to the local copies of `Ulcer Dataset (1).csv` and `Ulcer Image Dataset (1).csv` included in the repository.

### Author
**Ahmed Mahmoud Khalifa**  
[GitHub Profile](https://github.com/ahmedmahmoudkhalifa300)
