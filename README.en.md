<div align="center">

# EHR-Based Alzheimer’s Diagnostic Bottleneck Map

<p>
  <a href="./README.md">한국어</a> · <strong>English</strong>
</p>

<strong>
A research project identifying the earliest pre-diagnosis comorbidity record<br/>
and examining the interval to diagnosis and clinical-domain differences across patient groups
</strong>

<br/><br/>

![Event](https://img.shields.io/badge/2026-Multi--Omics%20Hands--On-147C8A)
![Data](https://img.shields.io/badge/Data-Synthetic%20EHR-5A8F99)
![Project](https://img.shields.io/badge/Project-Solo-0C4F5A)
![Analysis](https://img.shields.io/badge/Analysis-Logistic%20Regression-147C8A)
![Award](https://img.shields.io/badge/Award-Grand%20Prize-C5962A)

<br/>

<img
  src="./assets/overview/alzheimer-ehr-bottleneck-analysis.png"
  width="100%"
  alt="Overview of the Alzheimer’s EHR bottleneck analysis"
/>

<sub>
This overview diagram summarizes the analytical flow of the project. The actual results are shown in the presentation-based charts below.
</sub>

<br/><br/>

<a href="./materials/2026-multi-omics-presentation.pdf">
  <img src="https://img.shields.io/badge/Presentation-View-147C8A?style=for-the-badge" alt="View presentation" />
</a>
<a href="./materials/2026-multi-omics-poster.pdf">
  <img src="https://img.shields.io/badge/Poster-View-147C8A?style=for-the-badge" alt="View poster" />
</a>
<a href="./materials/2026-multi-omics-abstract.pdf">
  <img src="https://img.shields.io/badge/Abstract-View-5A8F99?style=for-the-badge" alt="View abstract" />
</a>
<a href="./materials/2026-multi-omics-award.pdf">
  <img src="https://img.shields.io/badge/Award-View-C5962A?style=for-the-badge" alt="View award" />
</a>
<a href="https://www.gwlrs.ac.kr/ko/news/press/view/360?p=1">
  <img src="https://img.shields.io/badge/Event%20News-View-5E6E73?style=for-the-badge" alt="View event news" />
</a>

</div>

---

## 🧭 Research Background

Before an Alzheimer’s disease diagnosis, records of hypertension, diabetes, kidney disease, and other comorbidities may accumulate. However, it is difficult to determine which clinical domain appeared first and how the interval from that record to diagnosis differed across patient groups.

This project defined the earliest of 24 candidate-condition records within the 10 years before diagnosis as the **first signal**. The date difference from the first signal to the Alzheimer’s disease diagnosis was calculated as a **record-based interval**, and the condition corresponding to the first signal was mapped to one of six clinical domains for comparison across interval groups.

Rather than predicting individual disease risk, the analysis focused on which clinical domain appeared first in the pre-diagnosis record and under what conditions the interval to diagnosis was observed to be longer.

---

## ❓ Research Questions

The study had four research questions but followed one analytical sequence. It first examined the size and distribution of the record-based interval, then compared the clinical domains of the first signals. It subsequently assessed whether the domain pattern remained after considering record count and how the findings changed when the observation window was modified.

<p align="center">
  <img
    src="./assets/study/research-questions.png"
    width="100%"
    alt="Research questions for the Alzheimer’s EHR analysis"
  />
</p>

---

## ⏱️ Analysis Design

**The analytical time axis was defined first.** The Alzheimer’s disease diagnosis date was set as the **Index**, and the preceding 10 years were used as the primary observation window. Among 24 candidate conditions, the earliest record within that window was selected as the first signal. Records on or after the diagnosis date were excluded so that information generated at or after diagnosis would not be treated as a pre-diagnosis record.

<p align="center">
  <img
    src="./assets/study/time-axis.png"
    width="100%"
    alt="Time-axis definition for the Alzheimer’s EHR analysis"
  />
</p>

**The analytical cohort was constructed using this definition.** Of 3,000 individuals in the synthetic cohort, 1,287 had Alzheimer’s disease and a recorded diagnosis date. A first signal within the preceding 10 years was identified for 893 of them.

<p align="center">
  <img
    src="./assets/study/cohort-flow.png"
    width="100%"
    alt="Cohort flow and first-signal capture rate"
  />
</p>

**The candidate conditions were grouped into six clinical domains.** Cardiovascular, metabolic, renal, bone/frailty, mental, and hematology domains provided a consistent level of interpretation for comparing the domain composition of the first signals in shorter- and longer-interval groups.

**The effects of record count and observation-window length were also examined.** Because the first signal was defined as the earliest record, patients with more candidate-condition records had more opportunities for an older date to be selected. Starting domain, candidate-condition record count, and age were therefore considered together when assessing factors associated with the long-interval group. The observation window was also changed to 5, 10, and 15 years to compare changes in first-signal capture and interval values.

<p align="center">
  <img
    src="./assets/study/analysis-workflow.png"
    width="100%"
    alt="Five-step workflow for the Alzheimer’s EHR analysis"
  />
</p>

---

## 📊 Key Findings

### Record-Based Interval

A first signal within the 10-year observation window was identified for 893 patients. The median interval from the first signal to Alzheimer’s disease diagnosis was **2,198 days (approximately 6.0 years)**. The 25th and 75th percentiles were 1,258 and 2,968 days, respectively.

These cut points were used to define the **Short**, **Middle**, and **Long** interval groups.

<p align="center">
  <img
    src="./assets/results/delay-distribution.png"
    width="100%"
    alt="Distribution of the pre-diagnosis record-based interval"
  />
</p>

### Starting Domains

The Short group had relatively higher proportions of first signals in the bone/frailty and mental domains. The Long group had higher proportions in the renal and metabolic domains, while cardiovascular conditions accounted for a large share in all three interval groups.

In other words, the clinical-domain composition of the earliest candidate-condition record differed across interval groups.

<p align="center">
  <img
    src="./assets/results/starting-domain-map.png"
    width="100%"
    alt="Clinical-domain distribution of the first signal by interval group"
  />
</p>

### Effects of Record Count and Observation Window

The domain-distribution differences alone were not sufficient to conclude that the underlying diagnostic pathways differed. Because the first signal was defined as the earliest record, an older record was more likely to be selected for patients with more candidate-condition records.

The mean number of candidate-condition records was **3.12** in the Long group and **1.53** in the Short group.

<p align="center">
  <img
    src="./assets/results/observation-intensity.png"
    width="100%"
    alt="Comparison of candidate-condition record counts across interval groups"
  />
</p>

In the logistic-regression model that considered record count and age together, record count remained strongly associated with membership in the Long group. Some domain differences remained after adjustment, but the longer interval could not be explained by the first-signal domain alone.

<p align="center">
  <img
    src="./assets/results/adjusted-associations.png"
    width="100%"
    alt="Adjusted logistic-regression associations with the Long interval group"
  />
</p>

Extending the observation window from 5 to 15 years allowed older candidate-condition records to enter the analysis. The first-signal capture rate consequently increased from **49.0% to 82.1%**, while the median record-based interval increased from **1,113 to 3,412 days**.

These findings show that the absolute interval can vary with the observation-window definition.

<table>
  <tr>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-capture-rate.png"
        width="100%"
        alt="Sensitivity of the first-signal capture rate to the observation-window definition"
      />
      <br/>
      <sub>First-signal capture rate</sub>
    </td>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-median-delay.png"
        width="100%"
        alt="Sensitivity of the median record-based interval to the observation-window definition"
      />
      <br/>
      <sub>Median record-based interval</sub>
    </td>
  </tr>
</table>

---

## 🔍 Interpretation

The Short and Long groups differed in the clinical-domain composition of their first signals. However, these differences cannot be interpreted as differences in the time from actual disease onset to diagnosis.

The interval calculated in this study is the date difference between the earliest qualifying candidate-condition record within a defined observation window and the Alzheimer’s disease diagnosis date. Patients with more candidate-condition records, or those observed over a longer window, may have older records included; the resulting interval may therefore also become longer.

The findings were consequently interpreted as a pattern showing which clinical domains tended to appear first in the Long group, not as evidence that a specific domain delayed diagnosis. Record count and observation-window length were considered when interpreting this pattern.

---

## 🎤 Presentation and Materials

The research question, time-axis and cohort definitions, statistical analysis, interpretation, and oral presentation were completed as a solo project. The project received the **Grand Prize in the Oral Presentation category** at the 2026 Synthetic Data-Based Multi-Omics Hands-On Workshop.

<table>
  <tr>
    <td width="50%" align="center">
      <img src="./assets/event/presentation-photo.jpg" width="100%" alt="Oral presentation at the Multi-Omics Hands-On Workshop" />
      <br/>
      <sub>Oral presentation</sub>
    </td>
    <td width="50%" align="center">
      <img src="./assets/event/award-photo.jpg" width="100%" alt="Grand Prize in the oral presentation category" />
      <br/>
      <sub>Grand Prize in the Oral Presentation category</sub>
    </td>
  </tr>
</table>

### Project Materials

| Material | Link | Description |
|:---|:---|:---|
| Presentation | [2026 Multi-Omics Hands-On presentation](./materials/2026-multi-omics-presentation.pdf) | Research questions, time axis, cohort, analysis, and major findings |
| Poster | [2026 Multi-Omics Hands-On poster](./materials/2026-multi-omics-poster.pdf) | Summary of the design and findings |
| Abstract | [Presentation abstract](./materials/2026-multi-omics-abstract.pdf) | Background, methods, results, and conclusion |
| Award | [Grand Prize in the Oral Presentation category](./materials/2026-multi-omics-award.pdf) | Awarded on January 23, 2026 |
| Official news | [Gangwon LRS Shared University](https://www.gwlrs.ac.kr/ko/news/press/view/360?p=1) | Event and achievement-sharing news |
| Media coverage | [Lecturer News](https://www.lecturernews.com/news/articleView.html?idxno=195955) · [Enews Today](https://www.enewstoday.co.kr/news/articleView.html?idxno=2385680) · [The Kyosu Shinmun](https://www.kyosu.net/news/articleView.html?idxno=156225) | Coverage of the workshop and research presentations |

The repository contains the study design, aggregate findings, presentation materials, and event records.

---

## © Use of Materials

No open-source or Creative Commons license is granted for this repository.

Unless otherwise stated, the **README text and original overview diagrams or analysis figures created by the author** are made available for academic portfolio and review purposes. Please obtain prior permission before reusing, modifying, or redistributing these materials.

The source data are not included and remain subject to the terms of the data provider. Event photographs, award documents, institutional logos, news coverage, and other third-party content are excluded and remain subject to the rights and terms of their respective owners or providers.
