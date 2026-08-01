# 実験記録（自動生成）

| 項目 | 値 |
|------|----|
| **run_id** | `run-20260801T071847Z` |
| **シナリオ** | `api-spec-change-priority` |
| **リポジトリ** | `stack-s0` |

手動項目（CI・作業時間・コミット数など）は [手動記入](#manual) の表に追記してください。 スプレッドシートへそのまま貼る場合は [TSV（全列）](#tsv) を使えます。

**修正工数:** 主指標は `git_app`（`experiment/results/`・`experiment/metrics/` を除外したアプリ差分）。 `git` は実験メタデータ（結果 JSON 等）を含む参考値です。

## 自動収集サマリー

| フェーズ | 記録時刻 | PHPUnit | Newman | PHPStan | ESLint |
|:---------|:---------|:--------|:-------|:--------|:-------|
| ベースライン | `20260801T071847Z` | 47/47 (100.0%) | 13/13 (100.0%) | 0 件 | OK |
| 更新直後 | `20260801T080610Z` | 47/47 (100.0%) | 13/13 (100.0%) | 0 件 | OK |
| 修正後 | `20260801T083008Z` | 54/54 (100.0%) | 15/15 (100.0%) | 0 件 | OK |

<a id="manual"></a>

## 手動記入（実験者が追記）

| フェーズ | CI (失敗/総数) | 作業時間 (分) | アプリ変更ファイル | アプリ追加行 | アプリ削除行 | コミット数 | 手動バグ | メモ |
|:---------|:---------------|:--------------|:-------------------|:-------------|:-------------|:-----------|:---------|:-----|
| ベースライン | 4/4 | 5 | 0 | 0 | 0 | 1 | 0 | タグと差分ゼロの anchor コミット（`a059298`）。CI 4ジョブ緑（PHPUnit 47/47・Newman 13/13・PHPStan 0・ESLint OK） |
| 更新直後 | 4/4 | 46 | 13 | 114 | 7 | 1 | 0 | 実装のみ（`25a511c`、tests/Postman 未修正）。`priority` は**非破壊的な属性追加**のため既存テストが全通過し、CI 4ジョブとも緑（PHPUnit 47/47・Newman 13/13）。status 数値化シナリオと違いテスト赤が出ない点に注意 |
| 修正後 |  | 29 | 17 | 262 | 10 | 1 | 0 | tests 3ファイル＋Postman に priority のフィルタ/ソート検証を追加（`00ac775`、tests/postman のみ・実装修正なし）。ローカル `check-quality.sh` 一発緑（PHPUnit 54/54・Newman 15/15・PHPStan 0・ESLint OK）。**未 push のため CI 未実行** |

## フェーズ別詳細

### ベースライン (`baseline`)

- **JSON:** [`baseline.json`](experiment/metrics/runs/run-20260801T071847Z/baseline.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git_app（アプリ修正工数・主指標）:** 0 files, +0 / -0 (`（なし）`)
- **git_frontend（フロント別・第2章）:** 0 files, +0 / -0 (`（なし）`)
- **git_backend（バックエンド別・第2章）:** 0 files, +0 / -0 (`（なし）`)
- **git（実験メタデータ込み）:** 0 files, +0 / -0 (`（なし）`)

### 更新直後 (`after_update`)

- **JSON:** [`after_update.json`](experiment/metrics/runs/run-20260801T071847Z/after_update.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git_app（アプリ修正工数・主指標）:** 13 files, +114 / -7 (` 13 files changed, 114 insertions(+), 7 deletions(-)`)
- **git_frontend（フロント別・第2章）:** 2 files, +55 / -1 (` 2 files changed, 55 insertions(+), 1 deletion(-)`)
- **git_backend（バックエンド別・第2章）:** 11 files, +59 / -6 (` 11 files changed, 59 insertions(+), 6 deletions(-)`)
- **git（実験メタデータ込み）:** 13 files, +114 / -7 (` 13 files changed, 114 insertions(+), 7 deletions(-)`)

### 修正後 (`after_fix`)

- **JSON:** [`after_fix.json`](experiment/metrics/runs/run-20260801T071847Z/after_fix.json)
- **git diff_ref:** `experiment-baseline-v1`
- **git_app（アプリ修正工数・主指標）:** 17 files, +262 / -10 (` 17 files changed, 262 insertions(+), 10 deletions(-)`)
- **git_frontend（フロント別・第2章）:** 2 files, +55 / -1 (` 2 files changed, 55 insertions(+), 1 deletion(-)`)
- **git_backend（バックエンド別・第2章）:** 14 files, +199 / -7 (` 14 files changed, 199 insertions(+), 7 deletions(-)`)
- **git（実験メタデータ込み）:** 17 files, +262 / -10 (` 17 files changed, 262 insertions(+), 10 deletions(-)`)

<a id="tsv"></a>

<details>
<summary>スプレッドシート用 TSV（全列）</summary>

```tsv
repository	scenario	phase	recorded_at	phpunit_pass	phpunit_total	phpunit_pass_rate	newman_pass	newman_total	newman_pass_rate	phpstan_errors	eslint_ok	ci_jobs_failed	ci_jobs_total	work_minutes	app_files_changed	app_lines_added	app_lines_deleted	frontend_files_changed	frontend_lines_added	frontend_lines_deleted	backend_files_changed	backend_lines_added	backend_lines_deleted	meta_files_changed	meta_lines_added	meta_lines_deleted	commits	manual_bugs	metrics_json	notes
stack-s0	api-spec-change-priority	baseline	20260801T071847Z	47	47	100.0	13	13	100.0	0	1				0	0	0	0	0	0	0	0	0	0	0	0			experiment/metrics/runs/run-20260801T071847Z/baseline.json	
stack-s0	api-spec-change-priority	after_update	20260801T080610Z	47	47	100.0	13	13	100.0	0	1				13	114	7	2	55	1	11	59	6	13	114	7			experiment/metrics/runs/run-20260801T071847Z/after_update.json	 13 files changed, 114 insertions(+), 7 deletions(-)
stack-s0	api-spec-change-priority	after_fix	20260801T083008Z	54	54	100.0	15	15	100.0	0	1				17	262	10	2	55	1	14	199	7	17	262	10			experiment/metrics/runs/run-20260801T071847Z/after_fix.json	 17 files changed, 262 insertions(+), 10 deletions(-)
```

</details>
