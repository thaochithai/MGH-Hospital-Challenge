# MGH-Hospital-Challenge
Analytics Dashboard for Hospital

# About this project
I approached this dataset by looking at the patient, operation, and finance level to analyze and deduct insights. These are some of the highlights from the findings:

**Patients:**

The top city with the most patients is Boston
Patients are mostly senior citizens aged 60 - 100
High patient return rate but a modest number of new patients (the number of new patients are calculated using the first encounter date - referred as joining date, hence, the total admitted patient is equal to total new patient in 2011 )
Patients live in proximity to the hospital, with older patients residing closer (the distance is calculated using the longitude and latitude of patients and hospital)
Each patient has an average of 2 insurances, with Medicare being the most popular among patients (patients have different insurance companies to pay for different procedures)
19% of patients visited hospital are admitted (admitted patient is defined as the patient has encounter duration longer than 1 day, which mean they stay overnight)
Average time between patient visits is around ﻿9﻿ months, and readmission is over a year (the average time between revisit and readmission is calculated by the day between two consecutive encounter dates)
> Targeted care for different age groups, 30 - 45 needs problem consultations and prenatal care, 46 - 60 require more medical interventions and treatments, while seniors (> 61) need regular follow-ups and urgent care

**Hospital Operation:**

Patients mostly encountered via ambulance or for outpatient services.
Inpatient admissions remain relatively low.
Care cooperation is relatively efficient and immediate, supported by encounter duration < 1 day and Average Length of Stay is 6.7 (< 9.9 average OECD countries)
The hospital is busiest during weekday mornings, specifically from 3-4 AM and 8-9 AM, as well as in the afternoon from 5-6 PM. Weekdays generally see higher activity compared to weekends.
> The COVID-19 pandemic drove more encounters for vaccines and introduced new respiratory-related procedures

**Finance:**

The hospital's revenue relies on check-ups, prenatal care, and urgent care services, accounting for nearly 50%. Of all procedures performed, 52% are covered.
Steady Revenue with a sharp increase in 2020–2021 due to the pandemic after prolonged decline since 2014
Highest revenue is from 91-100 and 76-90, while 30-45 is potential age group with significant revenue and highest cost per encounter despite being smaller segment
Medicare is the leading contributor, making it a crucial partner in insurance-paid procedures.
> Revenue primarily comes from urgent care and check-ups, especially from patients aged 76-100. Prenatal visits, costing three times more than average, make the 30-45 age group a key segment.
