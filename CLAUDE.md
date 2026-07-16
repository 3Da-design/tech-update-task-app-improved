# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) が本リポジトリで作業する際のガイダンスです。

## 必読（この順）

1. `../docs/EXPERIMENT-STACK.md` — 研究全体の正典（第1章完了・第2章方針・制約）
2. `../CLAUDE.md` — リポジトリ横断のルールと案内
3. 本ファイル
4. `docs/EXPERIMENT.md` — 第1章 improved 設計ドキュメント（本スタックの設計正典）

## 言語設定

ユーザーとのやり取り・説明・コミットメッセージ・コメントは **日本語**。コード識別子は英語可。

## リポジトリの位置づけ

| 項目 | 内容 |
|------|------|
| 研究テーマ | 技術更新に強い Web アプリ基盤の検討 |
| 章 | **第1章・第2章** |
| スタック ID | **S0 improved**（Laravel + Blade + Alpine.js） |
| 設計 | **improved**（Controller / Service / Repository / Interface の層分離） |
| 役割 | 第1章 improved の計測対象。第2章では **S0 基準点**（S1/S2 の **fork 元**） |

**目的:** 層分離の「良い例」。Web と API が同一の `TaskService` を共有し、仕様変更の修正を Service / Repository に集約できる構成を維持する。第2章 S1（HTML/JS）・S2（React）はここから fork される。

## 絶対に守る制約

1. **Fat Controller 化禁止** — `TaskService` / `TaskRepository` / `Contracts`（Interface）を削除・バイパスしない。
2. **ベースライン汚染禁止** — シナリオ変更（`priority` 追加等）は `exp/*` ブランチのみ。`main` / `experiment-baseline-v1` タグに混在させない。
3. **Docker Compose のみ** — ホストで `php artisan serve` / `npm install` を実行しない。
4. **ベースライン仕様** — タスク属性は `title` / `description` / `due_date` / `status` の4項目のみ（シナリオ前）。
5. **S1/S2 の基準点** — 本リポジトリの改変は下流（S1/S2）の比較基準に影響する。安易に構成を変えない。

## 開発環境

| 項目 | 値 |
|------|-----|
| Web（Laravel/nginx） | `http://localhost:8000` |
| Vite dev | `http://localhost:5173` |
| DB 公開ポート | `5432` |
| Compose 名 | `tech-update-task-app-improved`（ディレクトリ名由来） |
| コンテナ名 | `tech-update-task-app-{php,node,nginx,postgres}` |
| シードユーザー | `test@example.com` / `password` |

### 初回セットアップ

```bash
cp .env.example .env
docker compose up -d                                # vendor が無ければ entrypoint が composer install
docker compose exec app php artisan key:generate
docker compose exec app php artisan migrate --seed
composer npm:docker-build                           # ★ホストで実行（中身は node コンテナでの npm ci + build）
```

**`composer setup` を単体で使わないこと。** 実行場所がどちらでも完走しない：
コンテナ内（`docker compose exec app composer setup`）だと最終段 `npm:docker-build` が `docker` を呼ぶため `command not found` で落ち、
ホストだと `composer install` がホストの PHP で依存解決され、コンテナの PHP 8.4 とズレる。
上記のとおり **DB 操作はコンテナ内 / フロントビルドはホスト** に分けて実行する。

### よく使うコマンド

```bash
./scripts/check-quality.sh
docker compose exec app composer check     # phpstan + test
docker compose exec app composer phpstan
docker compose exec app composer test
./scripts/curl-api-smoke.sh
```

## アーキテクチャ（improved）

```text
Browser (Blade + Alpine.js)
    │
    ├─ Web\TaskController ─┐
    │                      ├─→ TaskService ─→ TaskRepository ─→ Task (Model)
    └─ API\TaskController ─┘
```

- `app/Http/Controllers/{Web,API,Auth,Concerns}/` — Web/API 二系統 + 認証
- `app/Services/` — `TaskService`（ユースケース）
- `app/Repositories/{,Contracts}/` — `TaskRepository` + Interface 抽象化

## 実験ワークフロー

```bash
docker compose exec app composer experiment:metrics -- --phase baseline    --diff-ref experiment-baseline-v1
docker compose exec app composer experiment:metrics -- --phase after_update --diff-ref experiment-baseline-v1
docker compose exec app composer experiment:metrics -- --phase after_fix    --diff-ref experiment-baseline-v1
docker compose exec app composer experiment:record  -- --scenario <id> --write
```

- 主指標: `git_app` の変更ファイル数・行数（`after_fix`）。通過率だけで判定しない。
- シナリオ手順: `docs/scenarios/*.md`（`api-spec-change-status-int` / `api-spec-change-priority` / `db-schema-change`）。
- 第1章 legacy との統合結果: `experiment/results/COMPARISON.md`。

## 関連ドキュメント

| ファイル | 内容 |
|----------|------|
| `../docs/EXPERIMENT-STACK.md` | 研究全体の正典 |
| `../CLAUDE.md` | リポジトリ横断ガイド |
| `docs/EXPERIMENT.md` | 第1章 improved 設計・指標定義 |
| `docs/scenarios/*.md` | 3シナリオ手順書 |
| `experiment/results/COMPARISON.md` | 第1章 legacy vs improved 統合結果 |
