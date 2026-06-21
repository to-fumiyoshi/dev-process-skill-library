# VALIDATION CHECKLIST

Skill を追加・更新したときの共通検証チェックリストです。
各項目は Pass / Fail の2値で判定し、Fail の場合は修正 PR を紐付けて再判定します。

## Layer A: Skill単体品質

- [ ] SKILL.md の frontmatter に `name`, `description`, `argument-hint`, `user-invocable`, `disable-model-invocation` が存在する
- [ ] `description` が「〜したいときに使う」「〜のときに使う」形式で始まり、ワークフローや実施内容のサマリーを含まない
- [ ] Phase 1〜4 と ゲート条件 #1 / #2 / #3 が定義されている
- [ ] sub-skills に phase1〜phase4 の実体ファイルが存在する
- [ ] `runbook.md` が存在し、SKILL.md から参照できる
- [ ] assets のログテンプレート参照が存在し、リンクが解決できる
- [ ] references または shared-references への参照リンクが解決できる
- [ ] 完了条件が判定可能な文で記述されている

## Layer B: ライブラリ整合品質

- [ ] 対象カテゴリの README に対象 Skill が列挙されている
- [ ] `skills/README.md` の Skill 体系マップ・利用可能一覧と矛盾しない
- [ ] 参照優先順位が `実装実体 > runbook > SKILL > 実行ログ` と整合している
- [ ] shared-references の参照リンクが解決できる
- [ ] `skills/shared-templates/copilot-instructions.md` が共通ルールとテンプレートの集約先として扱われている
- [ ] `.github/copilot-instructions.md` が最小ルール入口として維持され、詳細説明を `skills/shared-templates/copilot-instructions.md` へ委譲している
- [ ] 命名規約（kebab-case、カテゴリ配下配置）に一致している

## 運用ルール

- 判定値は `Pass` / `Fail` のみを使用する
- `Fail` の項目は修正 PR 番号を記録してから再判定する
- 一時的な例外は `skills/shared-governance/exception-log.md` に EX 採番で記録する
- 参照切れ判定は「リンク先ファイルの実在確認」で行う
