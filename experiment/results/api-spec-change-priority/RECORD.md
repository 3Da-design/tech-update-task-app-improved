# 実験記録（自動生成）

| 項目 | 値 |
|------|----|
| **run_id** | `run-20260718T012901Z` |
| **シナリオ** | `api-spec-change-priority` |
| **リポジトリ** | `stack-s0` |

手動項目（CI・作業時間・コミット数など）は [手動記入](#manual) の表に追記してください。 スプレッドシートへそのまま貼る場合は [TSV（全列）](#tsv) を使えます。

**修正工数:** 主指標は `git_app`（`experiment/results/`・`experiment/metrics/` を除外したアプリ差分）。 `git` は実験メタデータ（結果 JSON 等）を含む参考値です。

## 自動収集サマリー

| フェーズ | 記録時刻 | PHPUnit | Newman | PHPStan | ESLint |
|:---------|:---------|:--------|:-------|:--------|:-------|
| ベースライン | `20260718T012901Z` | 47/47 (100.0%) | 13/13 (100.0%) | 0 件 | OK |
| 更新直後 | `20260718T014053Z` | 45/47 (95.7%) | 13/13 (100.0%) | 0 件 | OK |
| 修正後 | `20260718T020730Z` | 54/54 (100.0%) | 15/15 (100.0%) | 0 件 | OK |

<a id="manual"></a>

## 手動記入（実験者が追記）

| フェーズ | CI (失敗/総数) | 作業時間 (分) | アプリ変更ファイル | アプリ追加行 | アプリ削除行 | コミット数 | 手動バグ | メモ |
|:---------|:---------------|:--------------|:-------------------|:-------------|:-------------|:-----------|:---------|:-----|
| ベースライン | 4/4 | 10| 0 | 0 | 0 | 0 | 0 | tag と差分ゼロの anchor コミット。CI 4ジョブ緑 |
| 更新直後 | 3/4 | 45 | 12 | 117 | 11 | 1 | 0 | tests 未更新。PHP Tests のみ赤（PHPUnit 45/47）、他3ジョブ緑 |
| 修正後 | 4/4 | 70 | 18 | 263 | 11 | 1 | 2 | tests/Postman 更新＋実装バグ2件修正（Store の誤 `sometimes`／Update の priority 欠落）。PHPUnit 54/54・Newman 15/15。※9ae90b0 未 push・ローカル check-quality 全緑 |

## フェーズ別詳細

### ベースライン (`baseline`)

- **JSON:** [`baseline.json`](experiment/metrics/runs/run-20260718T012901Z/baseline.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git_app（アプリ修正工数・主指標）:** 0 files, +0 / -0 (`（なし）`)
- **git_frontend（フロント別・第2章）:** 0 files, +0 / -0 (`（なし）`)
- **git_backend（バックエンド別・第2章）:** 0 files, +0 / -0 (`（なし）`)
- **git（実験メタデータ込み）:** 0 files, +0 / -0 (`（なし）`)

### 更新直後 (`after_update`)

- **JSON:** [`after_update.json`](experiment/metrics/runs/run-20260718T012901Z/after_update.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git_app（アプリ修正工数・主指標）:** 12 files, +117 / -11 (` 12 files changed, 117 insertions(+), 11 deletions(-)`)
- **git_frontend（フロント別・第2章）:** 2 files, +55 / -1 (` 2 files changed, 55 insertions(+), 1 deletion(-)`)
- **git_backend（バックエンド別・第2章）:** 10 files, +62 / -10 (` 10 files changed, 62 insertions(+), 10 deletions(-)`)
- **git（実験メタデータ込み）:** 12 files, +117 / -11 (` 12 files changed, 117 insertions(+), 11 deletions(-)`)

### 修正後 (`after_fix`)

- **JSON:** [`after_fix.json`](experiment/metrics/runs/run-20260718T012901Z/after_fix.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git_app（アプリ修正工数・主指標）:** 18 files, +263 / -11 (` 18 files changed, 263 insertions(+), 11 deletions(-)`)
- **git_frontend（フロント別・第2章）:** 2 files, +55 / -1 (` 2 files changed, 55 insertions(+), 1 deletion(-)`)
- **git_backend（バックエンド別・第2章）:** 14 files, +199 / -7 (` 14 files changed, 199 insertions(+), 7 deletions(-)`)
- **git（実験メタデータ込み）:** 18 files, +263 / -11 (` 18 files changed, 263 insertions(+), 11 deletions(-)`)

<a id="tsv"></a>

<details>
<summary>スプレッドシート用 TSV（全列）</summary>

```tsv
repository	scenario	phase	recorded_at	phpunit_pass	phpunit_total	phpunit_pass_rate	newman_pass	newman_total	newman_pass_rate	phpstan_errors	eslint_ok	ci_jobs_failed	ci_jobs_total	work_minutes	app_files_changed	app_lines_added	app_lines_deleted	frontend_files_changed	frontend_lines_added	frontend_lines_deleted	backend_files_changed	backend_lines_added	backend_lines_deleted	meta_files_changed	meta_lines_added	meta_lines_deleted	commits	manual_bugs	metrics_json	notes
stack-s0	api-spec-change-priority	baseline	20260718T012901Z	47	47	100.0	13	13	100.0	0	1				0	0	0	0	0	0	0	0	0	0	0	0			experiment/metrics/runs/run-20260718T012901Z/baseline.json	
stack-s0	api-spec-change-priority	after_update	20260718T014053Z	45	47	95.74	13	13	100.0	0	1				12	117	11	2	55	1	10	62	10	12	117	11			experiment/metrics/runs/run-20260718T012901Z/after_update.json	 12 files changed, 117 insertions(+), 11 deletions(-)
stack-s0	api-spec-change-priority	after_fix	20260718T020730Z	54	54	100.0	15	15	100.0	0	1				18	263	11	2	55	1	14	199	7	18	263	11			experiment/metrics/runs/run-20260718T012901Z/after_fix.json	 18 files changed, 263 insertions(+), 11 deletions(-)
```

</details>
