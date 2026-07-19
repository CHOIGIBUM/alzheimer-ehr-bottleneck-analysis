<div align="center">

# EHR 기반 알츠하이머 진단 병목 지도

<p>
  <strong>한국어</strong> · <a href="./README.en.md">English</a>
</p>

**진단 전 first signal과 AD 진단일 사이의 기록 기반 간격을 정의하고,  
지연군별 시작 임상 도메인과 관찰강도의 영향을 분석한 단독 연구 프로젝트**

![Event](https://img.shields.io/badge/2026-Multi--Omics%20Hands--On-147C8A)
![Data](https://img.shields.io/badge/Data-Synthetic%20EHR-5A8F99)
![Project](https://img.shields.io/badge/Project-Solo-0C4F5A)
![Analysis](https://img.shields.io/badge/Analysis-Logistic%20Regression-147C8A)
![Award](https://img.shields.io/badge/Award-Grand%20Prize-C5962A)

<br/>

<img
  src="./assets/overview/alzheimer-ehr-bottleneck-analysis.png"
  width="100%"
  alt="알츠하이머 EHR 병목 분석 프로젝트 개요"
/>

<sub>
프로젝트의 연구 설계와 분석 흐름을 요약한 개요 도식입니다. 실제 분석 결과는 아래 발표자료 기반 그림에서 확인할 수 있습니다.
</sub>

<br/><br/>

<a href="./materials/2026-multi-omics-presentation.pdf">
  <img src="https://img.shields.io/badge/발표자료-보기-147C8A?style=for-the-badge" alt="발표자료 보기" />
</a>
<a href="./materials/2026-multi-omics-poster.pdf">
  <img src="https://img.shields.io/badge/포스터-보기-147C8A?style=for-the-badge" alt="포스터 보기" />
</a>
<a href="./materials/2026-multi-omics-abstract.pdf">
  <img src="https://img.shields.io/badge/초록-보기-5A8F99?style=for-the-badge" alt="초록 보기" />
</a>
<a href="./materials/2026-multi-omics-award.pdf">
  <img src="https://img.shields.io/badge/상장-보기-C5962A?style=for-the-badge" alt="상장 보기" />
</a>
<a href="https://www.gwlrs.ac.kr/ko/news/press/view/360?p=1">
  <img src="https://img.shields.io/badge/행사%20소식-보기-5E6E73?style=for-the-badge" alt="행사 소식 보기" />
</a>

</div>

---

## 🧭 연구 개요

알츠하이머병 진단 이전에는 고혈압, 당뇨병, 신장질환 등 다양한 동반질환 기록이 축적될 수 있습니다. 그러나 이러한 기록이 어떤 임상 영역에서 시작되어 진단으로 이어졌는지를 시간축과 경로 관점에서 요약하기는 어렵습니다.

진단일 이전 10년의 관찰창에서 24개 후보질환 가운데 가장 이른 기록을 **first signal**로 정의했습니다. 이후 first signal부터 알츠하이머 진단일까지의 **기록 기반 간격(record-based interval)**을 계산하고, first signal에 해당하는 질환을 여섯 개 임상 도메인으로 분류했습니다.

분석의 중심은 개인의 실제 발병 시점을 추정하는 것이 아니라, 진단 전 EHR 기록이 어느 도메인에서 시작되었으며 기록 기반 간격이 환자군에 따라 어떻게 달라지는지를 살펴보는 데 있습니다.

<p align="center">
  <img
    src="./assets/study/problem-definition.png"
    width="100%"
    alt="알츠하이머 EHR 병목 분석의 문제 정의"
  />
</p>

---

## ❓ 연구 질문

분석은 기록 기반 간격, 시작 경로, 관찰강도와 분석 정의의 민감도를 순서대로 확인하도록 구성했습니다.

1. First signal부터 AD 진단일까지의 기록 기반 간격은 어느 정도이며 어떻게 분포하는가?
2. 간격이 짧은 군과 긴 군의 시작 임상 도메인은 어떻게 다른가?
3. 진단 전 기록량과 연령을 함께 고려한 뒤에도 도메인 패턴이 유지되는가?
4. Lookback을 5년, 10년, 15년으로 변경하면 포착률과 간격값은 얼마나 달라지는가?

<p align="center">
  <img
    src="./assets/study/research-questions.png"
    width="100%"
    alt="알츠하이머 EHR 분석 연구 질문"
  />
</p>

---

## ⏱️ 연구 설계

알츠하이머 진단일을 **Index**로 설정하고, Index 이전 10년을 기본 lookback으로 정의했습니다. Lookback 안에서 24개 후보질환의 날짜 중 가장 이른 날짜를 first signal로 선택했으며, `Index date - first signal date`를 기록 기반 간격으로 계산했습니다.

진단 이후에 생성된 정보가 사전 신호에 포함되지 않도록 Index 당일과 post-index 기록은 first signal 후보에서 제외했습니다.

<p align="center">
  <img
    src="./assets/study/time-axis.png"
    width="100%"
    alt="알츠하이머 EHR 분석 시간축 정의"
  />
</p>

<p align="center">
  <img
    src="./assets/study/leakage-control.png"
    width="100%"
    alt="알츠하이머 EHR 분석의 시간적 정보 누수 방지 규칙"
  />
</p>

---

## 🗂️ 데이터와 코호트

분석에는 COMPASS 플랫폼에서 제공된 **MIMICData Dementia/Alzheimer’s 합성 EHR**을 사용했습니다. 전체 3,000명 가운데 AD 진단 여부가 Yes이며 진단일이 존재하는 1,287명을 선정했습니다. 10년 lookback 안에서 first signal이 포착된 환자는 893명으로, 포착률은 69.4%였습니다.

24개 후보질환은 해석 단위를 일정하게 유지하기 위해 다음 여섯 개 도메인으로 매핑했습니다.

- **Cardiovascular:** 고혈압, 허혈성 심질환 등
- **Metabolic:** 제2형 당뇨병, 이상지질혈증 등
- **Renal:** 만성 신장질환, 말기 신부전 등
- **Bone/Frailty:** 골다공증, 골절 등
- **Mental:** 불안·공황, 우울 등
- **Hematology:** 빈혈, 결핍성 빈혈 등

<p align="center">
  <img
    src="./assets/study/cohort-flow.png"
    width="100%"
    alt="알츠하이머 EHR 분석 코호트 선정 흐름과 포착률"
  />
</p>

---

## 🧪 분석 방법

분석은 코호트 정의, first signal 추출, 기록 기반 간격 계산, 임상 도메인 매핑, 타당성 점검의 다섯 단계로 진행했습니다.

기록 기반 간격은 10년 lookback 분포의 분위수를 기준으로 구분했습니다.

- **Short:** 1,258일 이하
- **Middle:** 1,258일 초과 2,968일 미만
- **Long:** 2,968일 이상

Lookback 안에서 관찰된 후보 이벤트 수를 **기록량(event count)**으로 정의했습니다. 이후 Long 그룹 여부를 종속변수로 두고 시작 도메인, 기록량과 연령을 함께 포함한 로지스틱 회귀를 적용했습니다. 분석 정의에 따른 변화를 확인하기 위해 5년·10년·15년 lookback 민감도 분석도 수행했습니다.

<p align="center">
  <img
    src="./assets/study/analysis-workflow.png"
    width="100%"
    alt="알츠하이머 EHR 분석의 5단계 워크플로"
  />
</p>

---

## 📊 분석 결과

### 기록 기반 간격 분포

10년 lookback에서 first signal이 포착된 893명의 기록 기반 간격 중앙값은 **2,198일(약 6.0년)**이었습니다. IQR은 **1,258-2,968일**이었으며, 상위 25% 기준인 2,968일 이상을 Long 그룹으로 정의했습니다.

<p align="center">
  <img
    src="./assets/results/delay-distribution.png"
    width="100%"
    alt="알츠하이머 진단 전 기록 기반 간격 분포"
  />
</p>

### 시작 도메인 패턴

지연군별 first signal의 시작 도메인 구성에는 다음과 같은 상대적 차이가 나타났습니다.

- **Short 그룹:** Bone/Frailty와 Mental 비중이 상대적으로 높았습니다.
- **Long 그룹:** Renal과 Metabolic 비중이 상대적으로 증가했습니다.
- **Cardiovascular:** 모든 지연군에서 주요 시작 도메인으로 관찰되었습니다.

<p align="center">
  <img
    src="./assets/results/starting-domain-map.png"
    width="100%"
    alt="지연군별 first signal 시작 도메인 병목지도"
  />
</p>

### 관찰강도

Short 그룹의 평균 후보 이벤트 기록량은 **1.53개**, Long 그룹은 **3.12개**로 나타났습니다. 가장 이른 날짜를 first signal로 선택하는 구조에서는 기록이 많은 환자일수록 더 과거의 이벤트가 선택될 가능성이 있으므로, 기록량을 결과 해석과 함께 확인했습니다.

<p align="center">
  <img
    src="./assets/results/observation-intensity.png"
    width="100%"
    alt="지연군별 진단 전 후보 이벤트 기록량 비교"
  />
</p>

### 보정 분석

Long 그룹 여부를 종속변수로 두고 시작 도메인, 기록량과 연령을 함께 고려했습니다. 기록량이 많을수록 Long 그룹으로 관찰될 가능성이 증가하는 경향이 나타났으며, 일부 도메인 차이는 보정 이후에도 남았습니다.

<p align="center">
  <img
    src="./assets/results/adjusted-associations.png"
    width="100%"
    alt="Long 그룹 연관요인 로지스틱 회귀 결과"
  />
</p>

### 민감도 분석

Lookback을 길게 설정할수록 first signal 포착률이 증가했고, 선택될 수 있는 가장 이른 기록의 범위도 넓어져 기록 기반 간격의 중앙값이 함께 증가했습니다.

| Lookback | First signal 포착률 | 기록 기반 간격 중앙값 |
|:---:|---:|---:|
| 5년 | 49.0% | 1,113일 |
| 10년 | 69.4% | 2,198일 |
| 15년 | 82.1% | 3,412일 |

<table>
  <tr>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-capture-rate.png"
        width="100%"
        alt="Lookback 정의에 따른 first signal 포착률 민감도 분석"
      />
      <br/>
      <sub>First signal 포착률</sub>
    </td>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-median-delay.png"
        width="100%"
        alt="Lookback 정의에 따른 기록 기반 간격 중앙값 민감도 분석"
      />
      <br/>
      <sub>기록 기반 간격 중앙값</sub>
    </td>
  </tr>
</table>

---

## 🔍 결과 해석

지연군별 시작 도메인에서는 Short 그룹의 골·취약 및 정신 영역, Long 그룹의 신장 및 대사 영역 비중이 상대적으로 다르게 나타났습니다. 그러나 first signal을 가장 이른 기록으로 정의했기 때문에, 후보질환 기록이 많은 환자일수록 더 과거의 날짜가 선택될 가능성도 함께 고려해야 합니다.

실제로 Long 그룹에서는 진단 전 후보 이벤트 기록량이 더 많았으며, lookback을 변경했을 때 포착률과 간격의 중앙값도 함께 달라졌습니다. 따라서 이 지표는 실제 발병부터 진단까지의 시간을 직접 측정한 값이라기보다, 관찰기간과 기록량의 영향을 받는 **EHR 기반 간격**으로 해석했습니다.

분석의 핵심은 복잡한 모형을 적용하는 데 그치지 않고, 환자군·시간축·first signal과 관찰창의 정의가 결과에 미치는 영향을 함께 검토했다는 데 있습니다.

---

## 🎤 발표 및 수상

<table>
  <tr>
    <td width="50%" align="center">
      <img src="./assets/event/presentation-photo.jpg" width="100%" alt="Multi-Omics Hands-On 워크숍 구두발표 현장" />
      <br/>
      <sub>학술발표 현장</sub>
    </td>
    <td width="50%" align="center">
      <img src="./assets/event/award-photo.jpg" width="100%" alt="Multi-Omics Hands-On 워크숍 학술발표 최우수상 수상" />
      <br/>
      <sub>학술발표 부문 최우수상 수상</sub>
    </td>
  </tr>
</table>

---

## 📎 프로젝트 자료

| 자료 | 링크 | 내용 |
|:---|:---|:---|
| 발표자료 | [2026 Multi-Omics Hands-On 발표자료](./materials/2026-multi-omics-presentation.pdf) | 연구 질문, 시간축, 코호트, 분석 방법과 주요 결과 |
| 포스터 | [2026 Multi-Omics Hands-On 포스터](./materials/2026-multi-omics-poster.pdf) | 연구 설계와 결과 요약 |
| 초록 | [학술발표 초록](./materials/2026-multi-omics-abstract.pdf) | 배경·방법·결과·결론 정리 |
| 상장 | [학술발표 부문 최우수상](./materials/2026-multi-omics-award.pdf) | 2026년 1월 23일 수상 |
| 공식 소식 | [강원LRS공유대학](https://www.gwlrs.ac.kr/ko/news/press/view/360?p=1) | 행사 및 성과공유회 관련 소식 |
| 관련 보도 | [한국강사신문](https://www.lecturernews.com/news/articleView.html?idxno=195955) · [이뉴스투데이](https://www.enewstoday.co.kr/news/articleView.html?idxno=2385680) · [교수신문](https://www.kyosu.net/news/articleView.html?idxno=156225) | 워크숍 및 연구 발표 관련 보도 |

공개 저장소에는 연구 설계, 집계 결과, 발표 자료와 행사 기록을 중심으로 정리했으며 원본 데이터는 포함하지 않았습니다.

---

## 👤 수행 및 수상

| 구분 | 내용 |
|:---|:---|
| 수행 형태 | 단독 프로젝트 |
| 역할 | 연구 질문 설정, 시간축 및 first signal 정의, 코호트 구성, 임상 도메인 매핑, 통계분석, 결과 해석 및 구두발표 |
| 행사 | 합성데이터 기반 Multi-Omics Hands-On 워크숍 |
| 수상 | 학술발표 부문 최우수상 |

<div align="center">

**Solo Project · Research & Analysis · Grand Prize (Oral Presentation), 2026**

</div>
