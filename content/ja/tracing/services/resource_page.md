---
aliases:
- /ja/tracing/visualization/resource/
further_reading:
- link: /tracing/trace_collection/
  tag: ドキュメント
  text: アプリケーションで APM トレースをセットアップする方法
- link: /tracing/services/services_list/
  tag: ドキュメント
  text: Datadog に報告するサービスの一覧
- link: /tracing/services/service_page/
  tag: ドキュメント
  text: Datadog のサービスについて
- link: /tracing/trace_explorer/trace_view/
  tag: ドキュメント
  text: Datadog トレースの読み方を理解する
kind: documentation
title: リソースステータス画面
---

{{< img src="tracing/visualization/resource/ressource.png" alt="リソース"  >}}

リソースは、特定の[サービス][1]（通常は個々のエンドポイントまたはクエリ）に対する特定のアクションです。リソースの詳細については、[APM を開始する][2]をご覧ください。リソースごとに、APM は以下をカバーするダッシュボードページを自動的に生成します。

* 主要なヘルスメトリクス
* このサービスに関連付けられているすべてのモニターのモニターステータス
* このサービスに関連付けられているすべてのリソースのリストとメトリクス

## すぐに使えるグラフ

Datadog は、特定のリソースに対してすぐに使用できるグラフを提供しています。

* リクエスト - 選択して表示:
    *  **リクエストの合計量**
    *  **1 秒あたりのリクエスト**の量
* レイテンシー - 選択して表示:
    *  トレースされたリクエストの平均/p75/p90/p95/p99/最大レイテンシー
* エラー - 選択して表示:
    * **エラーの合計量**
    * **1 秒あたりのエラー**の量
    * **% エラー率**
* サブサービス: 複数のサービスが関係している場合、4 番目のグラフを使用して、サービスの**リクエストあたりの合計消費時間**/**消費時間の割合**/**平均時間**を*サービス*ごとまたは*タイプ*ごとに分類できます。

  これは、現在のサービスから他の*サービス*または*タイプ*への[トレース][3]に費やされた合計/相対/平均時間を表します。

  **注**: *Postgres* や *Redis* などのサービスは、他のサービスを呼び出さない「最終的な」オペレーションであり、サブサービスのグラフはありません。

{{< img src="tracing/visualization/resource/resource_otb_graphs.png" alt="すぐに使えるリソースグラフ"  style="width:90%;">}}

### ダッシュボードへのエクスポート

グラフを既存の[ダッシュボード][4]にエクスポートするには、各グラフの右上隅にある上向き矢印をクリックします。

### レイテンシー分布

リソースステータス画面にも、リソースレイテンシー分布グラフが表示されます。

{{< img src="tracing/visualization/resource/resource_latency_distribution.png" alt="レイテンシー分布"  style="width:100%;">}}

右上のセレクターを使用して特定のパーセンタイルを拡大するか、サイドバーにカーソルを合わせてパーセンタイルマーカーを表示します。

{{< img src="tracing/visualization/service/latency_distribution_sidebar.png" alt="レイテンシー分布セレクター"  style="width:50%;">}}

## 依存関係マップ

また、リソースの上流と下流のすべてのサービスの依存関係のマップを表示することができます。依存関係マップを使用すると、特定のリソース (エンドポイントやデータベースクエリなど) をエンドツーエンドで通過するスパンを持つサービスのフローをすばやく確認することができます。

依存関係マップは、サービスエントリースパンを含むリソースにのみ利用可能です。

{{<img alt="resource dependency map" src="tracing/visualization/resource/resource_dependency_map.png" style="width:100%;">}}

ノードにカーソルを合わせると、リクエスト/秒、エラーレート、平均レイテンシーなど、各サービスのメトリクスが表示されます。

ノードのハイライト色は、そのサービスの[モニターステータス][5]を示しています。サービスに複数のモニターが構成されている場合、最も厳しいモニターのステータスが表示されます。

{{<img src="tracing/visualization/resource/resource_dependency_map_hover.mp4" video="true" alt="hovering and clicking a resource dependency map node" style="width:100%;">}}

ノードをクリックすると、サービスページや関連するトレースなどを表示するオプションが付いたコンテキストメニューが表示されます。

## スパンサマリー

特定のリソースについて、Datadog は一致するすべてのトレースの[スパン][6]分析内訳を提供します。

{{< img src="tracing/visualization/resource/span_stats.png" alt="スパン統計"  style="width:80%;">}}

表示されるメトリクスは、スパンごとに次を表します。

`Avg Spans/trace`
: スパンが少なくとも 1 回存在する、現在のリソースを含むトレースのスパンの平均発生回数。

`% of Traces`
: スパンが少なくとも 1 回存在する現在のリソースを含むトレースの割合。

`Avg Duration`
: スパンが少なくとも 1 回存在する、現在のリソースを含むトレースのスパンの平均期間。

`Avg % Exec Time`
: スパンが少なくとも 1 回存在する、現在のリソースを含むトレースについて、スパンがアクティブだった実行時間の平均比率。

**注**: スパンは、子スパンの完了を待機していないときにアクティブと見なされます。特定のトレースの特定の時間にアクティブなスパンは、すべてリーフスパン（つまり、子のないスパン）です。

スパンサマリーテーブルは、サービスエントリースパンを含むリソースにのみ利用可能です。

## トレース

環境、サービス、オペレーション、およびリソース名で既にフィルタリングされている[トレース検索][8]モーダルで、このリソースに関連付けられている[トレース][7]のリストを参照してください。

{{< img src="tracing/visualization/resource/traces_list.png" alt="トレースの一覧画面"  style="width:90%;">}}

## {{< partial name="whats-next/whats-next.html" >}}

{{< partial name="whats-next/whats-next.html" >}}

[1]: /ja/tracing/glossary/#services
[2]: /ja/tracing/glossary/
[3]: /ja/tracing/glossary/#trace
[4]: /ja/dashboards/
[5]: /ja/monitors/manage/status/
[6]: /ja/tracing/glossary/#spans
[7]: /ja/tracing/trace_explorer/trace_view/
[8]: /ja/tracing/search/