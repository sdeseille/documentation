---
aliases:
- /ko/graphing/metrics/
- /ko/metrics/introduction/
- /ko/graphing/faq/inconsistent-sum-aggregation-between-different-time-windows-on-graph/
- /ko/dashboards/faq/inconsistent-sum-aggregation-between-different-time-windows-on-graph/
cascade:
  algolia:
    rank: 70
    tags:
    - 메트릭 제출
    - 메트릭 제출
title: 메트릭
---


{{< learning-center-callout header="Join an enablement webinar session" hide_image="true" btn_title="Sign Up" btn_url="https://www.datadoghq.com/technical-enablement/sessions/?tags.topics-0=Metrics">}}
  커스텀 메트릭에 대한 파운데이션 활성화 세션을 살펴보고 등록하세요. 커스텀 알고리즘에 대한 방문자 수, 평균 고객 장바구니 크기, 요청 지연 시간 또는 성능 분포 같은 애플리케이션 KPI를 추적하는 방법을 알아보세요.
{{< /learning-center-callout >}}

이 섹션에서는 Datadog 메트릭에 대한 소개 및 메트릭이 유용한 이유에 대해 설명합니다. 구체적으로 다음 주제가 포함되어 있습니다: 

{{< whatsnext desc="Datadog에 메트릭 제출하기" >}}
    {{< nextlink href="/metrics/custom_metrics">}}<u>커스텀 메트릭 제출하기</u> - 커스텀 메트릭이 무엇인지, 어떻게 제출하는 지에 대해 알아보세요.{{< /nextlink >}}
    {{< nextlink href="/opentelemetry/otel_metrics" >}}<u>OpenTelemetry 메트릭 전송하기</u> - Datadog Agent 또는 OpenTelemetry Collector를 설정하세요.{{< /nextlink >}}
    {{< nextlink href="/metrics/types" >}}<u>메트릭 유형</u> - Datadog에 제출할 수 있는 메트릭 유형입니다.{{< /nextlink >}}
    {{< nextlink href="/metrics/distributions" >}}<u>분포 메트릭</u> - 분포 메트릭과 전역적으로 정확한 백분위수에 대해 알아보세요.{{< /nextlink >}}
    {{< nextlink href="/metrics/units" >}}<u>메트릭 단위</u> - 메트릭과 연결될 수 있는 단위에 대해 알아보세요.{{< /nextlink >}}
{{< /whatsnext >}}

{{< whatsnext desc="Visualize and query your metrics" >}}
    {{< nextlink href="/metrics/explorer" >}}<u>메트릭 탐색기</u> - 모든 메트릭을 탐색하고 분석을 수행합니다.{{< /nextlink >}}
    {{< nextlink href="/metrics/summary" >}}<u>메트릭 요약</u> - Datadog 메트릭 활성 보고를 이해합니다.{{< /nextlink >}}
    {{< nextlink href="/metrics/advanced-filtering" >}}<u>고급 필터링</u> - 반환된 메트릭의 범위를 좁힐 수 있도록 데이터를 필터링합니다.{{< /nextlink >}}
    {{< nextlink href="/metrics/nested_queries" >}}<u>중첩 쿼리</u> - 고급 쿼리 기능을 해제하기 위해 추가 집계 레이어를 적용하세요.{{< /nextlink >}}
{{< /whatsnext >}}

{{< whatsnext desc="커스텀 메트릭 볼륨 및 비용에 대한 이해와 관리" >}}
    {{< nextlink href="metrics/metrics-without-limits/" >}}<u>Metrics without Limits™</u> - Metrics Without Limits™을 사용하여 태그 및 집계 설정으로 커스텀 메트릭 볼륨을 제어하는 ​​방법을 알아보세요.{{< /nextlink >}}
{{< /whatsnext >}}

## 개요
### 메트릭이란 무엇인가요?

메트릭이란 지연, 오류 비율에서 사용자 가입까지 시간에 따른 모든 환경 변화를 추적할 수 있는 숫자 값입니다.

Datadog에서 메트릭 데이터는 데이터 요소로 수집 및 저장되며 값과 타임스탬프를 포함합니다.

```text
[ 17.82,  22:11:01 ]
```

데이터 요소 시퀀스는 시계열로 저장됩니다.

```text
[ 17.82,  22:11:01 ]
[  6.38,  22:11:12 ]
[  2.87,  22:11:38 ]
[  7.06,  22:12:00 ]
```

초 단위 타임스탬프 이하로 쪼개진 모든 메트릭은 가장 가까운 초로 반올림됩니다. 동일한 타임스탬프를 지닌 요소가 있는 경우 나중 요소가 이전 요소를 덮어씁니다.

### 메트릭이 왜 유용한가요?

메트릭은 시스템에 대한 전반적인 그림을 제공합니다. 메트릭을 사용해 한눈에 환경 상태를 평가할 수 있습니다. 사용자가 얼마나 빠르게 웹사이트를 로딩하고 서버에서 평균 얼마의 메모리를 소비하는지 즉각적으로 시각화해 보여줍니다. 문제를 파악하면 [로그][1] 및 [추적][2]을 사용해 추가적으로 트러블슈팅할 수 있습니다.

시스템 상태를 추적하는 메트릭은 Datadog 통합에서 자동으로 {< translate key="통합_개수" >}}개 이상의 서비스를 사용해 수집됩니다. 또한 비즈니스에 밀접한 메트릭을 추적할 수 있습니다. 이는 커스텀 메트릭이라고도 알려져 있습니다. 사용자 로그인 횟수, 사용자 장바구니 규모, 팀의 코드 커밋 빈도 등을 추적할 수 있습니다.

또한 메트릭은 환경 규모를 조정하여 고객의 수요를 충족할 수 있도록 돕습니다. 리소스 소비량을 정확히 판단하면 성능을 개선하고 비용을 절감할 수 있습니다.

### Datadog에 메트릭 제출하기

메트릭은 여러 장소에서 Datadog로 전송될 수 있습니다.

- [Datadog 지원 통합][8]: Datadog의 {{< translate key="integration_count" >}}개 이상의 통합에는 기본으로 제공되는 메트릭이 포함되어 있습니다. 이러한 메트릭에 액세스하려면 해당 서비스의 특정 통합 페이지로 이동해 설치 지침을 따릅니다. 예를 들어, EC2 인스턴스를 모니터링해야 하는 경우 [Amazon EC2 통합 설명서][9]로 이동해야 합니다.

- Datadog 플랫폼 내에서 직접 메트릭을 생성할 수 있습니다. 예를 들어 로그에 표시되는 오류 상태 코드를 계산하고 Datadog에 [새로운 메트릭으로 저장][10]할 수 있습니다.

- 자주, 비즈니스와 관련된 메트릭을 추적해야 합니다. 예를 들어 사용자 로그인 횟수나 가입을 확인해야 할 수 있습니다. 이러한 경우 [커스텀 메트릭][11]을 만듭니다. 커스텀 메트릭은 [에이전트][12], [DogStatsD][13] 또는 [HTTP API][14]를 통해 제출할 수 있습니다.

- 또한 [Datadog 에이전트][15]는 자동으로 여러 표준 메트릭(CPU 또는 디스크 사용량 등)을 보냅니다.

모든 메트릭 제출 소스와 방법에 대한 요약을 보려면 [메트릭 유형 설명서][16]를 읽으세요.

### 메트릭 유형 및 실시간 메트릭 가시성

#### 메트릭 유형

Datadog는 다양한 메트릭 유형을 통해 고유한 사용 사례를 지원합니다. 개수, 게이지, 비율, 히스토그램, 분포가 그것입니다. 메트릭 유형은 앱에서 메트릭으로 활용할 수 있는 그래프와 함수를 결정합니다.

Datadog 에이전트는 전송되는 단일 데이터 요소마다 Datadog 서버에 별도의 요청을 보내지 않습니다. 대신 _플러시 시간 간격_ 동안 수집한 값을 보고합니다. 메트릭 유형은 이 시간 간격 동안 호스트에서 수집된 값이 제출을 위해 집계되는 방식을 결정합니다.

**_개수_** 유형을 시간 간격 동안 제출된 모든 값을 추가합니다. 예를 들어 웹사이트 방문수와 같은 메트릭을 추적하는 데 적합합니다.

**_비율_** 유형은 개수를 세고 시간 간격으로 나눕니다. "초당 방문수"에 관심이 있는 경우 유용합니다.

**_게이지_** 유형은 시간 간격 동안 보고된 마지막 값을 가져옵니다. 이 유형은 RAM 또는 CPU 사용량을 추적하는 데 적합합니다. 왜냐하면 마지막 값이 시간 간격 동안 호스트의 동작에 대한 상태를 잘 보여주기 때문입니다. 이 경우에 _개수_와 같은 다른 유형을 사용하면 부정확하고 극적인 값이 등장할 수 있습니다. 올바른 메트릭 유형을 선택하는 것이 정확한 데이터를 보장하는 방법입니다.

**히스토그램**은 제출된 값을 요약하는 5가지 각기 다른 값을 보고합니다. 평균, 개수, 중앙값, 95번째 백분위수 및 최대가 이에 해당합니다. 히스토그램은 다섯 개의 각기 다른 시계열을 생산합니다. 이 메트릭 유형은 지연과 같은 요소에 적합합니다. 왜냐하면 평균 값을 알기에 충분하지 않기 때문입니다. 히스토그램을 통해 매 단일 데이터 요소를 기록할 필요 없이 데이터가 어떻게 분포되어 있는지 이해할 수 있습니다.

**_분포_** 는 히스토그램과 비슷하지만 환경 내 모든 호스트에서 특정 시간 간격 동안 제출된 값을 요약합니다. 또한 다수의 백분위 수를 보고하도록 선택할 수 있습니다(p50, p75, p90, p95 및 p99). [배포 설명서][19]에서 이 강력한 기능에 대해 자세히 알아볼 수 있습니다.

각 메트릭 유형과 제출 지침에 대한 자세한 예시는 [메트릭 유형][16] 설명서를 참조하세요.

## 메트릭 쿼리

Datadog의 [메트릭 탐색기][3], [대시보드][4] 또는 [노트북][5]를 사용해 메트릭을 시각화하고 그래프를 만들 수 있습니다.

**팁**: Datadog의 글로벌 검색에서 메트릭 요약 페이지를 열려면 <kbd>Cmd/Ctrl</kbd> + <kbd>K</kbd> 를, `metrics`의 경우 검색을 누르세요.

시계열 시각화 예시는 다음과 같습니다.

{{< img src="metrics/introduction/timeseries_example.png" alt="여러 급등 지점과 함께 단일 파란 선으로 표시된 지연 메트릭 시계열 그래프" >}}

이 선 그래프는 사용자가 경험한 지연(밀리초 단위) Y축과 시간 X축을 보여줍니다. 

#### 추가 시각화

Datadog은 사용자가 메트릭을 쉽게 그래프로 표시하고 나타낼 수 있도록 다양한 시각화 옵션을 제공합니다.

메트릭 쿼리는 시작하기 위한 동일한 두 가지 평가 단계, 즉 시간 집계와 공간 집계로 구성됩니다. 자세한 내용은 [메트릭 쿼리의 구조][6]를 참조하세요.

{{< whatsnext desc="Metrics 사용자가 유용하게 여기는 두 가지 시각화 기능:">}}
    {{< nextlink href="dashboards/widgets/query_value/" >}}<u>쿼리 값 위젯</u> - 두 단계의 결과를 단일 값으로 줄입니다.{{< /nextlink >}}
    {{< nextlink href="/dashboards/widgets/top_list/" >}}<u>상위 목록</u> - 그룹당 단일 값을 반환합니다.{{< /nextlink >}}
{{< /whatsnext >}}

추가적으로 Datadog는 시각화를 위한 많은 유형의 그래프와 위젯을 보유하고 있습니다. Datadog의 [메트릭 그래프에 대한 블로그 시리즈]에서 자세히 알아볼 수 있습니다.

그래프화 경험은 대시보드, 노트북, 모니터를 사용하는지에 관계없이 일정합니다. 그래프화 편집기 UI를 사용하거나 직접 원본 쿼리열을 변경하여 그래프를 만들 수 있습니다. 쿼리 열을 편집하려면 맨 오른쪽의 `</>` 버튼을 사용합니다.

### 메트릭 쿼리 분석

Datadog의 메트릭 쿼리는 다음과 같습니다.

{{< img src="metrics/introduction/newanatomy.jpg" alt="색상 코딩된 섹션을 사용한 예시 쿼리" style="width:70%;">}}

이 쿼리를 몇 단계로 나눌 수 있습니다.

#### 메트릭 이름

먼저 **메트릭** 옆에 있는 드롭다운에서 검색하거나 선택하여 그래프화하려는 특정 메트릭을 고릅니다. 어느 메트릭을 사용해야 할지 확신이 들지 않는다면 메트릭 탐색기나 노트북으로 시작합니다. 또한 메트릭 요약 페이지에서 활성 보고 메트릭 목록을 확인할 수 있습니다.

#### 메트릭 필터링

메트릭을 선택한 후 태그를 기준으로 쿼리를 필터링할 수 있습니다. 예를 들어 `account:prod` 태그를 사용해 쿼리가 프로덕션 호스트의 메트릭만 포함하도록 _범위를 좁힐 수 있습니다._ 자세한 정보는 [태깅 설명서][17]를 읽어보세요.

#### 시간 집계 설정

다음으로, 시간 롤업을 사용하여 데이터의 세분성을 선택합니다. 이 예에서는 매 시간(3600초)마다 하나의 데이터 포인트가 있다고 정의했습니다. 각 시간 버킷의 데이터를 집계하는 방법을 선택할 수 있습니다. 기본적으로 _avg_가 적용되지만 사용 가능한 다른 옵션은 _sum_, _min_, _max_ 및 _count_입니다. 함수 또는 인애플리케이션 모디파이어를 사용하여 메트릭 데이터를 집계하고 버킷화하는 방법을 사용자 정의할 수도 있습니다. 예를 들어 최대값을 적용하고 메트릭 데이터가 달력 정렬 쿼리에 맞춰 적시에 롤업 및 버킷팅되는 방식을 사용자 정의하려면 `.rollup(max, 60)`를 사용합니다. 자세한 내용은 [함수][24], [롤업][23] 및 [인애플리케이션 모디파이어][25] 문서를 참조하세요.

#### 공간 집계 설정

Datadog에서 "공간"이란 각기 다른 호스트와 태그에서 메트릭이 분포되는 방법입니다. 공간에는 제어할 수 있는 두 가지 요소가 있습니다. 바로, 애그리게이터(aggregator)와 그룹화입니다.

_애그리게이터_는 각 그룹의 메트릭이 결합되는 방식을 정의합니다. 합계(sum), 최소(min), 최대(max) 및 평균(avg)과 같은 4가지 집계가 있습니다.

_그룹화_는 그래프의 선을 구성하는 요소들을 정의합니다. 예를 들어 4개 지역에 걸쳐 수백 개의 호스트가 있는 경우 지역별 그룹화를 통해 각 지역을 하나의 선으로 그래프화할 수 있습니다. 이를 통해 많은 시계열을 4개로 줄일 수 있습니다.

#### 함수 적용(선택사항)

수학적 [함수][18]를 통해 그래프 값을 수정할 수 있습니다. 즉, 정수와 메트릭(예를 들어, 메트릭 2배 증가) 간 산술을 수행할 수 있습니다. 예를 들어, 메모리 활용률에 대한 새 시계열로 `jvm.heap_memory / jvm.heap_memory_max`을(를) 만들 수 있습니다.

### 시간 및 공간 집계

_시간 집계_ 및 _공간 집계_는 모든 쿼리에서 중요한 두 개의 구성 요소입니다. 이러한 집계의 작동 방식을 이해하면 그래프 오해석을 방지할 수 있으므로 이러한 개념은 아래에서 더 자세히 설명됩니다.

#### 시간 집계

Datadog는 데이터 요소를 대량으로 저장합니다. 대부분 그래프로 모두 표시하는 것이 불가능합니다 .픽셀보다 더 많은 데이터 요소가 있을 것입니다. Datadog는 시간 집계를 사용해 이 문제를 해결합니다. 데이터 요소를 시간 범위로 구분합니다. 예를 들어 4시간 볼륨을 확인하는 경우, 데이터 요소는 2분 단위로 구분됩니다. 이것을 _롤업_이라고 부릅니다. 쿼리에 대해 결정한 시간 간격이 늘어날 수록 데이터의 세분성이 줄어듭니다.

각 시간 범위로 데이터를 결합하는 데 사용할 수 있는 5가지 집계, 즉 합계(sum), 최소(min), 최대(max), 평균(avg) 및 개수(count)가 있습니다.

시간 집계는 _항상_ 만드는 모든 쿼리에 적용된다는 사실을 기억하는 것이 중요합니다.

#### 공간 집계

공간 집계는 단일 메트릭을 태그(호스트, 컨테이너, 지역 등)를 사용해 여러 시계열로 나눕니다. 예를 들어 지역별 EC2 인스턴스 지연을 확인하려면 각 지역의 호스트 결합을 위해 기능별로 공간 집계 그룹화를 사용해야 합니다.

공간 집계를 사용하여 적용할 수 있는 4가지 집계에는 _합계(sum)_, _최소(min)_, _최대(max)_ 및 _평균(avg)_이 있습니다. 위 예시를 사용하고 4개 지역(us-east-1, us-east-2, us-west-1 및 us-west-2)에 호스트가 퍼져 있는 경우를 생각해 봅시다. 각 지역의 호스트는 애그리게이터 함수를 사용해 결합해야 합니다. _최대_ 애그리게이터_를 사용하면 호스트 전반에서 경험한 최대 지연이 표시됩니다. _평균_애그리게이터_를 사용하면 지역별 평균 지연이 표시됩니다.

#### 중첩 쿼리
UI에서 또는 [API][27]을 통해 중첩된 쿼리를 사용하여 시간과 공간의 기존 쿼리 결과에 추가 집계 레이어를 추가합니다. 자세한 내용은 [중첩된 쿼리][26] 설명서를 참조하세요.


### 메트릭에 대한 실시간 정보 보기

[메트릭 요약 페이지][20]는 지정된 시간(지난 시간, 지난일, 지난주)에 Datadog에 보고된 메트릭 목록을 표시합니다. 메트릭은 메트릭 이름이나 태그로 필터링할 수 있습니다. 

아무 메트릭 이름을 클릭하여 더 자세한 정보를 담은 상세 정보 사이드 패널을 표시합니다. 사이드 패널에 표시되는 상세 정보는 특정 메트릭에 대한 핵심 정보로 메타데이터(유형, 단위, 간격), 메트릭 개수, 보고 호스트 개수, 제출된 태그 개수, 메트릭에 제출된 모든 태그를 포함하는 표를 포함합니다. 메트릭에 제출된 태그를 확인하면 태그 설정으로 보고된 메트릭 수를 이해하는 데 도움이 됩니다. 이 수는 태그 값 조합에 따라 달라집니다.

**참고:** 메트릭 요약의 상세 정보 사이드 패널에 보고된 메트릭 수가 빌링에 반영되는 것이 아닙니다. 지난 달 사용량에 대한 정확한 계산은 [사용량 상세 정보][21]을 참조하세요.

자세한 정보는 [메트릭 요약 설명서][22]를 읽으세요.

## 참고 자료

{{< whatsnext desc="메트릭에 대해 다음 내용도 확인하세요.">}}
    {{< nextlink href="/metrics/advanced-filtering" >}}<u>고급 필터링</u> - 데이터를 필터링하여 반환되는 메트릭의 범위를 좁힙니다.{{< /nextlink >}}
    {{< nextlink href="/metrics/distributions" >}}<u>분포 메트릭</u> - 전체 데이터 세트에서 글로벌 백분위수를 계산하세요.{{< /nextlink >}}
    {{< nextlink href="metrics/metrics-without-limits/" >}}<u>Metrics without Limits™</u> - Metrics Without Limits™을 사용하여 태그 및 집계 설정으로 커스텀 메트릭 볼륨을 제어하는 ​​방법을 알아보세요.{{< /nextlink >}}
    {{< nextlink href="https://dtdg.co/fe" >}}<u>기본 구축</u> - 인터랙티브 세션에 참여하여 메트릭에 대해 자세히 알아보세요.{{< /nextlink >}}
{{< /whatsnext >}}

[1]: /ko/logs
[2]: /ko/tracing/
[3]: /ko/metrics/explorer/
[4]: /ko/dashboards/
[5]: /ko/notebooks/
[6]: https://docs.datadoghq.com/ko/metrics/#anatomy-of-a-metric-query
[7]: https://www.datadoghq.com/blog/timeseries-metric-graphs-101/
[8]: /ko/integrations/
[9]: /ko/integrations/amazon_ec2/
[10]: /ko/logs/logs_to_metrics/
[11]: /ko/metrics/custom_metrics/
[12]: /ko/agent/
[13]: /ko/metrics/custom_metrics/dogstatsd_metrics_submission/
[14]: /ko/api/
[15]: https://docs.datadoghq.com/ko/agent/basic_agent_usage/
[16]: /ko/metrics/types/
[17]: /ko/getting_started/tagging/using_tags/
[18]: /ko/dashboards/functions/
[19]: /ko/metrics/distributions/
[20]: https://app.datadoghq.com/metric/summary
[21]: /ko/account_management/plan_and_usage/usage_details/
[22]: /ko/metrics/summary/
[23]: /ko/dashboards/functions/rollup/#rollup-with-calendar-aligned-queries
[24]: /ko/dashboards/functions/
[25]: /ko/metrics/custom_metrics/type_modifiers/?tab=count#in-application-modifiers
[26]: /ko/metrics/nested_queries
[27]: https://docs.datadoghq.com/ko/api/latest/metrics/#query-timeseries-data-across-multiple-products