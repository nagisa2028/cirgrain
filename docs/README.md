# 設計文書

cirgrain の設計文書の目次。

## 文書の種類

- **主題の文書**（下の表）: いま何が成り立つかを書く。決定が変われば書き換える。書き方は [template.md](template.md)。
- **決定記録**（[`decisions/`](decisions/README.md)）: なぜそう決めたかを書く。merge 後は書き換えない。
- **未決事項**（[open-questions.md](open-questions.md)）: まだ決まっていないこと。

運用のルール（決定記録が要る場合、1 つの PR で揃えるもの）は [CONTRIBUTING.md](../CONTRIBUTING.md) の Documents にある。

## 主題の文書

担当範囲は、全体の概要をまとめてから決める。それまでは空。主題の分け方自体も、そのときに見直す。

状態: `未着手`（見出しのみ）/ `草案`（書きかけ、未確定の箇所あり）/ `確定`

| 文書 | 概要 | 担当範囲 | 状態 |
| --- | --- | --- | --- |
| [overview.md](overview.md) | cirgrain とは何で、何のために作るか | | 未着手 |
| [glossary.md](glossary.md) | 用語の定義。ほかの文書から参照される側 | | 未着手 |
| [architecture.md](architecture.md) | システムを構成する要素と、そのつながり | | 未着手 |
| [reconcile.md](reconcile.md) | 望んだ状態に実際の状態を近づける仕組み | | 未着手 |
| [identity.md](identity.md) | 誰が何をできるか | | 未着手 |
| [api.md](api.md) | 利用者とシステムの接点 | | 未着手 |
| [data-model.md](data-model.md) | 永続化するデータ | | 未着手 |
| [compute.md](compute.md) | compute 領域 | | 未着手 |
| [network.md](network.md) | network 領域 | | 未着手 |
| [storage.md](storage.md) | storage 領域 | | 未着手 |
| [image.md](image.md) | image 領域 | | 未着手 |
| [operations.md](operations.md) | 運用 | | 未着手 |
| [security.md](security.md) | 安全性 | | 未着手 |
| [testing.md](testing.md) | 検証 | | 未着手 |
