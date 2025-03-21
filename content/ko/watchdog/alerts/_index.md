---
title: Watchdog 경고
---

## 개요

Watchdog은 시스템과 애플리케이션에서 이상 징후를 사전에 식별해 냅니다. 이상 징후를 식별하면 [Watchdog 알림 탐색기][1]에 이상 상태가 각각 표시되며, 발생한 상황, 다른 시스템에 미칠 수 있는 영향, 근본 원인에 대한 자세한 정보를 함께 제공해 드립니다.

{{< img src="watchdog/watchdog.png" alt="진행 중인 로그 이상 오류 경고 1개, 해결된 로그 이상 오류 1개, 근본 원인 분석을 통해 해결된 오류율 경고 1개가 표시된 Watchdog 경고 페이지" >}}

## Watchdog 경고 세부 사항

경고 개요 카드에는 다음 섹션이 포함되어 있습니다.

{{< img src="watchdog/alerts/alerts_overview.png" alt="sms-service의 send-sms 엔드포인트에서 높은 오류율을 보여주는 Watchdog 경고 카드의 스크린샷" style="width:100%;">}}

1. **상태**: 이상 상태는 `ongoing`, `resolved` 또는 `expired`일 수 있습니다. (이상 상태가 48시간 이상 지속되는 경우 `expired`입니다.)
3. **타임라인**: 이상이 발생한 기간을 설명합니다.
4. **메시지**: 이상 상태를 설명합니다.
5. **그래프**: 이상 상태를 시각화하여 나타냅니다.
6. **태그**: 이상 범위를 표시합니다.
7. [**영향**][4](해당되는 경우): 이상 상태가 영향을 미치는 사용자, 보기 또는 서비스를 설명합니다.

경고 개요 카드의 아무 곳이나 클릭하면 경고 상세 정보 창이 열립니다.

경고 개요 카드의 정보를 반복하는 것 외에도 **개요** 탭에는 다음 필드 중 하나 이상이 포함될 수 있습니다.

* **예상 범위**: **Show expected bounds** 확인란을 클릭합니다. 예상 동작과 비정상 동작을 구분하기 위해 그래프 색상이 변경됩니다.
* **제안하는 다음 단계**: 비정상적인 동작을 조사하고 분류하기 위한 단계를 설명합니다.
* **모니터링** 탭에는 경고와 관련된 모니터링이 나열됩니다. 표시된 각 모니터링에는 현재 경고와 관련된 메트릭과 해당 범위에 포함된 관련 태그가 존재합니다.

또한 Watchdog은 이상이 다시 발생하면 알림을 받을 목적으로 하나 이상의 모니터링을 생성할 것을 제안합니다. 해당 모니터링은 아직 존재하지 않으므로 테이블에 `suggested` 상태로 표시됩니다. 조직에 제안된 모니터링을 활성화하려면 **모니터링 활성화**를 클릭합니다. 새 모니터링을 생성하거나, 편집하거나, 복제하거나, 음소거하거나, 삭제할 수 있는 일련의 아이콘이 표시됩니다.

## Watchdog 경고 익스플로러

시간 범위, 검색창 또는 패싯을 사용하여 Watchdog 경고 피드를 필터링할 수 있습니다.

* **시간 범위**: 특정 시간 범위 내에서 감지된 경고를 보려면 오른쪽 상단의 시간 범위 선택기를 사용하세요. 지난 6개월 동안 발생한 모든 경고를 볼 수 있습니다.
* **검색창**: **경고 필터** 검색창에 텍스트를 입력하여 경고 타이틀을 검색합니다.
* **패싯**: Watchdog 경고 피드의 왼쪽에는 아래의 검색 패싯이 포함되어 있습니다. 패싯별로 경고를 필터링하려면 해당 상자를 선택하세요.

사용 가능한 패싯:

| 모든 경고 그룹    | 설명                                                                     |
|---------------------|---------------------------------------------------------------------------------|
| 경고 범주      | `apm`, `infrastructure` 또는 `logs` 경고를 모두 표시합니다.                          |
| 경고 유형          | 애플리케이션 성능 모니터링(APM) 또는 인프라스트럭처 통합의 메트릭을 사용하여 경고를 선택합니다.            |
| 경고 상태        | 상태별 경고를 선택합니다(`ongoing`, `resolved`, 또는 `expired`).     |
| APM 기본 태그     | 경고를 표시할 [정의된 APM 기본 태그][6]입니다.                        |
| 환경         | 환경에서 경고를 표시합니다. `env` 태그에 대한 자세한 내용을 확인하려면 [통합 서비스 태깅][5]을 참조하세요.|
| 서비스             | 서비스에서 경고를 표시합니다. `service` 태그에 대한 자세한 내용을 확인하려면 [통합 서비스 태깅][5]을 참조하세요.|
| 영향을 받는 최종 사용자   | (RUM 필요). Watchdog이 영향을 받는 최종 사용자를 식별한 경우입니다. 자세한 내용을 확인하려면 [영향 분석][4] 항목을 참조하세요. |
| 근본 원인          | (애플리케이션 성능 모니터링(APM) 필요). Watchdog이 이상 징후 또는 심각한 서비스 장애의 근본 원인을 발견한 경우입니다. 자세한 내용을 확인하려면 [근본 원인 분석][9] 항목을 참조하세요. |
| 팀                | 영향을 받은 서비스를 소유한 팀입니다. [Software Catalog][7]에서 강화되었습니다.  |
| 로그 이상 유형    | 해당 유형의 로그 이상만 표시합니다. 지원하는 유형은 신규 로그 패턴과 기존 로그 패턴의 증가입니다.|
| 로그 소스          | 해당 소스의 로그를 포함하는 경고만 표시합니다.                           |
| 로그 상태          | 해당 로그 상태의 로그를 포함하는 경고만 표시합니다.                         |

## Watchdog 경고 적용 범위

다중 애플리케이션 및 인프라스트럭처 메트릭을 다루는 Watchdog 경고:

{{< tabs >}}
{{% tab "로그 관리" %}}

수집한 로그는 수신 수준에서 분석되며, Watchdog은 `environment`, `service`, `source`, `status` 태그 이외에도 탐지된 패턴에 대한 집계를 수행합니다.
해당 방식으로 집계한 로그에서 아래와 같은 비정상적 동작이 있는지 검사합니다.

* 경고 또는 오류 상태의 로그 발생.
* 경고 또는 오류 상태 로그의 갑작스러운 증가.

로그 이상 상태는 모두 로그 익스플로러에 [통찰][3]로 표시되며, 검색 컨텍스트 및 역할에 적용된 제한 사항에 매칭됩니다.
Watchdog이 특히 `severe`라고 식별한 로그 이상 상태는 [Watchdog 경고 익스플로러][1]에 표시되며, [Watchdog 로그 모니터링][2]을 설정하여 알림을 받을 수 있습니다.
`severe` 이상은 다음과 같이 정의됩니다.

* 오류 로그 포함
* 최소 10분 동안 지속(일시적인 오류를 방지하기 위해).
* 큰 폭의 증가(작은 증가를 피하기 위해).
* 낮은 `noise` 점수 (특정 서비스에 대한 많은 경고 발생을 방지하기 위해). `noise` 점수는 서비스 수준에서 다음과 같이 계산됩니다.
    * 오류 패턴의 수를 살펴봅니다(높을수록 노이즈가 더 심함).
    * 패턴이 서로 얼마나 가까운지 계산합니다(가까울수록 노이즈가 더 심함).

#### 필수 데이터 기록

Watchdog이 예상 동작의 기준을 설정하려면 몇 가지 데이터가 필요합니다. 로그 이상 상태의 경우 최소 기록 내역은 24시간입니다. 
Watchdog은 필수 최소 기록이 확보되면 이상 징후을 찾기 시작하며, 기록량이 증가할수록 Watchdog의 성능이 향상됩니다. 6주분의 기록 내역이 존재할 때 성능은 최적화됩니다.

#### 로그 이상 감지 비활성화

로그 이상 감지를 비활성화하려면 [Log Management 파이프라인 페이지][4]로 이동하여  Log Anomalies 토글을 클릭합니다.

[1]: https://app.datadoghq.com/watchdog
[2]: /ko/monitors/types/watchdog/
[3]: /ko/watchdog/insights?tab=logmanagement#explore-insights
[4]: https://app.datadoghq.com/logs/pipelines
{{% /tab %}}
{{% tab "APM" %}}

Watchdog은 아래와 같은 메트릭에서 이상 징후를 찾기 위해 모든 서비스 및 리소스를 검사합니다.

  * 오류율
  * 레이턴시
  * 히트(요청률)

Watchdog은 거의 사용하지 않는 엔드포인트나 서비스를 필터링하여 노이즈를 줄이고 트래픽이 소량인 이상 상태를 배제합니다. 또한, 히트(요청률) 이상이 감지되었으나 레이턴시나 오류율에 영향을 미치지 않는 경우 해당 이상 상태는 무시됩니다.

#### 필수 데이터 기록

Watchdog이 예상 동작의 기준을 설정하려면 몇 가지 데이터가 필요합니다. 메트릭 이상 상태의 경우 최소 기록 내역은 2주입니다. 
Watchdog은 필수 최소 기록이 확보되면 이상 징후을 찾기 시작하며, 기록량이 증가할수록 Watchdog의 성능이 향상됩니다. 6주분의 기록 내역이 존재할 때 성능은 최적화됩니다.

{{% /tab %}}
{{% tab "USM" %}}

Watchdog은 아래와 같은 메트릭에서 이상 징후를 찾기 위해 모든 서비스 및 리소스를 검사합니다.

  * 오류율
  * 레이턴시
  * 히트(요청률)

Watchdog은 최소한으로 사용되는 엔드포인트와 서비스를 필터링하여 노이즈를 줄이고 소량의 트래픽에서 이상 현상을 방지합니다. 또한 적중률에 대한 이상이 탐지되었지만 대기 시간이나 오류율에 영향을 미치지 않는 경우 해당 이상은 무시됩니다.

#### 필수 데이터 기록

Watchdog은 예상되는 동작의 기준을 정의하기 위해 데이터를 필요로 합니다. 메트릭 이상 항목의 경우 최소 기록은 2주입니다. Watchdog은 최소 필수 기록을 사용할 수 있게 되면 이상 징후를 찾기 시작하며, 기록이 늘어나면 Watchdog이 향상됩니다. 6주간의 기록이 쌓이면 최상의 성능을 얻을 수 있습니다.

{{% /tab %}}
{{% tab "인프라스트럭처" %}}

Watchdog은 다음 통합에서 인프라스트럭처 메트릭을 확인합니다.

  * 호스트 수준 메모리 사용량(메모리 누수) 및 TCP 재전송 속도의 경우에는 [System][1].
  * [Redis][2]
  * [PostgreSQL][3]
  * [MySQL][15]
  * [SQLServer][16]
  * [Cassandra][17]
  * [Oracle Database][18]
  * [NGINX][4]
  * [도커(Docker)][13]
  * [쿠버네티스(Kubernetes)][14]
  * [Amazon Web Services][5]:
    * [S3][6]
    * [ELB/ALB/NLB][7]
    * [CloudFront][8]
    * [DynamoDB][9]
    * [RDS][10]
    * [ECS][11]
    * [Lambda][12]

#### 필수 데이터 기록

Watchdog이 예상 동작의 기준을 설정하려면 몇 가지 데이터가 필요합니다. 메트릭 이상 상태의 경우 최소 기록 내역은 2주입니다. 
Watchdog은 필수 최소 기록이 확보되면 이상 징후을 찾기 시작하며, 기록량이 증가할수록 Watchdog의 성능이 향상됩니다. 6주분의 기록 내역이 존재할 때 성능은 최적화됩니다.

[1]: /ko/integrations/system/
[2]: /ko/integrations/redisdb/
[3]: /ko/integrations/postgres/
[4]: /ko/integrations/nginx/
[5]: /ko/integrations/amazon_web_services/
[6]: /ko/integrations/amazon_s3/
[7]: /ko/integrations/amazon_elb/
[8]: /ko/integrations/amazon_cloudfront/
[9]: /ko/integrations/amazon_dynamodb/
[10]: /ko/integrations/amazon_rds/
[11]: /ko/containers/amazon_ecs/?tab=awscli
[12]: /ko/serverless/
[13]: /ko/containers/docker/?tab=standard
[14]: /ko/containers/kubernetes/installation/?tab=operator
[15]: /ko/integrations/mysql/
[16]: /ko/integrations/mysql/
[17]: /ko/integrations/cassandra/
[18]: /ko/integrations/oracle/
{{% /tab %}}
{{< /tabs >}}

### 이상 탐지 커스터마이징

Watchdog은 파워 모니터링 및 대시보드와 동일한 시즌 알고리즘을 사용합니다. 다른 메트릭에서 이상 징후를 찾아내거나 감도를 커스터마이징하려면 다음 알고리즘을 활용합니다.

* [이상 징후 모니터링][10]
* [예측 모니터링][11]
* [아웃라이어(outlier) 모니터링][12]

## Watchdog 경고를 확인할 수 있는 곳

Watchdog Alerts는 Datadog 내의 다음 위치에 나타납니다.

* [Watchdog 경고 익스플로러][1]
* 개별 [APM 서비스 페이지][3]
* [Software Catalog][7]에서
* 모든 익스플로러에서 사용할 수 있는 [Watchdog 통찰 패널][8]

### 애플리케이션 성능 모니터링(APM) 페이지의 워치독 쌍안경 아이콘

Watchdog이 APM 메트릭에서 불규칙성을 감지하면 [APM Software Catalog][7]에서 영향을 받는 서비스 옆에 분홍색 Watchdog 쌍안경 아이콘이 나타납니다.

{{< img src="watchdog/service_list.png" alt="5개 서비스를 보여주는 Software Catalog 스크린샷. 웹 스토어 서비스 이름 뒤에는 분홍색 쌍안경 아이콘이 표시됩니다." style="width:75%;" >}}

[서비스 페이지][3] 상단의 [Watchdog 통찰][8] 캐러셀에서 메트릭 이상 상태에 대한 자세한 내용을 확인할 수 있습니다.

메트릭 그래프에서도 Watchdog 아이콘을 찾을 수 있습니다.

{{< img src="watchdog/latency_graph.png" alt="y축에 서비스 레이턴시(초)를 표시하고 x축에 하루 중 시간을 표시하는 그래프. 전체 그래프가 분홍색으로 강조 표시되고 상단에 May 2: 13:31 Ongoing이라는 메시지가 표시됩니다." style="width:75%;" >}}

쌍안경 아이콘을 클릭하면 자세한 내용이 포함된 Watchdog 경고 카드를 볼 수 있습니다.

## 보관된 경고 관리

Watchdog 경고를 보관하려면 사이드 패널에서 오른쪽 상단 모서리에 있는 폴더 아이콘을 누릅니다. 경고를 보관하면 홈페이지와 같은 Datadog 사이트의 다른 위치뿐만 아니라 익스플로러에서 경고가 숨겨집니다. 경고가 보관되면 관련 서비스 또는 리소스 옆에 분홍색 Watchdog 쌍안경 아이콘이 표시되지 않습니다.

보관된 경고를 보려면 [Watchdog 경고 익스플로러][1]의 왼쪽 상단에 있는**Show _N_ archived alerts** 확인란 옵션을 선택합니다. 해당 옵션은 보관된 경고가 하나 이상 있는 경우에만 사용할 수 있습니다. 또한 각 경고를 보관한 사용자와 보관된 시기를 확인하고 해당 경고를 피드에 복원할 수 있습니다.

**참고**: 보관을 해도 Watchdog이 서비스 또는 리소스와 관련된 향후 문제에 플래그를 지정하는 것이 금지되지 않습니다.

[1]: /ko/watchdog
[3]: /ko/tracing/services/service_page/
[4]: /ko/watchdog/impact_analysis/
[5]: /ko/getting_started/tagging/unified_service_tagging/
[6]: /ko/tracing/guide/setting_primary_tags_to_scope/
[7]: /ko/tracing/software_catalog/
[8]: /ko/watchdog/insights?tab=logmanagement#explore-insights
[9]: /ko/watchdog/rca/
[10]: /ko/monitors/types/anomaly/
[11]: /ko/monitors/types/forecasts/?tab=linear
[12]: /ko/monitors/types/outlier/?tab=dbscan