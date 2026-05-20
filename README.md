# Samurai Painting Quote Tool
**AI-Powered Painting Estimation with Hallucination Guard Protocol**

> 🛡️ Portfolio Project — Isao Matsumoto | AI Consultant & Automation Specialist  
> 📍 Sydney, Australia → Japan (Oct 2026)  
> 🔗 [linkedin.com/in/isao-matsumoto-1b271411b](https://linkedin.com/in/isao-matsumoto-1b271411b)

---

## スクリーンショット / Screenshots

### 入力フォーム / Input Form
![Quote Form](<スクリーンショット 2026-05-20 215029.png>)

### 検証プロトコル（エラー検出）/ Verification Protocol (Errors Detected)
![Verification Protocol](<スクリーンショット 2026-05-20 215230.png>)

### AI検証レポート（通過）/ AI Verification Report (Passed)
![AI Verification Report](<スクリーンショット 2026-05-20 215354.png>)

---

## 概要 / Overview

シドニーの塗装業向けに開発した、AI検証プロトコル搭載の見積もり自動化ツール。
材質・塗膜状態・NSW市場単価・論理矛盾を自動検証し、ハルシネーション（誤情報）を防ぐ仕組みを組み込んだポートフォリオ作品。

An AI-powered painting quote automation tool built for Sydney's painting industry.
Features automatic validation of materials, paint conditions, NSW market rates, and logical contradictions — embedding a Hallucination Guard Protocol to prevent AI-generated errors.

---

## ファイル構成 / Files

| File | Version | Description |
|------|---------|-------------|
| `samurai-painting-quote-v5.html` | **v5 (Latest)** | + Hallucination Guard Protocol v1.0 |
| `samurai-painting-quote-v4.html` | v4 | Baseline — material/condition/NSW rate engine |

> v4 is kept intentionally to show the diff and progression.

---

## 🆕 v5 — Hallucination Guard Protocol v1.0

### コンセプト / Concept

> **「AIの出力を検証するAI」**  
> *"An AI that verifies AI output"*

v4までは人間が目視で見積もりをチェックする必要があった。
v5では、生成ボタンを押す前に**9項目の自動検証エンジン**が動作し、
論理矛盾・入力漏れ・市場乖離を検知してブロックする。

Before v5, a human had to manually verify the quote output.
In v5, a **9-item automatic verification engine** runs before the quote is generated,
detecting logical contradictions, missing inputs, and market-rate deviations.

### UI変更 / UI Changes

- **🛡️ STRICT MODE トグル** — ヘッダー右上に配置（グリーンアクセント `#00e676`）
- **Verification Panel** — 生成前に検証結果をリアルタイム表示
- **AI Verification Report** — 厳密モードON時、見積書末尾に自動付加

### 9つの検証項目 / 9 Verification Checks

| # | Check | EN | JA |
|---|-------|----|----|
| 1 | **Active Items** | At least 1 surface or item must be enabled | 有効な表面・項目が1件以上あること |
| 2 | **Surface Area** | All enabled surfaces must have area > 0 | 有効な全表面に面積が入力済みであること |
| 3 | **Item Quantity** | All enabled items must have qty > 0 | 有効な全項目に数量が入力済みであること |
| 4 | **Client Info** | Client name and address provided | お客様名・住所が入力済みであること |
| 5 | **Job Type** | At least 1 job type selected | 作業内容が1件以上選択済みであること |
| 6 | **Logic Contradiction** | Material × condition contradiction detection (e.g. New Build + Peeling) | 材質×塗膜状態の論理矛盾検出（例：新築×剥離あり） |
| 7 | **NSW Market Rate** | Blended rate per m² vs NSW market range per surface type | 表面別NSW市場単価（$/m²）との照合 |
| 8 | **Count Consistency** | Line item count verified by enumeration (件数＝列挙一致) | 明細件数を列挙で検証・件数と一致確認 |
| 9 | **Total Sanity** | Grand total > $0 and above minimum threshold | 合計額が$0超・最低閾値以上であること |

> **Check #8** directly implements the Hallucination Guard core principle:  
> *"件数を出すなら、全部言える状態で出せ"*  
> *(If you state a count, be in a state where you can enumerate all of them)*

### エラー時の動作 / On Error

- `fail` (赤) → 見積もり生成ブロック / Quote generation blocked
- `warn` (黄) → 警告表示・生成は可能 / Warning shown, generation allowed
- `pass` (緑) → 検証通過 / Verification passed

---

## 機能一覧 / Features (v4 + v5)

- **材質別単価エンジン** — Timber / Masonry / Fiber Cement / Render / Metal / Texture Coat / Weatherboard
- **塗膜状態補正** — New / Good / Fair / Poor / Peeling / Water Damage (労務係数±調整)
- **NSW市場レンジ照合** — 表面別に設定された市場単価レンジで自動チェック
- **論理矛盾検出** — 新築×剥離あり等の入力ミスを自動ブロック
- **雨樋対応** — Timber / Colorbond / uPVC 材質別
- **Extras** — 足場・高圧洗浄・カラーコンサル・5年保証・現場清掃・プライマー・防カビ
- **日英切替** — 🇦🇺 EN / 🇯🇵 JP リアルタイム切替
- **PDF出力** — ブラウザ印刷対応（A4最適化）
- **GST計算** — 自動計算・見積書に反映

---

## 技術スタック / Tech Stack

- **Vanilla HTML / CSS / JavaScript** — フレームワーク不使用
- **No backend / No API key required** — 完全クライアントサイド動作
- **Print CSS** — A4 PDF出力最適化
- **Google Fonts** — Bebas Neue / Shippori Mincho / Inter

---

## ポートフォリオとしての位置づけ / Portfolio Context

このツールは以下を実証するポートフォリオ作品です:

1. **建築×AI の融合** — 27年の塗装現場経験（NSW市場相場・材質特性・施工工程の実務知識）をAIロジックに落とし込んだ
2. **Hallucination Guard の実装** — AIが生成した見積もりを別のロジックが二重検証する「AIのAIチェック」アーキテクチャ
3. **実業務への直接適用** — 架空のデモではなく、実際のSamurai Painting Servicesで使用中のツール
4. **段階的改善** — v4→v5の差分で、ソフトウェアを継続的に改善する能力を可視化

This tool demonstrates:
- **Domain expertise × AI**: 27 years of hands-on painting experience encoded as AI logic
- **AI-verifying-AI architecture**: A Hallucination Guard that validates quote outputs before delivery
- **Real-world deployment**: Used in actual business operations, not a demo
- **Iterative improvement**: v4→v5 diff shows the ability to systematically upgrade software

---

## 使い方 / How to Use

1. `samurai-painting-quote-v5.html` をブラウザで開く / Open in browser
2. 顧客情報・作業内容・表面を入力 / Enter client info, job type, surfaces
3. 🛡️ STRICT MODE をONにする（推奨）/ Enable STRICT MODE (recommended)
4. **GENERATE QUOTE** をクリック / Click GENERATE QUOTE
5. エラーがあればパネルに表示→修正 / Fix any verification errors shown
6. PDF印刷 or 保存 / Print or save as PDF

---

## 作者 / Author

**松本 勲 / Isao Matsumoto**  
AI Consultant & Automation Specialist (ex-Painting Contractor, 27 years)  
📧 isao1301111@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/isao-matsumoto-1b271411b)

---

## ロードマップ / Roadmap

- [x] Screenshots (STRICT MODE ON/OFF comparison)
- [ ] Claude API連携 — 音声入力→自動見積もり生成
- [ ] Stripe Billing統合 — 見積もり承認後に自動請求
- [ ] Multi-language (English / Japanese / Thai)
