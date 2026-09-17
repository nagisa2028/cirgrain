# 設計文書

cirgrain の設計文書の目次。各文書の担当範囲だけを書き、仕様の要約はここに置かない。

## 文書の種類

- **主題の文書**（下の表）: いま何が成り立つかを書く。決定が変われば書き換える。
- **決定記録**（[`decisions/`](decisions/README.md)）: なぜそう決めたかを書く。merge 後は書き換えない。
- 運用のルール（決定記録が要る場合、1 つの PR で揃えるもの）は [CONTRIBUTING.md](../CONTRIBUTING.md) の Documents にある。

## 主題の文書

状態: `未着手`（見出しのみ）/ `草案`（書きかけ、未確定の箇所あり）/ `確定`

| 文書 | 担当範囲 | 状態 |
| --- | --- | --- |
| [overview.md](overview.md) | 目的、位置付け、目標としないこと、長期目標 | 未着手 |
| [glossary.md](glossary.md) | 用語の定義。詳細な仕様は担当文書へリンクする | 未着手 |
| [architecture.md](architecture.md) | module の構成と依存方向、process ごとの module 選択、module 境界と serialization、controller と worker の通信 | 未着手 |
| [reconcile.md](reconcile.md) | 宣言型と reconcile、保守的な収束、実状態の観測、削除と finalizer の共通原則 | 未着手 |
| [identity.md](identity.md) | cloud / organization / project の階層、identity、API token と access token、RBAC | 未着手 |
| [api.md](api.md) | 利用者に公開する表現: resource、非同期操作、status、error、ID、wire format、versioning | 未着手 |
| [data-model.md](data-model.md) | 永続化するデータの共通規約: timestamp、`deleted_at`、文字列の上限、論理削除 | 未着手 |
| [compute.md](compute.md) | compute 固有の要求と設計 | 未着手 |
| [network.md](network.md) | network 固有の要求と設計 | 未着手 |
| [storage.md](storage.md) | storage 固有の要求と設計 | 未着手 |
| [image.md](image.md) | image 固有の要求と設計 | 未着手 |
| [operations.md](operations.md) | 前提条件、初期化、worker の参加、停止と復旧の運用 | 未着手 |
| [security.md](security.md) | 脅威モデルと、主題をまたぐ安全要件 | 未着手 |
| [testing.md](testing.md) | テスト方針、検証方法、検証環境。機能ごとの受け入れ条件は各主題の文書に置く | 未着手 |
| [open-questions.md](open-questions.md) | 未決事項、選択肢、影響する主題 | 未着手 |

領域ごとの文書（compute / network / storage / image）は [CONTRIBUTING.md](../CONTRIBUTING.md) の Areas に対応する。領域の定義元は Areas の表だけで、ここには置かない。

## 境界

重なりやすい主題の書き分け。共通の規約は一度だけ定義し、ほかの文書は参照する。

| 境界 | 前者に書くこと | 後者に書くこと |
| --- | --- | --- |
| architecture / operations | module の配置と通信の構造 | 初期化、参加、停止、復旧の手順と運用 |
| reconcile / api | 収束、観測、削除の共通原則 | 利用者に見える非同期操作、status、error の契約 |
| api / data-model | 外部に公開する表現 | 永続化するデータの共通規約 |
| identity / security | 階層、認証、認可の具体的な仕様 | 脅威モデルと横断的な安全要件 |
| 共通の文書 / 領域の文書 | 共通の規約 | 共通の規約への参照と、その領域固有の挙動 |

例: 削除の共通の流れは `reconcile.md`、`deleted_at` の保存規約は `data-model.md`、`Volume` を削除できる条件は `storage.md`。

## 主題の文書の書き方

機能や論点ごとに、要求・設計・検証を並べる。文書全体を「要求」章と「設計」章に二分しない。

```markdown
## Worker registration

### Requirements
何を満たすか、なぜ必要か。

### Design
どう実現するか。決定記録があればリンクする（[D-0003](decisions/0003-….md)）。未実装ならそう書く。

### Verification
要求を満たしたと判断する条件。
```

目次（この文書）、`glossary.md`、`open-questions.md` はこの形に従わず、それぞれの形で書く。
