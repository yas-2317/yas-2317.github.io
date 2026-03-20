# Quiet Tools トップページ 構成改善ハンドオフ

## 概要

トップページを「ブランドトップ + 4アプリ一覧」として素直に読めるよう構成を整理する。
文言は変更しない。削る・優先順位を整理する・見せ方を揃えることが主目的。

---

## 現状の課題（index.html ベースで確認済み）

| 課題 | 現状の該当箇所 |
|---|---|
| ブランドコピーの重複 | topbar の `tagline-pill`（lang-ja: 「シンプルだけど、役に立つ。」）と hero の `kicker`（SIMPLE • USEFUL • QUIET）が二重に存在 |
| カテゴリ見出しが不要 | `group-label` に DAILY / MEMORY があり、4本しかない現段階では認知コストになっている |
| カード内 CTA が均等 | Open / Support / Privacy / Terms がすべて同じ `.btn` スタイルで並んでいて、主 CTA が埋もれている |

---

## 変更内容

### 1. ブランドコピーの重複解消

**削除:** hero セクション内の kicker（2行）を削除

```html
<!-- 削除する -->
<div class="kicker lang-ja">SIMPLE • USEFUL • QUIET</div>
<div class="kicker lang-en">SIMPLE • USEFUL • QUIET</div>
```

**修正:** topbar の tagline-pill を lang 分けせず「Simple. Useful. Quiet.」1本に統一

```html
<!-- 変更前 -->
<div class="tagline-pill lang-ja">シンプルだけど、役に立つ。</div>
<div class="tagline-pill lang-en">Simple. Useful. Quiet.</div>

<!-- 変更後 -->
<div class="tagline-pill">Simple. Useful. Quiet.</div>
```

**結果:** ブランドコピーはトップバーに1回だけ表示される。

---

### 2. カテゴリ見出しの削除・フラット化

**削除:** `group-label`（DAILY / MEMORY）と `card-group` ラッパーを削除し、4カードを単一の `.cards` グリッドに統合

```html
<!-- 変更前 -->
<section class="card-groups">
  <div class="card-group">
    <p class="group-label">...</p>
    <div class="cards">
      [DarumaKnock]
      [TimeBud]
    </div>
  </div>
  <div class="card-group">
    <p class="group-label">...</p>
    <div class="cards">
      [TravelGuard]
      [Dessin]
    </div>
  </div>
</section>

<!-- 変更後 -->
<section class="card-groups">
  <div class="cards">
    [DarumaKnock]
    [TimeBud]
    [TravelGuard]
    [Dessin]
  </div>
</section>
```

**CSS:** `.cards` の `grid-template-columns: 1fr 1fr` はそのまま維持。4カードが 2×2 で並ぶ。

---

### 3. カード内 CTA の優先順位整理

**Open** を主 CTA として目立たせる。**Support / Privacy / Terms** は補助リンクとして小さく表示する。

**CSS に追加:**

```css
.btn-sub {
  display: inline-flex;
  align-items: center;
  padding: 6px 10px;
  border-radius: 10px;
  font-size: 0.8rem;
  font-weight: 500;
  color: rgba(159,178,204,0.75);
  border: 1px solid rgba(230,238,249,0.08);
  background: transparent;
  text-decoration: none;
  transition: color .15s, border-color .15s;
}
.btn-sub:hover {
  color: rgba(159,178,204,1);
  border-color: rgba(230,238,249,0.18);
  text-decoration: none;
}
```

**各カードのボタン構造（4カード共通）:**

```html
<!-- 変更前: 全部 .btn で均等 -->
<div class="btns">
  <a class="btn" href="...">Open</a>
  <a class="btn" href="...">Support</a>
  <a class="btn" href="...">Privacy</a>
  <a class="btn" href="...">Terms</a>
</div>

<!-- 変更後: Open のみ .btn、残りは .btn-sub -->
<div class="btns">
  <a class="btn" href="..."><span class="lang-ja">開く</span><span class="lang-en">Open</span></a>
  <a class="btn-sub" href="..."><span class="lang-ja">Support</span><span class="lang-en">Support</span></a>
  <a class="btn-sub" href="..."><span class="lang-ja">Privacy</span><span class="lang-en">Privacy</span></a>
  <a class="btn-sub" href="..."><span class="lang-ja">Terms</span><span class="lang-en">Terms</span></a>
</div>
```

リンク先 URL は変更しない。

---

## 変更ファイル

`projects/quiet-tools-web/index.html`（1ファイルのみ）

---

## 変更しないもの

- 全文言（hero 見出し・本文・各アプリコピー）
- リンク先 URL
- CSS の変数・カラー・全体トーン
- レスポンシブ対応（`@media` の内容）
- フッター構造
- JP / EN 切り替え JS

---

## 完了条件チェックリスト

- [ ] ブランドコピーの重複がなくなっている（topbar に1回だけ）
- [ ] hero の kicker が削除されている
- [ ] DAILY / MEMORY のカテゴリ見出しが削除されている
- [ ] 4アプリがフラットな 2×2 グリッドで表示されている
- [ ] Open が主 CTA、Support / Privacy / Terms が補助リンクになっている
- [ ] JP / EN 切り替えが正常に動作している
- [ ] レイアウト崩れがない
- [ ] 既存リンクが壊れていない

---

## 実装手順

1. `feature/qt-structure-v1` ブランチ作成
2. index.html を上記差分に沿って修正
3. ブラウザで JP / EN 切り替えを確認
4. diff 確認 → PR 作成 → マージ
