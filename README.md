# Handoff: 片山電業 コーポレートサイト

## Overview
滋賀県大津市坂本に拠点を置く電気工事会社「片山電業」のコーポレートサイト。事業は **送電線の鉄塔組立工事および架線工事**。地域インフラを支える専門性・信頼感と、採用（全国から仲間を募集）・新規取引先募集を訴求することが目的。トップから各セクションへ「ページ切替（SPA的な擬似ルーティング）」で遷移する、編集的（エディトリアル）で高級感のある和モダンデザイン。

## About the Design Files
このバンドルに含まれるファイルは **HTMLで作成されたデザインリファレンス（プロトタイプ）** です。最終的な見た目と挙動を示すものであり、本番コードとしてそのまま流用する前提ではありません。本タスクは、これらのHTMLデザインを **ターゲットのコードベースの既存環境（React / Next.js / Vue / 静的サイトジェネレータ等）で、その流儀・ライブラリ・パターンに沿って再現する** こと。まだ環境がない場合は、コーポレートサイトとして適切なフレームワーク（例: Next.js + 静的書き出し、Astro 等）を選定して実装してください。

> 補足: 元ファイルは社内ツールの「Design Component（`.dc.html`）」形式で、`support.js` ランタイム上で動く軽量テンプレート + ロジッククラスです。**この形式を再現する必要はありません。** マークアップ・スタイル・挙動の仕様として読み取り、ターゲット環境の通常のコンポーネントに翻訳してください。

## Fidelity
**High-fidelity (hifi)**。最終的な配色・タイポグラフィ・余白・アニメーションまで作り込み済み。下記の値どおりにピクセル単位で再現してください。ただし画像はプレースホルダ（ドラッグ&ドロップ枠）を含むため、実写真への差し替えが前提です。

## Site Structure / 擬似ルーティング
ヘッダーナビによる**ページ切替式（フルページリロードなし）**。`state.page` 一つで表示中ページを管理し、該当ページのみ描画。ページ切替時はスクロール最上部へリセットし、フェードイン（`kdPageIn` 0.55s ease）で入場。

ページ（`page` キー）:
- `home` — トップ（ヒーロー + 理念 + 3カード誘導 + CTA帯）
- `service` — 事業内容
- `reason` — 選ばれる理由
- `works` — 施工実績
- `recruit` — 採用情報
- `about` — 会社案内（代表メッセージ + 会社概要）
- `contact` — お問い合わせ（フルブリード写真ヒーロー）

ヘッダーのナビ項目は5つ（事業内容 / 選ばれる理由 / 施工実績 / 採用情報 / 会社案内）+ 右端に「お問い合わせ」ピルボタン。現在ページのナビには銅色のドット（下に5px円, `#b56a37`）を表示。フッターのメニューリンクも各ページへ遷移。

## Design Tokens

### Colors
| 用途 | Hex |
|---|---|
| 背景（ベースのクリーム） | `#f5f3ee` |
| 背景（やや濃いクリーム / セクション） | `#ece7dd` |
| カード明色 | `#fff7ee` |
| 主要テキスト（墨） | `#1f1d1a` |
| ダークセクション背景 | `#1f1d1a` |
| サブテキスト | `#3a352e` / `#5a5349` |
| 微弱ラベル・キャプション | `#a39c8f` / `#8a8378` |
| アクセント銅（コッパー） | `#b56a37` |
| アクセント淡銅（ダーク背景上） | `#e9b787` |
| ヒーロー「空」スカイブルー | `#7ec8f0` |
| 罫線（クリーム上） | `#ddd5c7` / `#d8d0c2` |
| フッター藍グラデ | `#1a2a55` → `#16234a` → `#0e1838` |
| フッター文字 | `#d3d9ea` / `#aab4d2` / `#9aa6c8` |

### 見出しキーワードの特殊装飾（`background-clip:text` でグラデーション）
- 事業内容の見出し「**天空**」: `linear-gradient(110deg,#7ec8f0 0%,#3a7fd0 45%,#0a2a6b 100%)`（青系グラデ）, フォールバック色 `#3a7fd0`
- 施工実績の見出し「**信頼の証**」: 単色 深紅 `#8e1b22`
- 採用情報の見出し「**未来**」: メタリック（ダークスチール）`linear-gradient(120deg,#3a434d 0%,#9aa6b2 26%,#56606b 50%,#aeb9c4 66%,#2e363f 88%,#6b757f 100%)`, フォールバック `#3a434d`
- 採用情報の見出し「**仲間**」: メタリック（ディープゴールド）`linear-gradient(120deg,#6b4a1c 0%,#c79a4b 26%,#8a6620 50%,#e3bd6e 66%,#5c3f15 88%,#a87f33 100%)`, フォールバック `#8a6620`
- 会社案内の見出し「**大動脈**」: 単色 明るい赤 `#e23b3b`
- ヒーロー H1「**空**」: 単色 `#7ec8f0`

`background-clip:text` の実装例:
```css
background: linear-gradient(110deg,#7ec8f0,#3a7fd0 45%,#0a2a6b);
-webkit-background-clip: text;
background-clip: text;
-webkit-text-fill-color: transparent;
color: #3a7fd0; /* フォールバック */
```

### Typography
Google Fonts:
- `Shippori Mincho B1`（明朝, weight 500/600/700/800）— 和文見出し・社名
- `Noto Sans JP`（weight 400/500/700）— 本文
- `Cormorant Garamond`（italic 500/600）— 英字ラベル・番号・装飾

スケール（`clamp()` でレスポンシブ）:
- ヒーロー H1: `clamp(44px,8.4vw,128px)`, line-height 1.12, letter-spacing 0.04em, Shippori 700
- 各ページ導入 H1: `clamp(30px,5vw,60px)`, line-height 1.45, letter-spacing 0.05em, Shippori 700
- セクション H2: `clamp(26px,3.6vw,46px)` ～ `clamp(28px,4vw,52px)`, Shippori 700
- サービス見出し H3: `clamp(21px,2.7vw,36px)`, Shippori 600
- 本文 p: `clamp(15px,1.5vw,18px)`, line-height 2.1–2.25
- 英字ラベル: Cormorant italic, 12–15px, letter-spacing 0.2–0.34em, 色 `#b56a37`
- 番号（01–05）: Cormorant italic, 大きめ（40px等）

### Spacing / Radius / その他
- セクション縦パディング: `clamp(80px,10vw,150px)` 前後。ページ導入は `clamp(118px,13vw,190px)` 上（固定ヘッダー分の余白込み）
- 横パディング: `clamp(20px,5vw,56px)`
- コンテンツ最大幅: `1320px`（中央寄せ）
- カード角丸: 10–12px、画像枠: 6–8px、ピルボタン: 999px
- 金のヘアライン（導入の区切り線）: width 64px, height 1px, `linear-gradient(90deg,transparent,#c79a5b,transparent)`、登場アニメ `kdRuleIn`（scaleX 0→1, 0.8s ease 0.2s）

## Screens / Views

### 1. Header（全ページ共通・固定）
- `position:fixed; top/left/right:0; z-index:50`、`background:rgba(245,243,238,0.9); backdrop-filter:blur(14px)`、下境界 `1px solid rgba(31,29,26,0.08)`
- パディング `15px clamp(20px,5vw,56px)`
- 左: ロゴ。42px円 `#1f1d1a` 内に Cormorant italic の「K」（`#f5f3ee`）。右に社名「片山電業」(Shippori 700, 18px, ls .14em) + 英字「KATAYAMA DENGYO」(Cormorant italic, 11px, ls .22em, `#8a8378`)。クリックで `home` へ
- 右（デスクトップ ≥881px）: ナビ5項目（和文13px + 英字ラベル Cormorant 10px）。現在地は下に銅ドット。続けて「お問い合わせ」ピル（`#1f1d1a` 背景, `#f5f3ee` 文字, 銅ドット付き）
- モバイル（≤880px）: 右に「MENU」ボタン → 全画面メニュー（`#1f1d1a`）。各項目は Shippori 23px + 英字ラベル。下部に銅色（`#b56a37`）の電話ブロック。閉じる×ボタン

### 2. Home
- **ヒーロー**: `min-height:100vh`、下寄せ。背景は鉄塔写真（`images/hero-tower.png`, object-fit cover）。Ken Burns ズーム（`kdKenBurns` 26s alternate）。上に複数の光演出レイヤー（後述アニメ）。暗色グラデ `linear-gradient(180deg, rgba(18,17,14,.42) 0%, rgba(18,17,14,.1) 36%, rgba(18,17,14,.8) 100%)`。
  - 英字キャッチ「Power Transmission · Steel Towers」(Cormorant italic, 罫線付き)
  - H1「<span 空(#7ec8f0)>を、つなぐ。」(clamp(44px,8.4vw,128px))
  - リード文（白 92%）2行
  - CTA: 「お問い合わせ」ピル（クリーム背景）+ 電話ピル（枠線, `077-575-1237`）
  - 右下に縦書き「SCROLL」インジケータ
- **理念ティーザー**: 2カラム grid。左に英字「Philosophy / 私たちの仕事」+ H2「高い空の上で、電気の<span 銅>道</span>をつなぐ。」、右に本文2段落
- **3カード誘導**: grid（minmax 260px）。
  - 事業内容カード: 背景 `#1f1d1a` / 文字クリーム / 英字「01 — SERVICE」淡銅
  - 施工実績カード: 背景 `#ece7dd` / 墨字 / 英字「02 — WORKS」銅
  - 採用情報カード: 背景 `#b56a37` / `#fff7ee` 文字 / 英字「03 — RECRUIT」
  - 各カード末尾に「View →」。クリックで該当ページへ
- **CTA帯**: `#1f1d1a` 背景, 中央寄せ。英字「Contact」+ H2「まずは、お気軽に<span 淡銅>ご相談を。</span>」+ 電話ピル（淡銅 `#e9b787` 背景）

### 3. Service（事業内容）
- 導入: 英字「SERVICE」+ H1「<span 青グラデ>天空</span>の現場を支える、専門の技術。」+ 金ヘアライン + リード文
- ダーク帯（`#1f1d1a`）に4項目を罫線区切りのリスト（grid: 番号 / 本文 / 矢印）。各行クリックで `contact` へ
  1. 鉄塔組立工事
  2. 架線工事
  3. 保守・点検・改修
  4. 高所作業・安全管理
  - 番号は Cormorant italic（`#7a746a`）、見出し Shippori 600（clamp 21–36px）、本文 14.5px（白66%）、矢印 淡銅

### 4. Reason（選ばれる理由）
- 導入: 英字「PROMISE」+ H1「確かさで、選ばれ続ける。」+ 金ヘアライン + リード
- 3カラム（minmax 260px）。各カードは上に2px墨ボーダー、番号 Cormorant 40px 銅 + 英字ラベル、H3、本文
  1. 安全第一の施工体制（SAFETY）
  2. 専門技術と有資格者（SKILL）
  3. 地域に根ざした対応力（TRUST）

### 5. Works（施工実績）
- 導入: 英字「WORKS」+ H1「ひとつの現場が、<span 深紅 #8e1b22>信頼の証。</span>」+ 金ヘアライン + リード
- `#ece7dd` 帯に3カラムの画像カード（プレースホルダ枠 `image-slot`, 角丸6px, 高さ clamp(240px,30vw,340px)）。下に和文タイトル + 英字（TOWER / WIRING / MAINTENANCE）
  - 実装時は通常の `<img>` + 説明テキストに置換。画像は後日支給

### 6. Recruit（採用情報）
- 導入: 英字「RECRUIT」+ H1「空の上で、<span メタリック銀>未来</span>を<span メタリック金>仲間</span>へ。」
  - ※元コピーは「未来をつなぐ仲間へ。」。"未来"=ダークスチールメタリック, "仲間"=ディープゴールドメタリック
- 銅色帯（`#b56a37`, `#fff7ee` 文字）に2カード（`#fff7ee` 背景）
  - 「一緒に働く仲間」（STAFF）: 本文 + タグピル（未経験歓迎 / 経験者優遇 / 全国募集）
  - 「新規お取引先」（PARTNER）: 本文 + タグピル（協力会社 / 資材・取引）
  - 下に電話CTA（`#1f1d1a` ピル）
- 採用の背景ストーリー（会社案内の代表メッセージと連動）: 代表は16歳で送電線工事の世界へ、13年の下積みを経て29歳（令和3年/2021）で独立。現在5名の小規模だが事業拡大に向け全国から仲間と新規取引先を募集中

### 7. About（会社案内）
- 導入: 英字「COMPANY」+ H1「電気の<span 赤 #e23b3b>大動脈</span>を、足元から。」+ 金ヘアライン + リード
- **代表メッセージ**: `#ece7dd` 帯。2カラム。左に代表写真枠（角丸8px, 高さ clamp(360px,42vw,520px)）+ 左下に墨色の名札（「Representative / 代表　片山 恭太」）。右に英字「Message / 代表メッセージ」+ H2「一基の鉄塔に、<span 銅>13年分</span>の誇りを。」+ 本文2段落 + 署名
- **会社概要テーブル**: 2カラム。左に見出し「会社概要」+ 説明 + お問い合わせピル。右に定義リスト（左ラベル120px幅, 罫線区切り）
  | 項目 | 値 |
  |---|---|
  | 会社名 | 片山電業 |
  | 代表者 | 片山 恭太（34歳） |
  | 設立 | 令和3年 |
  | 事業内容 | 送電線の鉄塔組立工事及び架線工事 |
  | 所在地 | 〒520-0113 滋賀県大津市坂本六丁目22-19 |
  | 対応エリア | 関西一円（全国対応） |
  | 電話番号 | 077-575-1237 |

  ※郵便番号 520-0113 は坂本エリアの代表値で仮置き。要確認。

### 8. Contact（お問い合わせ）
- フルブリード写真ヒーロー（`min-height:92vh`）。背景 `images/footer-tower.jpg`（cover, scale1.06, brightness .92 saturate 1.12）。
- 上に水色〜青のグラデオーバーレイ（`linear-gradient(180deg, rgba(120,190,235,.32), rgba(90,165,220,.14) 40%, rgba(40,90,150,.5))` + 放射状ハイライト）。
- 中央寄せ: 英字「Contact」+ H1「まずは、<span #eaf6ff>お気軽にご相談を。</span>」（白, テキストシャドウ）+ リード + 白い電話ピル（文字 `#1a4e86`）+ 受付時間/住所

### 9. Footer（全ページ共通）
- 藍色グラデ背景 `linear-gradient(180deg,#1a2a55,#16234a 50%,#0e1838)` + 放射状ハイライト
- 4カラム: ロゴ&説明 / MENU（各ページリンク）/ CONTACT（電話・受付）/ OFFICE（住所・代表・設立）
- 下段: 「© 2026 KATAYAMA DENGYO」「Power Transmission · Otsu, Shiga」

## Interactions & Behavior

### ページ遷移
- ナビ/カード/フッターリンクのクリックで `state.page` を更新 → 該当ページのみ描画
- 遷移時: `window.scrollTo(top:0)` + フェードイン `kdPageIn`（opacity 0→1, translateY 16px→0, 0.55s ease）
- 現在ページのナビに銅ドット表示

### ホバー / プレス（全ボタン・リンク・カードに付与）
JSで `a, button, [data-card]` に付与（ピル= border-radius≥40px, grid行, `[data-card]` を対象）:
- **hover**: `translateY(-4〜-6px) scale(1.015〜1.035)` + 影 `0 16px 34px rgba(0,0,0,.2)`、transition .2s ease
- **press(pointerdown)**: `translateY(1px) scale(.96〜.99)` + 影弱め、transition .08s
- **離す/外す**: `transform:none`、戻り transition `.34s cubic-bezier(.34,1.56,.5,1)`（軽いバウンド）

### ヒーローの光アニメーション（`prefers-reduced-motion` で無効化）
- `kdKenBurns`（26s alternate）: 背景画像 scale 1.04→1.14 + 微小トランスレート
- `kdGlow`（7s）: 右下の暖色グロー（径 60vw, screen 合成）が opacity/scale で脈動
- `kdFlicker`（5.5s）: 暖色ウォッシュの明滅
- `kdRise`（11–17s, 複数ディレイ）: 火の粉状の光点が下から上へ上昇（screenっぽい発光 + box-shadow）
- `kdBeacon`（3.2s）: 鉄塔頂部付近の赤い航空灯が点滅
- `kdRuleIn`（0.8s ease 0.2s）: 各ページ導入の金ヘアラインが scaleX で登場

### レスポンシブ
- ナビ: ≤880px でハンバーガー（全画面メニュー）に切替（`matchMedia('(max-width: 880px)')`）
- 主要グリッドは `repeat(auto-fit, minmax(...))` で段組が自動で縦積みに
- フォントは `clamp()` で可変

## State Management
- `page`: 'home' | 'service' | 'reason' | 'works' | 'recruit' | 'about' | 'contact'（表示ページ）
- `isMobile`: boolean（`matchMedia` 監視）
- `menuOpen`: boolean（モバイルメニュー開閉）
- データ取得なし（静的サイト）。お問い合わせは電話リンク（`tel:077-575-1237`）のみ。フォーム化する場合は別途実装が必要

## Assets
`images/` に同梱:
- `hero-tower.png` — ヒーロー背景（鉄塔）
- `footer-tower.jpg` — お問い合わせページ背景（鉄塔・夕景）
- `hero-photo.jpg` — 予備のヒーロー写真候補
- 施工実績3枠・代表写真枠は **プレースホルダ**（実写真は後日支給前提）

アイコン: 装飾はテキスト矢印「→」と CSS 円のみ。アイコンフォント/SVGライブラリ不使用。

フォント: 上記 Google Fonts 3種を `<link>` 読み込み。

## Files
- `片山電業.dc.html` — 全ページを含むデザイン本体（テンプレート + ロジック）。マークアップ/スタイル/挙動の一次ソース
- `image-slot.js` — プレースホルダ画像枠のランタイム（参考用。実装では通常の `<img>` でよい）
- `support.js` — `.dc.html` のランタイム（参考用。再現不要）
- `images/` — 写真アセット

## 実装時の注意（要確認事項）
- 郵便番号 520-0113 は仮。正式値を確認
- 代表表記ゆれ: 初期データは「片山京太」、最新は「片山 恭太（34歳）」。**恭太** が最新指定
- 設立「令和3年」=2021年
- 施工実績・代表写真は実写真への差し替えが前提
- お問い合わせは現状 電話のみ。メールフォーム/問い合わせフォームが必要なら追加実装
