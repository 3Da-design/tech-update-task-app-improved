# 実験記録（自動生成）

| 項目 | 値 |
|------|----|
| **run_id** | `run-20260703T062340Z` |
| **シナリオ** | `api-spec-change-status-int` |
| **リポジトリ** | `improved` |

手動項目（CI・作業時間・コミット数など）は [手動記入](#manual) の表に追記してください。 スプレッドシートへそのまま貼る場合は [TSV（全列）](#tsv) を使えます。

## 自動収集サマリー

| フェーズ | 記録時刻 | PHPUnit | Newman | PHPStan | ESLint |
|:---------|:---------|:--------|:-------|:--------|:-------|
| ベースライン | `20260703T062340Z` | 47/47 (100.0%) | 13/13 (100.0%) | 0 件 | OK |
| 更新直後 | `20260703T062501Z` | 30/47 (63.8%) | 10/13 (76.9%) | 0 件 | OK |
| 修正後 | `20260703T062604Z` | 47/47 (100.0%) | 13/13 (100.0%) | 0 件 | OK |

<a id="manual"></a>

## 手動記入（実験者が追記）

| フェーズ | CI (失敗/総数) | 作業時間 (分) | 変更ファイル | 追加行 | 削除行 | コミット数 | 手動バグ | メモ |
|:---------|:---------------|:--------------|:-------------|:-------|:-------|:-----------|:---------|:-----|
| ベースライン | | 10 | 0 | 0 | 0 | 0 | 0 | 変更なし（baseline 計測） |
| 更新直後 | | 20 | 11 | 65 | 16 | 1 | 0 | PHPUnit 17失敗・Newman 3失敗（テスト・Postman未修正） |
| 修正後 | 4/4 | 30 | 15 | 87 | 38 | 2 | 0 | 主指標: 15 files, +87/-38。Controller 未変更 |

## フェーズ別詳細

### ベースライン (`baseline`)

- **JSON:** [`baseline.json`](experiment/metrics/runs/run-20260703T062340Z/baseline.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git:** 0 files, +0 / -0 (`（なし）`)

### 更新直後 (`after_update`)

- **JSON:** [`after_update.json`](experiment/metrics/runs/run-20260703T062340Z/after_update.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git:** 11 files, +65 / -16 (` 11 files changed, 65 insertions(+), 16 deletions(-)`)

### 修正後 (`after_fix`)

- **JSON:** [`after_fix.json`](experiment/metrics/runs/run-20260703T062340Z/after_fix.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git:** 15 files, +87 / -38 (` 15 files changed, 87 insertions(+), 38 deletions(-)`)

<a id="tsv"></a>

<details>
<summary>スプレッドシート用 TSV（全列）</summary>

```tsv
repository	scenario	phase	recorded_at	phpunit_pass	phpunit_total	phpunit_pass_rate	newman_pass	newman_total	newman_pass_rate	phpstan_errors	eslint_ok	ci_jobs_failed	ci_jobs_total	work_minutes	files_changed	lines_added	lines_deleted	commits	manual_bugs	metrics_json	notes
improved	api-spec-change-status-int	baseline	20260703T062340Z	47	47	100.0	13	13	100.0	0	1	0	4		0	0	0	0	0	experiment/metrics/runs/run-20260703T062340Z/baseline.json	変更なし（baseline 計測）
improved	api-spec-change-status-int	after_update	20260703T062501Z	30	47	63.83	10	13	76.92	0	1	2	4		11	65	16	1	0	experiment/metrics/runs/run-20260703T062340Z/after_update.json	PHPUnit 17失敗・Newman 3失敗（テスト・Postman未修正）
improved	api-spec-change-status-int	after_fix	20260703T062604Z	47	47	100.0	13	13	100.0	0	1	0	4		15	87	38	2	0	experiment/metrics/runs/run-20260703T062340Z/after_fix.json	主指標: 15 files, +87/-38。Controller 未変更
```

</details>
