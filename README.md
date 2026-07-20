<div align="center">

# EHR 기반 알츠하이머 진단 병목 지도

<p>
  <strong>한국어</strong> · <a href="./README.en.md">English</a>
</p>

<strong>
AD 진단 전에 가장 먼저 나타난 동반질환 기록을 찾고,<br/>
그 기록부터 진단일까지의 간격과 환자군별 임상 도메인 차이를 분석한 연구 프로젝트
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
프로젝트의 분석 흐름을 요약한 개요 도식입니다. 실제 분석 결과는 아래 발표자료 기반 그래프에서 확인할 수 있습니다.
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

알츠하이머병 진단 이전에는 고혈압, 당뇨병, 신장질환 등 여러 동반질환 기록이 축적될 수 있습니다. 그러나 진단 전에 어떤 임상 영역의 기록이 먼저 나타났고, 그 기록부터 진단일까지의 간격이 환자군에 따라 어떻게 다른지는 쉽게 파악하기 어렵습니다.

이 프로젝트에서는 진단일 이전 10년 동안 기록된 24개 후보질환 가운데 가장 이른 기록을 **첫 기록(first signal)**으로 정의했습니다. 첫 기록부터 알츠하이머 진단일까지의 날짜 차이를 **기록 기반 간격(record-based interval)**으로 계산하고, 첫 기록에 해당하는 질환을 여섯 개 임상 도메인으로 묶어 간격군별 구성을 비교했습니다.

개별 환자의 질환 위험을 예측하는 것이 아니라, 진단 전 기록이 어느 임상 영역에서 먼저 나타났고 그 기록부터 진단일까지의 간격이 어떤 조건에서 길게 관찰되는지를 살펴보는 데 초점을 두었습니다.

---

## ❓ 연구 질문

연구 질문은 네 가지였지만, 분석 흐름은 하나였습니다. 먼저 기록 기반 간격의 크기와 분포를 확인하고, 다음으로 첫 기록이 속한 임상 도메인을 비교했습니다. 이후 기록량을 고려했을 때에도 도메인 패턴이 유지되는지, 관찰기간을 바꾸면 결과가 어떻게 달라지는지를 확인했습니다.

<p align="center">
  <img
    src="./assets/study/research-questions.png"
    width="100%"
    alt="알츠하이머 EHR 분석 연구 질문"
  />
</p>

---

## ⏱️ 분석 설계

**분석 기준이 되는 시간축을 먼저 정의했습니다.** 알츠하이머 진단일을 **진단일(Index)**로 두고, 그 이전 10년을 기본 관찰기간으로 설정했습니다. 24개 후보질환 가운데 관찰기간 안에서 가장 먼저 기록된 날짜를 첫 기록으로 선택했습니다. 진단 당일과 이후의 기록은 제외하여, 진단 후 생성된 정보가 사전 기록에 포함되지 않도록 했습니다.

<p align="center">
  <img
    src="./assets/study/time-axis.png"
    width="100%"
    alt="알츠하이머 EHR 분석 시간축 정의"
  />
</p>

**이 기준에 따라 분석 대상 코호트를 구성했습니다.** 전체 합성 코호트 3,000명 가운데 AD 진단일이 확인되는 환자는 1,287명이었고, 이 중 893명에서 진단 전 10년 이내의 첫 기록을 확인할 수 있었습니다.

<p align="center">
  <img
    src="./assets/study/cohort-flow.png"
    width="100%"
    alt="알츠하이머 EHR 분석 코호트 선정 흐름과 포착률"
  />
</p>

**후보질환은 여섯 개 임상 도메인으로 묶었습니다.** 심혈관, 대사, 신장, 골·취약, 정신, 혈액 도메인으로 해석 단위를 통일하고, 기록 기반 간격이 짧은 환자군과 긴 환자군에서 첫 기록의 도메인 구성이 어떻게 다른지를 비교했습니다.

**기록량과 관찰기간의 영향도 함께 살펴보았습니다.** 첫 기록을 가장 이른 날짜로 정했기 때문에, 후보질환 기록이 많은 환자에서는 더 오래된 기록이 선택될 가능성이 있습니다. 이에 첫 기록의 도메인, 후보질환 기록량과 연령을 함께 고려해 긴 간격군과 관련되는 요인을 분석했습니다. 또한 관찰기간을 5년·10년·15년으로 변경하여 첫 기록 포착률과 간격값이 얼마나 달라지는지도 비교했습니다.

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

10년 관찰기간에서 첫 기록이 확인된 환자는 893명이었습니다. 첫 기록부터 AD 진단일까지의 간격은 중앙값 **2,198일(약 6.0년)**이었습니다. 분포의 25백분위수와 75백분위수는 각각 1,258일과 2,968일이었습니다.

이 분포를 기준으로 환자를 **짧은 간격군(Short)**, **중간 간격군(Middle)**, **긴 간격군(Long)**으로 구분했습니다.

<p align="center">
  <img
    src="./assets/results/delay-distribution.png"
    width="100%"
    alt="알츠하이머 진단 전 기록 기반 간격 분포"
  />
</p>

### 시작 도메인

짧은 간격군에서는 첫 기록이 골·취약 또는 정신 도메인에 속한 비중이 상대적으로 높았습니다. 긴 간격군에서는 신장과 대사 도메인의 비중이 높았고, 심혈관 도메인은 세 간격군 모두에서 큰 비중을 차지했습니다.

즉, 간격군에 따라 가장 먼저 기록된 후보질환의 임상 영역 구성이 다르게 나타났습니다.

<p align="center">
  <img
    src="./assets/results/starting-domain-map.png"
    width="100%"
    alt="간격군별 첫 기록의 임상 도메인 분포"
  />
</p>

### 기록량과 관찰기간의 영향

도메인 분포의 차이만으로 실제 진단 경로가 달랐다고 보기는 어려웠습니다. 첫 기록을 가장 이른 날짜로 정의했기 때문에, 후보질환 기록이 많은 환자에서는 더 오래된 기록이 선택될 가능성이 있었기 때문입니다.

실제로 긴 간격군의 평균 후보질환 기록량은 **3.12개**로, 짧은 간격군의 **1.53개**보다 많았습니다.

<p align="center">
  <img
    src="./assets/results/observation-intensity.png"
    width="100%"
    alt="간격군별 진단 전 후보질환 기록량 비교"
  />
</p>

기록량과 연령을 함께 고려한 로지스틱 회귀에서도 기록량은 긴 간격군과 강한 관련성을 보였습니다. 일부 도메인 차이는 보정 후에도 남았지만, 긴 간격이 첫 기록의 도메인만으로 설명된다고 보기는 어려웠습니다.

<p align="center">
  <img
    src="./assets/results/adjusted-associations.png"
    width="100%"
    alt="긴 간격군 연관요인 로지스틱 회귀 결과"
  />
</p>

관찰기간을 5년에서 15년으로 늘리면 더 오래된 후보질환 기록까지 분석에 포함될 수 있습니다. 이에 따라 첫 기록 포착률은 **49.0%에서 82.1%**로 증가했고, 기록 기반 간격의 중앙값도 **1,113일에서 3,412일**로 늘어났습니다.

이 결과는 기록 기반 간격의 절대값이 관찰기간 설정에 따라 달라질 수 있음을 보여줍니다.

<table>
  <tr>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-capture-rate.png"
        width="100%"
        alt="관찰기간 정의에 따른 첫 기록 포착률 민감도 분석"
      />
      <br/>
      <sub>첫 기록 포착률</sub>
    </td>
    <td width="50%" align="center">
      <img
        src="./assets/results/sensitivity-median-delay.png"
        width="100%"
        alt="관찰기간 정의에 따른 기록 기반 간격 중앙값 민감도 분석"
      />
      <br/>
      <sub>기록 기반 간격 중앙값</sub>
    </td>
  </tr>
</table>

---

## 🔍 결과 해석

짧은 간격군과 긴 간격군은 첫 기록이 속한 임상 도메인의 구성에서 차이를 보였습니다. 그러나 이 차이를 실제 발병부터 진단까지 걸린 시간의 차이로 해석할 수는 없습니다.

이 연구에서 계산한 간격은 실제 발병 시점이 아니라, 정해진 관찰기간 안에서 가장 먼저 확인된 후보질환 기록과 AD 진단일 사이의 날짜 차이입니다. 후보질환 기록이 많거나 관찰기간이 길면 더 과거의 기록이 포함될 수 있으므로, 계산된 간격도 함께 길어질 수 있습니다.

따라서 결과는 특정 임상 도메인이 진단을 지연시켰다는 의미가 아니라, 긴 간격군에서 어떤 임상 영역의 기록이 먼저 나타났는지를 보여주는 패턴으로 해석했습니다. 이 패턴을 읽을 때에는 기록량과 관찰기간의 영향을 함께 고려했습니다.

---

## 🎤 발표 및 자료

연구 질문 설정, 시간축과 코호트 정의, 통계분석, 결과 해석과 구두발표까지 전 과정을 단독으로 수행했습니다. 2026년 합성데이터 기반 Multi-Omics Hands-On 워크숍에서 **학술발표 부문 최우수상**을 수상했습니다.

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

저장소에는 분석 설계와 집계 결과, 발표자료 및 행사 기록을 정리했습니다.

---

## © 자료 이용 범위

이 저장소에는 별도의 오픈소스 또는 Creative Commons 라이선스를 적용하지 않습니다.

별도로 표시하지 않은 경우, **직접 작성한 README와 직접 제작한 개요 도식·분석 그림**은 학술 포트폴리오 및 검토 목적으로 공개합니다. 자료의 재사용, 수정 또는 재배포가 필요한 경우 사전에 문의해 주세요.

원본 데이터는 이 저장소에 포함하지 않으며, 데이터 이용 권한은 제공기관의 이용조건을 따릅니다. 행사 사진, 상장, 기관 로고, 기사 및 기타 제3자 콘텐츠는 위 이용 범위에서 제외되며 각 권리자와 제공기관의 조건을 따릅니다.
