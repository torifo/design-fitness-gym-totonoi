# 蒼 — AOI WELLNESS HOUSE — fitness-gym/totonoi Spec

**Status:** Approved
**Author:** torifo
**Created:** 2026-05-24
**Updated:** 2026-05-24

---

## 1. Overview

### Problem Statement
都市部のフィットネスジムは「鍛える・痩せる・結果を出す」の煽り CTA と赤・黒・ネオン系の高揚色で構成されがちで、ストレスを抱えたデスクワーカーが本来求めている「整える時間」とトーンが合わない。サウナ・水風呂・ピラティスを軸にしたリカバリー文化を、煽らずに、retreat の静けさで提示するジムサイトの例が乏しい。

### Goal
架空のウェルネスハウス「蒼（AOI WELLNESS HOUSE）」を、サウナ × 水風呂 × 外気浴 × ピラティス × 瞑想 を主軸とした「整えるジム」として実装する。on の宿系・Aman Spa のような retreat 表現と、日本のサウナ「ととのう」文化を接続し、墨・苔・木・障子のソフトパレットと余白多めの静寂感のあるサイトを構築する。

### Non-Goals
- 「3ヶ月で −10kg」のような結果主義の煽り CTA
- 重量・回数・BPM など、激しい筋トレ表現
- 鮮やかな赤・蛍光色・ネオン系の高揚配色
- カート・オンライン物販・決済機能
- BeforeAfter 写真によるダイエット訴求

---

## 2. User Stories

| ID | Persona | Want to | So that |
|----|---------|---------|---------|
| US-01 | 35歳デスクワーカー（男性） | サウナ・水風呂・外気浴の動線を事前に知りたい | 仕事帰りに迷わず整えに行ける |
| US-02 | 40代マネージャー（女性） | ピラティスと瞑想のクラス時間を見たい | 月曜の朝に予定を組める |
| US-03 | 50代経営者 | 静かな個室サウナや会員制プランを知りたい | 人の少ない時間にこもれる |
| US-04 | 出張中の30代ビジネスパーソン | 単発利用（ドロップイン）の料金と持ち物を知りたい | 当日ふらりと立ち寄れる |

---

## 3. Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | ヒーローは木目・石・湯気のソフトな静止画＋縦組み明朝の店名 | P0 |
| FR-02 | 施設紹介：サウナ室／水風呂／外気浴ととのいスペース／ピラティススタジオ／瞑想室 の5区画 | P0 |
| FR-03 | 「ととのうフロー」を 入浴 → サウナ → 水風呂 → 外気浴 → 休 の5ステップで図示 | P0 |
| FR-04 | 週間クラス表（ピラティス／ヨガ／瞑想／呼吸法／軽い有酸素） | P0 |
| FR-05 | 料金プラン：ドロップイン／月会員／個室会員 の3段（煽りなしのトーン） | P0 |
| FR-06 | 「整える」哲学を語る短文セクション（明朝、行間広め、余白多め） | P1 |
| FR-07 | スタッフ・整体師紹介（2〜3名、肩書きは「整え手」「呼吸案内人」など） | P1 |
| FR-08 | アクセス・営業時間・持ち物リスト | P0 |
| FR-09 | スクロール時に湯気のような微細フェードイン演出（控えめ） | P1 |
| FR-10 | 840px 以下で 1 カラム化、画像は天地を圧縮しない | P0 |

---

## 4. Key Design Decisions

| Decision | Chosen | Rationale | Rejected |
|----------|--------|-----------|----------|
| 配色 | 墨 × 苔 × 木 × 生成り（off-white） | retreat の自然素材感を出すソフトパレット | 黒×赤×ネオン（鍛えるジム表現） |
| 主見出し書体 | Shippori Mincho B1（縦組み可） | 和の静けさと余白に明朝の細い縦画が効く | 太いゴシック（力みすぎる） |
| 本文書体 | Noto Sans JP Light + Inter Light | 細字で「静寂」を担保 | Bold 多用 |
| 写真トーン | 低彩度・低コントラスト・湯気の白み | Aman Spa 的な瞑想的閲覧 | 高彩度のジム広告写真 |
| 装飾 | 罫線一本 + 大きな余白 + 縦組み | 障子・床の間の見立て | グラデ・シャドウ・派手なボタン |
| CTA トーン | 「ご予約」「見学のご案内」 | 静かな招きの言葉 | 「今すぐ申し込む」「無料体験！」 |
| ヒーロー演出 | 湯気の slow fade in（4s） | 「ととのう」までの間の表現 | カルーセル・自動再生動画 |
| ナビ | 上部にロゴ、リンクは縦の細罫で区切る | 余白の支配を崩さない | メガメニュー |

---

## 5. Design System

```css
:root {
  /* Palette — 墨・苔・木・障子 */
  --sumi:    #1c1a17;   /* 墨（本文・見出し） */
  --kinari:  #f1ece2;   /* 生成り（背景） */
  --shoji:   #e8e2d3;   /* 障子（セクション背景） */
  --koke:    #5a6b4a;   /* 苔（アクセント） */
  --mokume:  #8c6a4a;   /* 木目（補助） */
  --ishi:    #b7b1a4;   /* 石（罫線・補助テキスト） */
  --yuge:    #ffffff;   /* 湯気（白み） */

  /* Typography */
  --font-mincho: 'Shippori Mincho B1', 'Hiragino Mincho ProN', serif;
  --font-sans:   'Noto Sans JP', 'Inter', system-ui, sans-serif;
  --font-kana:   'Klee One', 'Shippori Mincho B1', serif;

  /* Rhythm */
  --space-xl: clamp(4rem, 8vw, 8rem);
  --space-lg: clamp(2.5rem, 5vw, 5rem);
  --space-md: 1.5rem;
  --leading-body: 2.1;       /* 行間広め（静寂） */
  --tracking-mincho: 0.08em; /* 明朝の縦画を活かす字間 */

  /* Lines */
  --rule: 1px solid var(--ishi);
}

/* 見出しは細く・大きく・字間広め */
h1, h2 {
  font-family: var(--font-mincho);
  font-weight: 300;
  letter-spacing: var(--tracking-mincho);
}
```

---

## 6. References

### 参照サイト
- [Aman Spa](https://www.aman.com/spa) — retreat の静寂表現、余白支配、自然素材の写真扱い
- [zen place pilates](https://zenplace.co.jp/) — 「整える」「自律神経」の語り口、白＋淡木色の配色
- [SaunaLab](https://saunalab.jp/) — サウナ文化サイトのロゴ・トーン参考

### Fonts
- [Shippori Mincho B1](https://fonts.google.com/specimen/Shippori+Mincho+B1) — 主見出し（明朝、縦組み対応）
- [Klee One](https://fonts.google.com/specimen/Klee+One) — 引用・キャプション（手書き風楷書）
- [Noto Sans JP](https://fonts.google.com/noto/specimen/Noto+Sans+JP) — 本文
- [Inter](https://fonts.google.com/specimen/Inter) — ラテン併記

### 同シリーズ参照
- [fitness-gym 親 README](../README.md)
- [seasidebookshop/fuyunagi spec](../../seasidebookshop/fuyunagi/spec.md) — 和の静の表現
- [stationery/mono spec](../../stationery/mono/spec.md) — 余白と最小装飾の系譜
