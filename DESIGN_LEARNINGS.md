# Design Learnings — 蒼 AOI WELLNESS HOUSE

「鍛えるジム」の語彙を一切持ち込まずに、フィットネス領域のサイトを成立させる挑戦だった。

## 学び 1：CTA の温度を下げると、構造ごと変わる

「今すぐ」「無料体験」を消した瞬間、ヒーローの h1 に動詞の現在形すら置けなくなる。「整える時間を。」という体言止めまで弱めて、ようやくトーンが揃った。CTA を「ご予約」「見学のご案内」に限定すると、料金カードのボタン色も赤や黄が浮き、苔（#5a6b4a）一色に落ち着いた。**CTA の語感を決めると、配色・タイポ・余白の幅が芋づる式に決まる**ことを実感した。

## 学び 2：縦組みは Safari の `text-orientation` で破綻する

`writing-mode: vertical-rl` 単独だと数字や英字が横向きになり、`text-orientation: mixed` を必須にした。ただしモバイルでは縦組みの高さがビューポートを食うため、`@media (max-width:840px)` で `writing-mode: horizontal-tb` に戻し、字間も `.45em → .2em` に縮めた。**「縦組みはモバイルで横組みに切り替える」前提で設計**するのが現実的。

## 学び 3：湯気フェードインは `mix-blend-mode: screen` で初めて湯気になる

radial-gradient だけで透明感を作ろうとすると「白い円」にしか見えず、`mix-blend-mode: screen` を当てて初めて背景写真と湯気が滲んだ。`prefers-reduced-motion` 時はアニメを無効化しつつ `opacity: .7` で静止状態で湯気を残す処理にして、動かない人にも「湯気のある場所」を伝えた。

## 学び 4：Klee One は危険物

引用と figcaption だけに限定した。本文に混ぜると一気にカジュアル化し、retreat の寡黙さが崩れる。**手書き楷書は「ここぞ」で 1〜2 箇所**が限度。

## 学び 5：日本語の折り返しは「禁則処理」だけでは足りない

`line-break: strict` や `word-break: auto-phrase` を入れていても、PC 幅のカードや縦組みでは、文字間隔・コンテナ高・`text-wrap: balance` の影響で「ととの / う」「外気浴ととの / いスペース」のような不自然な分断が起きた。ヒーローの縦組み「ととのう」は `max-height:min(72vh,620px)` で縦方向の余白を確保し、`.kanji` に `white-space:nowrap` / `word-break:keep-all` / `overflow-wrap:normal` を指定して語中分断を防いだ。

施設カードの「外気浴ととのいスペース」は、全体を nowrap にするとカード幅を圧迫するため、`外気浴` と `<span class="nowrap">ととのいスペース</span>` に分けた。**日本語UIでは、文全体ではなく「意味の最小単位」を nowrap 化する**ほうが、PC・iPad・スマホの各幅で自然に見える。
