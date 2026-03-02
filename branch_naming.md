# ブランチ命名規格

## 目的
この規則は、すべてのプロジェクトで一貫したブランチ名を用いることで、以下を達成する。

- 役割と目的が一目で分かる  
- 履歴・レビュー・検索を容易にする  
- CI/CD や自動化と連携しやすくする  
- 将来の大規模開発・AI 解析に耐えられる構造にする  
- プロジェクト横断で統一された Git 運用を実現する  

---

## 基本ルール
ブランチ名は次の形式に従う。

```
<prefix>/<short-description-with-hyphens>
```

### 使用できる文字
- 英小文字  
- 数字  
- ハイフン（`-`）  
- スラッシュ（`/`）  

### 禁止事項
- アンダーバー（`_`）は禁止  
- 日本語は禁止  
- スペースは禁止  
- 長すぎる説明は禁止  

### 理由
- ハイフンは世界的に最も一般的で、CLI・URL と相性が良い  
- アンダーバーは一部のツールで扱いづらく、国際的には少数派  
- 英語＋ハイフンは OSS のデファクトスタンダード  

---

## prefix（役割）
コミットメッセージの type と対応させる。

| prefix   | 用途                         | 例 |
|----------|------------------------------|-----|
| feat     | 新機能                       | `feat/add-login-page` |
| fix      | バグ修正                     | `fix/zero-input-crash` |
| refactor | 振る舞いを変えない整理       | `refactor/solver-structure` |
| perf     | パフォーマンス改善           | `perf/optimize-search-pruning` |
| docs     | ドキュメント                 | `docs/update-readme` |
| test     | テスト追加・修正             | `test/add-boundary-tests` |
| chore    | 雑務（設定・スクリプトなど） | `chore/update-dependencies` |
| build    | ビルド設定・依存関係         | `build/update-dockerfile` |
| ci       | CI 設定                      | `ci/add-lint-workflow` |

---

## short-description（説明部分）
- 英語で書く  
- 単語はハイフンで区切る  
- できるだけ短く、要点だけを書く  
- 「何をするブランチか」が一目で分かるようにする  

### 良い例
```
feat/add-recursive-solver
fix/zero-input-crash
refactor/expression-evaluator
docs/add-usage-examples
```

### 悪い例
```
feat/add_a_new_recursive_solver   ← アンダーバー禁止
fix/バグ修正                      ← 日本語禁止
feat/add-a-very-long-description-that-is-hard-to-read
```

---

## チケット番号との連携（任意）
タスク管理ツールを使う場合は、チケット番号を含めてもよい。

```
feat/123-add-recursive-solver
fix/456-handle-zero-input
```

---

## main ブランチの扱い
- `main` は常に動く状態を保つ  
- 直接コミットしない  
- 原則としてブランチを切ってからマージする  
- 大規模変更は専用ブランチを作成する  

---

## 例まとめ
```
feat/add-recursive-solver
feat/add-tchisla-cli
fix/zero-input-crash
refactor/solver-internal-structure
perf/optimize-search-pruning
docs/update-readme
test/add-boundary-tests
chore/cleanup-scripts
build/update-dockerfile
ci/add-github-actions
```

---

## この規格の特徴（世界標準との整合性）
- Conventional Commits と完全に対応  
- GitHub Flow / GitLab Flow と互換性あり  
- OSS の一般的な命名規則と一致  
- URL・CLI・CI/CD との相性が最適  
- AI による解析・分類が容易  
