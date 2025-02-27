# 🏥 MGH Hospital Analytics Dashboard

## 📊 Overview
This project presents a comprehensive analytics dashboard for Massachusetts General Hospital (MGH), focusing on patient demographics, hospital operations, and financial performance. The dashboard provides actionable insights to support strategic decision-making and operational improvements.

## 🔄 Data Model

<img width="751" alt="Screenshot 2025-02-27 204953" src="https://github.com/user-attachments/assets/90ffaa5b-a9f9-4eb0-b7d2-1b8c9e0628e3" />

### Star Schema Implementation
The dashboard utilizes a star schema data model with:

#### Fact Table
- **encounters**: Contains all patient visit records and core metrics

#### Dimension Tables
- **patients_lookup**: Patient demographic information and attributes
- **procedures_lookup**: Medical procedures reference data
- **payers_lookup**: Insurance and payment method information
- **organization_lookup**: Healthcare facility and department data
- **calendar_lookup**: Date dimension for time-based analysis

#### DAX Calculations
The model leverages numerous DAX measures to create calculated metrics and KPIs that power the visualizations throughout the dashboard.

## 📱 Dashboard Structure
The dashboard consists of four main tabs:
1. **Executive Summary** - Overall hospital performance across patient, operational, and financial metrics
2. **Patient Analytics** - Detailed patient demographics and visit patterns
3. **Hospital Operations** - Operational efficiency and resource utilization
4. **Financial Performance** - Revenue streams and cost analysis

## 🔍 Key Features & Technical Implementation

### 👥 Patient Analytics
![Patient Analytics Dashboard](https://github.com/user-attachments/assets/02fec41e-a62d-448f-a657-68d0094d8c92)

#### 📐 Advanced Metrics Implementation:
- **Geographic Analysis**: Calculated patient distance from hospital using longitude and latitude coordinates
- **Patient Acquisition Tracking**: Identified new patients based on first encounter date
- **Admission Classification**: Categorized visits with encounter duration > 1 day as admissions
- **Length of Stay Calculation**: Implemented DAX measures to calculate average stay duration

```
Average Length of Stay = 
AVERAGEX(
    SUMMARIZE(
        FILTER(
            encounters,
            encounters[DURATION]>0),
        encounters[Id],
        encounters[START],
        encounters[STOP],
        "duration", (encounters[STOP]-encounters[START])
    ), 
    ([duration])
)
```

- **Readmission Analysis**: Calculated intervals between consecutive patient visits using complex DAX formulas

```
Days Between = 
AVERAGEX(
    VALUES(encounters[PATIENT]),
    VAR CurrentPatientID = encounters[PATIENT]
    VAR EngagementDates = 
        CALCULATETABLE(
            VALUES(encounters[START]),
            encounters[PATIENT] = CurrentPatientID
        )
    VAR DateDifferences = 
        ADDCOLUMNS(
            EngagementDates,
            "DaysDifference", 
                DATEDIFF(
                    CALCULATE(
                        MAX(encounters[START]),
                        FILTER(
                            encounters,
                            encounters[PATIENT] = CurrentPatientID &&
                            encounters[START] < EARLIER(encounters[START])
                        )
                    ),
                    encounters[START], 
                    DAY
                )
        )
    VAR NonBlankDifferences = 
        FILTER(
            DateDifferences,
            NOT(ISBLANK([DaysDifference]))
        )
    RETURN
        AVERAGEX(NonBlankDifferences, [DaysDifference])
)
```

#### 💡 Key Insights:
- Boston residents constitute the largest patient segment
- Patient demographics skew toward seniors (60-100 years)
- High patient return rate but moderate new patient acquisition
- Patients typically live in proximity to the hospital, with older patients residing closer
- Multiple insurance coverage is common (avg. 2 per patient), with Medicare being predominant
- 19% hospital visit rate for admissions
- Average interval between visits: ~9 months; readmission interval: >1 year

#### 🎯 Strategic Implications:
- **Age-Based Care Models**: Tailored approaches for different demographic segments:
  - 30-45 age group: Problem consultations and prenatal care
  - 46-60 age group: Medical interventions and treatments
  - 61+ age group: Regular follow-ups and urgent care services

### ⚕️ Hospital Operations
![Operations Dashboard](https://github.com/user-attachments/assets/71ee3831-375c-4222-b42d-c44a336aeec1)

#### Key Insights:
- Ambulatory services and outpatient care dominate encounter types
- Inpatient admissions represent a smaller proportion of overall hospital activity
- Care coordination metrics show efficiency: most encounters resolve within 24 hours
- Average Length of Stay: 6.7 days (below OECD country average of 9.9 days)
- Peak operation times: Weekday mornings (3-4 AM, 8-9 AM) and afternoons (5-6 PM)
- Significant weekday vs. weekend activity differential

#### Strategic Implications:
- COVID-19 pandemic drove substantial increases in vaccination encounters
- Resource allocation should prioritize peak operational periods

### 💰 Financial Performance
![Financial Dashboard](https://github.com/user-attachments/assets/41ac47ac-cbd8-4671-85b5-e0227c62082c)

#### Key Insights:
- Primary revenue drivers: check-ups, prenatal care, and urgent care (nearly 50% of revenue)
- Insurance coverage for 52% of all procedures performed
- Revenue trend: Declining from 2014, with sharp recovery in 2020-2021 during pandemic
- Highest revenue by age group: 91-100 and 76-90
- Emerging opportunity in 30-45 age group: highest cost per encounter despite smaller segment
- Medicare leads as primary payer, establishing it as a crucial partner

#### Strategic Implications:
- Revenue optimization should focus on urgent care and check-up service lines
- Consider expanded prenatal services targeting 30-45 age group (3x higher per-encounter cost)

## 📁 Data Source
This project utilizes data provided by Maven Analytics.
