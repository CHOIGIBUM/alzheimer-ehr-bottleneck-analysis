<div align="center">

# EHR-Based Alzheimer’s Diagnostic Bottleneck Map

<p>
  <a href="./README.md">한국어</a> · <strong>English</strong>
</p>

<strong>
A solo research project examining how record-based intervals and starting clinical domains differ,<br/>
using the earliest pre-diagnosis comorbidity record as the first signal
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
This graphic summarizes the project timeline and analytical flow. Figures derived from the original presentation are shown below.
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

Before an Alzheimer’s disease diagnosis, records of hypertension, diabetes, kidney disease, and other comorbidities may accumulate over time. However, it is difficult to see at a glance where those records began and how they preceded the eventual diagnosis.

This project defined the earliest recorded pre-diagnosis comorbidity as the **first signal** and calculated the **record-based interval** from that signal to the Alzheimer’s disease diagnosis date. The condition corresponding to the first signal was grouped into a clinical domain, allowing the starting pathways of patients with shorter and longer intervals to be compared.

Rather than predicting individual disease risk, the analysis focused on where pre-diagnosis EHR records began and under what conditions the interval appeared longer.

---

## ❓ Research Questions

The analysis was organized to examine the interval distribution, starting pathways, the influence of observation intensity, and changes caused by the lookback definition.

<p align="center">
  <img
    src="./assets/study/research-questions.png"
    width="100%"
    alt="Research questions for the Alzheimer’s EHR analysis"
  />
</p>

---

## ⏱️ Analysis Design

**The time axis was fixed first.** The Alzheimer’s disease diagnosis date was set as the **Index**, and the preceding 10 years were used as the primary lookback window. Among 24 candidate conditions, the earliest date before the Index was selected as the first signal. Events recorded on the Index date or afterward were excluded.

<p align="center">
  <img
    src="./assets/study/time-axis.png"
    width="100%"
    alt="Time-axis definition for the Alzheimer’s EHR analysis"
  />
</p>

**The cohort was then narrowed according to that time axis.** Of 3,000 individuals in the synthetic cohort, 1,287 had Alzheimer’s disease and a recorded diagnosis date. A first signal within the 10-year lookback was captured for 893 of them.

<p align="center">
  <img
    src="./assets/study/cohort-flow.png"
    width="100%"
    alt="Cohort flow and first-signal capture rate"
  />
</p>

**Individual conditions were grouped into six clinical domains.** Cardiovascular, metabolic, renal, bone/frailty, mental, and hematology domains were used as a consistent level of interpretation for comparing starting pathways across interval groups.

**The observed differences were then re-examined.** Patients with more recorded candidate conditions had more opportunities for an earlier date to become the first signal. Starting domain, candidate-event count, and age were therefore considered together. The lookback window was also changed to 5, 10, and 15 years to assess how strongly the findings depended on the analytical definition.

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

A first signal within the 10-year lookback was captured for 893 patients. The median interval from first signal to Alzheimer’s disease diagnosis was **2,198 days (approximately 6.0 years)**. The 25th and 75th percentiles were 1,258 and 2,968 days, respectively.

These cut points were used to define the **Short**, **Middle**, and **Long** interval groups.

<p align="center">
  <img
    src="./assets/results/delay-distribution.png"
    width="100%"
    alt="Distribution of the pre-diagnosis record-based interval"
  />
</p>

### Starting Domains

The Short group had relatively higher proportions of bone/frailty and mental first signals, whereas the Long group showed higher proportions of renal and metabolic first signals. Cardiovascular conditions remained a major starting domain across all three groups.

This pattern suggests that the clinical domain in which pre-diagnosis records begin may differ across patient groups.

<p align="center">
  <img
    src="./assets/results/starting-domain-map.png"
    width="100%"
    alt="Starting-domain map by interval group"
  />
</p>

### Validity of the Indicator

Starting-domain differences alone were not sufficient to describe differences in the diagnostic pathway. Because the first signal was defined as the earliest record, patients with more candidate records had a greater chance of having an earlier date selected.

The mean candidate-event count was **3.12** in the Long group and **1.53** in the Short group.

<p align="center">
  <img
    src="./assets/results/observation-intensity.png"
    width="100%"
    alt="Comparison of candidate-event counts across interval groups"
  />
</p>

When event count and age were considered together, event count remained strongly associated with membership in the Long group. Some domain differences remained after adjustment, but domain patterns and observation intensity still needed to be interpreted separately.

<p align="center">
  <img
    src="./assets/results/adjusted-associations.png"
    width="100%"
    alt="Adjusted logistic-regression associations with the Long group"
  />
</p>

Extending the lookback window from 5 to 15 years increased the first-signal capture rate from **49.0% to 82.1%** and increased the median interval from **1,113 to 3,412 days**. The absolute interval therefore depended substantially on the observation-window definition.

<table>
  <tr>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-capture-rate.png"
        width="100%"
        alt="Sensitivity of the first-signal capture rate to the lookback definition"
      />
      <br/>
      <sub>First-signal capture rate</sub>
    </td>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-median-delay.png"
        width="100%"
        alt="Sensitivity of the median record-based interval to the lookback definition"
      />
      <br/>
      <sub>Median record-based interval</sub>
    </td>
  </tr>
</table>

---

## 🔍 Interpretation

The starting domain of the first signal differed across interval groups, but these differences were not interpreted as direct evidence of diagnostic delay after disease onset. Observation intensity and the length of the lookback window changed both the selected first signal and the resulting interval.

The interval in this project therefore represents the time between the earliest qualifying record within a defined observation window and the Alzheimer’s disease diagnosis date. It is an **EHR-based interval**, not an estimate of disease onset.

The central contribution of the analysis was not only to identify a domain pattern, but also to examine how that pattern was shaped by the time axis, record count, and indicator definition.

---

## 🎤 Presentation and Materials

This was a solo project covering the research question, time-axis definition, cohort construction, statistical analysis, interpretation, and oral presentation. It received the **Grand Prize in the Oral Presentation category** at the 2026 Synthetic Data-Based Multi-Omics Hands-On Workshop.

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

The repository is organized around the study design, aggregate findings, presentation materials, and event records.

---

## © Use of Materials

No open-source or Creative Commons license is granted for this repository.

Unless otherwise stated, the **README text and original overview diagrams or analysis figures authored by Gibum Choi** are made available for academic portfolio and review purposes. Please obtain prior permission before reusing, modifying, or redistributing these materials.

The source data are not included and remain subject to the terms of the data provider. Jointly authored materials, event photographs, award documents, institutional logos, news coverage, and other third-party content are excluded and remain subject to the rights and terms of their respective owners or providers.
