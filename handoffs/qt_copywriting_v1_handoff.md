# Quiet Tools トップページ 文言更新ハンドオフ

## 概要

Quiet Tools トップ（index.html）の日英コピーを整理。
4アプリ横断で自然につながるコンセプト文言に統一する。

---

## 方針

- ブランドコピー「Simple. Useful. Quiet.」は変更しない
- 日本語版：ヒーロー文言のみ調整。各アプリの日本語コピーは維持
- 英語版：ヒーロー文言 + 各アプリの英語説明文を更新
- 各アプリの h3（見出し）は日英ともに変更しない
- リンク構造・CSS・JS・レイアウトは維持。差分最小

---

## 変更ファイル

`projects/quiet-tools-web/index.html`（1ファイルのみ）

---

## 変更内容

### ヒーローセクション

| 要素 | 変更前 | 変更後 |
|---|---|---|
| JA 見出し | 日頃の細かくて忘れやすいタスクを、すぐ終わらせる。 | 日々の細かいことを、静かに片づける。 |
| JA 本文 2行目 | Quiet Tools はシンプルに役立つツールを作っています。 | Quiet Tools は、シンプルだけど役に立つツールを作っています。 |
| EN 見出し | Finish the small tasks you forget—fast. | Small tools for everyday clarity. |
| EN 本文（全文） | No bloat. Just the essentials—done quickly.<br>Quiet Tools builds small tools that quietly work. | Quiet Tools builds simple apps that help you organize, decide, and remember—without noise, clutter, or extra steps. |

### 各アプリ英語説明文（`<p class="lang-en">` のみ。h3 は変更しない）

#### DarumaKnock
- 変更前：`Quickly clean up extra subscriptions. See spending and renewal dates, and drop unused ones one by one.`
- 変更後：`Track subscriptions, renewal dates, and monthly costs in one place—and quietly let go of what no longer matters.`

#### TimeBud
- 変更前：`Type candidate times and get a ready-to-send message block. Time zones, handled fast.`
- 変更後：`Turn candidate times into a ready-to-send message block, so scheduling across time zones takes less effort.`

#### TravelGuard
- 変更前：`Manage insurance, visas, and emergency contacts before you fly. Leave nothing unchecked.`
- 変更後：`Keep trip essentials like visas, insurance, and emergency contacts together, so nothing important gets missed before departure.`

#### Dessin
- 変更前：`Record feelings, not items. What you really love won't leave.`
- 変更後：`Capture feelings, not just items, and keep a quiet record of what continues to stay with you over time.`

---

## 変更しないもの

- 各アプリの h3（日英ともに現状維持）
- 各アプリの日本語 p コピー（現状維持）
- JA ヒーロー本文 1行目：「余計な機能は増やさず、必要なことだけをサッと終わらせる。」（現状維持）
- リンク（Open / Support / Privacy / Terms）
- CSS・JS・セクション構造・レイアウト

---

## 実装手順

1. `feature/quiet-tools-copywriting-v1` ブランチ作成
2. `index.html` の該当テキストのみ差し替え
3. diff 確認（JP/EN 切り替え・リンク壊れなし）
4. PR 作成・マージ
