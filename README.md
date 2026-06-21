# 開発プロセス標準化 Skill ライブラリ

ソフトウェア開発向けの再利用可能な Skill セットを管理し、`skills` 配下資材を一次ソースとして電子書籍化できるように運用するリポジトリです。

運用方針・Skill 体系・ガバナンスなどの詳細は [skills/README.md](skills/README.md) に集約しています。

## このライブラリの学習設計思想

> 「スキルを実行するたびに、開発者が少しずつプロのプロセス設計者になっていく」

このライブラリは単なる AI 実行手順集ではなく、使うほど上手くなる学習システムとして設計されています。

### 3つの学習設計原則

#### 1. 教育コンテキストを AI 実行手順と分離する

各 SKILL.md には `（教育）` サフィックスの付いたセクションが含まれます。AI エージェントはこれらを実行指示としては扱わず、開発者が学ぶための読み物として機能します。

| セクション | 役割 |
| --- | --- |
| `## このスキルが解く問題（教育）` | なぜこのフローが必要かを3行で説明する |
| `## 前提スキル / 次のステップ（教育）` | スキル間のナビゲーション（学習の地図） |
| `## 実行前の自己確認（開発者向け）（教育）` | Phase 1 開始前に開発者自身が確認するチェックリスト |

#### 2. 振り返りを証跡ログに組み込む

`assets/*-log-template.md` の末尾には `## 振り返り（Phase 4完了後に開発者が記入）` セクションがあります。スキルを実行するたびに振り返りを蓄積することで、習熟が自動化されます。

#### 3. AI スコープ境界を明示する

`（教育）` セクション冒頭の `<!-- AI実行対象外 -->` コメントが、AI エージェントへの実行スコープ境界シグナルです。AI は教育セクションを読むが、実行指示としては扱いません。

## 電子書籍生成ガイド（skills 資材ベース）

### 生成の考え方

- 一次ソースは `skills/` 配下の `SKILL.md`, `runbook.md`, `sub-skills/*.md`, `assets/*.md`
- ルート README は導線、ディレクトリ説明、クイズ同期ガイドを担う
- 電子書籍向けの構成編集は中間原稿で行い、元の Skill 資材は直接編集しない

### 標準フロー

1. `skills/` 配下で更新対象を確定する
2. 中間原稿（例: `docs/ebook-src/`）に章順で取り込む
3. 用語表記・見出し階層・重複説明を整える
4. 電子書籍ファイルを `ebook-output/` に出力する
5. 目次・リンク・図表番号・用語リンクを確認する

### 成果物の配置方針

- 一次ソース: `skills/`
- 生成用中間原稿: `docs/ebook-src/`（運用時に作成）
- 生成物: `ebook-output/`（運用時に作成）

## ディレクトリ説明（統合）

| パス | 役割 |
| --- | --- |
| `skills/` | Skill 本体、カテゴリ別 README、共有ガバナンス、共有テンプレート、共有参照を管理する中核ディレクトリ |
| `skills/010_requirements-and-planning/` | 要件・計画カテゴリの Skill 群 |
| `skills/020_design-and-implementation/` | 設計・実装カテゴリの Skill 群 |
| `skills/030_verification-and-quality/` | 検証・品質カテゴリの Skill 群 |
| `skills/040_operations-and-release/` | 運用・リリースカテゴリの Skill 群 |
| `skills/050_learning-and-improvement/` | 学習・改善カテゴリの Skill 群 |
| `skills/060_development-method/` | 開発方法論カテゴリの Skill 群 |
| `skills/shared-governance/` | 例外記録、四半期レビュー、KPI 月次ログなどの共通運用記録 |
| `skills/shared-templates/` | Skill 作成時のテンプレート群 |
| `skills/shared-references/` | 複数 Skill で使い回す用語集・ガイド・参照資料 |
| `.github/` | GitHub/Copilot 関連の補助設定・テンプレート |

## 利用導線

- Skill 全体の運用ルールを確認する: [skills/README.md](skills/README.md)
- Copilot 運用の共通ルールを確認する: [skills/shared-templates/copilot-instructions.md](skills/shared-templates/copilot-instructions.md)
- カテゴリ単位で Skill を選ぶ: `skills/*/README.md`
- 新規 Skill を追加する: `skills/shared-templates/skill/`
- 用語を確認する: `skills/shared-references/glossary.md`

## クイズ同期ガイド（統合版）

dev-process-skill-library の更新を spa-quiz-app に反映する際の基準です。

| クイズセクション | 主な一次ソース | 反映先ファイル |
| --- | --- | --- |
| 概論・運用導入 | [skills/README.md](skills/README.md)（対象読者、目的、全体フロー、RACI、KPI、共通運用） | `spa-quiz-app/src/data/dev-process-skill-library/intro-overview.json` |
| 要件・計画 | 010_requirements-and-planning 配下 Skill | `spa-quiz-app/src/data/dev-process-skill-library/requirements-planning.json` |
| 設計・実装 | 020_design-and-implementation 配下 Skill | `spa-quiz-app/src/data/dev-process-skill-library/design-implementation.json` |
| 検証・品質 | 030_verification-and-quality 配下 Skill | `spa-quiz-app/src/data/dev-process-skill-library/verification-quality.json` |
| 運用・リリース | 040_operations-and-release 配下 Skill | `spa-quiz-app/src/data/dev-process-skill-library/operations-release.json` |
| 学習・改善 | 050_learning-and-improvement 配下 Skill | `spa-quiz-app/src/data/dev-process-skill-library/learning-improvement.json` |

更新手順:

1. 一次ソース更新ファイルを抽出する
2. 影響するクイズセクションを特定する
3. 対象 JSON を更新する
4. 問数変更時は metadata の `totalQuestions` と `questionCount` を更新する
5. セクション変更時は quizSets 定義を更新する
6. `validate:quiz`, `validate:metadata`, `validate:all` を実行する
7. `sync-data`, `build` を実行して表示確認する
