<div align="center">

# EHR 기반 알츠하이머 진단 병목 지도

<p>
  <strong>한국어</strong> · <a href="./README.en.md">English</a>
</p>

<strong>
AD 진단 전 가장 이른 동반질환 기록을 기준으로,<br/>
기록 기반 간격과 시작 임상 도메인이 어떻게 달라지는지 분석한 단독 연구 프로젝트
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
  alt="알츠하이머 EHR 병목 분석 프로젝트 개요"
/>

<sub>
프로젝트의 시간축과 분석 흐름을 요약한 개요 도식입니다. 실제 분석 결과는 아래 발표자료 기반 그림에서 확인할 수 있습니다.
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

## 🧭 연구 배경

알츠하이머병 진단 이전에는 고혈압, 당뇨병, 신장질환 등 여러 동반질환 기록이 축적될 수 있습니다. 그러나 이러한 기록이 어느 임상 영역에서 시작되고, 어떤 흐름으로 진단에 이르는지를 한눈에 파악하기는 어렵습니다.

이 프로젝트에서는 진단 전 가장 이른 동반질환 기록을 **first signal**로 정의하고, 그 시점부터 알츠하이머 진단일까지의 **기록 기반 간격(record-based interval)**을 계산했습니다. First signal에 해당하는 질환은 임상 도메인으로 묶어, 간격이 짧은 환자군과 긴 환자군의 시작 경로를 비교했습니다.

개인의 질환 위험을 예측하기보다, 진단 전 EHR 기록이 어디에서 시작되고 그 간격이 어떤 조건에서 길게 관찰되는지를 설명하는 데 초점을 두었습니다.

---

## ❓ 연구 질문

분석은 기록 기반 간격의 분포, 시작 경로, 기록량의 영향과 관찰기간에 따른 변화를 순서대로 확인하도록 구성했습니다.

<p align="center">
  <img
    src="./assets/study/research-questions.png"
    width="100%"
    alt="알츠하이머 EHR 분석 연구 질문"
  />
</p>

---

## ⏱️ 분석 설계

**시간축을 먼저 고정했습니다.** 알츠하이머 진단일을 **Index**로 두고, 그 이전 10년을 기본 관찰창으로 설정했습니다. 24개 후보질환 가운데 Index 이전에 가장 먼저 기록된 날짜를 first signal로 선택했으며, 진단 당일과 이후 기록은 후보에서 제외했습니다.

<p align="center">
  <img
    src="./assets/study/time-axis.png"
    width="100%"
    alt="알츠하이머 EHR 분석 시간축 정의"
  />
</p>

**분석할 환자군을 시간축에 맞춰 좁혔습니다.** 전체 합성 코호트 3,000명 가운데 AD 진단일이 확인되는 환자는 1,287명이었고, 이 중 893명에서 10년 이내 first signal이 포착됐습니다.

<p align="center">
  <img
    src="./assets/study/cohort-flow.png"
    width="100%"
    alt="알츠하이머 EHR 분석 코호트 선정 흐름과 포착률"
  />
</p>

**개별 질환은 여섯 개 임상 도메인으로 묶었습니다.** 심혈관, 대사, 신장, 골·취약, 정신, 혈액 도메인으로 해석 단위를 통일해 지연군별 시작 경로를 비교했습니다.

**관찰된 차이를 한 번 더 확인했습니다.** 기록이 많은 환자에서는 더 과거의 이벤트가 first signal로 선택될 가능성이 있으므로, 시작 도메인과 함께 후보 이벤트 기록량과 연령을 고려했습니다. 또한 관찰창을 5년·10년·15년으로 바꾸어 결과가 분석 정의에 따라 얼마나 달라지는지도 비교했습니다.

<p align="center">
  <img
    src="./assets/study/analysis-workflow.png"
    width="100%"
    alt="알츠하이머 EHR 분석의 5단계 워크플로"
  />
</p>

---

## 📊 주요 결과

### 기록 기반 간격

10년 관찰창에서 first signal이 포착된 환자는 893명이었습니다. First signal부터 AD 진단일까지의 간격은 중앙값 **2,198일(약 6.0년)**이었고, 하위 25%와 상위 25%의 경계는 각각 1,258일과 2,968일이었습니다.

이 분포를 기준으로 간격이 짧은 **Short**, 중간 범위인 **Middle**, 긴 **Long** 그룹을 구분했습니다.

<p align="center">
  <img
    src="./assets/results/delay-distribution.png"
    width="100%"
    alt="알츠하이머 진단 전 기록 기반 간격 분포"
  />
</p>

### 시작 도메인

Short 그룹에서는 골·취약과 정신 도메인의 비중이 상대적으로 높았고, Long 그룹에서는 신장과 대사 도메인의 비중이 증가했습니다. 심혈관 도메인은 세 그룹 모두에서 주요 시작 영역으로 나타났습니다.

이 결과는 환자군에 따라 진단 전 기록이 시작된 임상 영역이 서로 다를 수 있음을 보여줍니다.

<p align="center">
  <img
    src="./assets/results/starting-domain-map.png"
    width="100%"
    alt="지연군별 first signal 시작 도메인 병목지도"
  />
</p>

### 지표의 타당성

시작 도메인 차이만으로 실제 진단 경로의 차이를 설명하기에는 부족했습니다. First signal을 가장 이른 기록으로 정의했기 때문에, 후보질환 기록이 많은 환자에서는 더 과거의 날짜가 선택될 가능성이 있기 때문입니다.

실제로 Long 그룹의 평균 후보 이벤트 기록량은 **3.12개**로, Short 그룹의 **1.53개**보다 많았습니다.

<p align="center">
  <img
    src="./assets/results/observation-intensity.png"
    width="100%"
    alt="지연군별 진단 전 후보 이벤트 기록량 비교"
  />
</p>

기록량과 연령을 함께 고려한 분석에서도 기록량은 Long 그룹과 강한 관련성을 보였습니다. 일부 도메인 차이는 보정 이후에도 남았지만, 도메인 패턴과 기록량의 영향을 분리해 해석할 필요가 있었습니다.

<p align="center">
  <img
    src="./assets/results/adjusted-associations.png"
    width="100%"
    alt="Long 그룹 연관요인 로지스틱 회귀 결과"
  />
</p>

관찰창을 5년에서 15년으로 늘리자 first signal 포착률은 **49.0%에서 82.1%**로 증가했고, 기록 기반 간격의 중앙값도 **1,113일에서 3,412일**로 늘어났습니다. 즉 간격의 절대값은 관찰기간의 정의와 분리해 해석하기 어려웠습니다.

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

지연군별로 first signal의 시작 도메인이 다르게 나타났지만, 그 차이를 실제 발병 이후의 진단 지연으로 단정하지 않았습니다. 기록량과 관찰창의 길이가 first signal의 선택과 간격값을 함께 변화시켰기 때문입니다.

따라서 이 프로젝트에서 계산한 간격은 질환 발생 시점을 나타내는 값이 아니라, 정해진 관찰창 안에서 가장 먼저 확인된 기록과 AD 진단일 사이의 **EHR 기반 간격**으로 해석했습니다.

핵심은 특정 도메인 패턴을 제시한 데 그치지 않고, 그 패턴이 어떤 시간축·기록량·지표 정의에서 만들어졌는지를 함께 확인했다는 데 있습니다.

---

## 🎤 발표 및 자료

이 프로젝트는 단독으로 수행했으며, 연구 질문과 시간축 정의부터 코호트 구성, 통계분석, 결과 해석과 구두발표까지 전 과정을 진행했습니다. 2026년 합성데이터 기반 Multi-Omics Hands-On 워크숍에서 **학술발표 부문 최우수상**을 수상했습니다.

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

### 프로젝트 자료

| 자료 | 링크 | 내용 |
|:---|:---|:---|
| 발표자료 | [2026 Multi-Omics Hands-On 발표자료](./materials/2026-multi-omics-presentation.pdf) | 연구 질문, 시간축, 코호트, 분석 방법과 주요 결과 |
| 포스터 | [2026 Multi-Omics Hands-On 포스터](./materials/2026-multi-omics-poster.pdf) | 연구 설계와 결과 요약 |
| 초록 | [학술발표 초록](./materials/2026-multi-omics-abstract.pdf) | 배경·방법·결과·결론 정리 |
| 상장 | [학술발표 부문 최우수상](./materials/2026-multi-omics-award.pdf) | 2026년 1월 23일 수상 |
| 공식 소식 | [강원LRS공유대학](https://www.gwlrs.ac.kr/ko/news/press/view/360?p=1) | 행사 및 성과공유회 관련 소식 |
| 관련 보도 | [한국강사신문](https://www.lecturernews.com/news/articleView.html?idxno=195955) · [이뉴스투데이](https://www.enewstoday.co.kr/news/articleView.html?idxno=2385680) · [교수신문](https://www.kyosu.net/news/articleView.html?idxno=156225) | 워크숍 및 연구 발표 관련 보도 |

저장소에는 연구 설계, 집계 결과, 발표자료와 행사 기록을 중심으로 정리했습니다.

---

## © 자료 이용 범위

이 저장소에는 별도의 오픈소스 또는 Creative Commons 라이선스를 적용하지 않습니다.

별도로 표시하지 않은 경우, **최기범이 직접 작성한 README와 자체 제작한 개요 도식·분석 그림**은 학술 포트폴리오 및 검토 목적으로 공개합니다. 자료의 재사용, 수정 또는 재배포가 필요한 경우 사전에 문의해 주세요.

원본 데이터는 이 저장소에 포함하지 않으며, 데이터 이용 권한은 제공기관의 이용조건을 따릅니다. 공동 제작 자료, 행사 사진, 상장, 기관 로고, 기사 및 기타 제3자 콘텐츠는 위 이용 범위에서 제외되며 각 권리자와 제공기관의 조건을 따릅니다.
