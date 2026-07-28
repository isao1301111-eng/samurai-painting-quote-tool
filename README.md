# Samurai Painting Quote Tool
**AI-Powered Painting Estimation with Hallucination Guard Protocol**

> 🛡️ Portfolio Project — Isao Matsumoto | AI Automation Developer（建築塗装27年 × AI）  
> 📍 Sydney, Australia → Japan (Sep 2026)  
> 🔗 [linkedin.com/in/isao-matsumoto-1b271411b](https://linkedin.com/in/isao-matsumoto-1b271411b)

[![Try the Live App (v6)](https://img.shields.io/badge/%F0%9F%9A%80_Try_the_Live_App-v6-C9A84C)](https://isao1301111-eng.github.io/samurai-painting-quote/samurai-painting-quote-v6.html)
[![Application Repo](https://img.shields.io/badge/Application_Repo-samurai--painting--quote-blue)](https://github.com/isao1301111-eng/samurai-painting-quote)

> 📌 これは **LinkedIn 用のポートフォリオ紹介ページ**です。実際に動くアプリ本体（v4 → v6）は [**samurai-painting-quote**](https://github.com/isao1301111-eng/samurai-painting-quote) にあります。
> 📌 This is the **portfolio write-up for LinkedIn.** The working application (v4 → v6) lives in [**samurai-painting-quote**](https://github.com/isao1301111-eng/samurai-painting-quote).

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

このリポジトリには progression（進化の過程）を示すスナップショットとして v4・v5 を同梱しています。**最新の v6 は本体アプリリポジトリ [samurai-painting-quote](https://github.com/isao1301111-eng/samurai-painting-quote) で公開・稼働中**です。

This repo bundles the v4 / v5 snapshots to show the progression. **The latest v6 is published and running in the application repo [samurai-painting-quote](https://github.com/isao1301111-eng/samurai-painting-quote).**

| File / Link | Version | Description |
|------|---------|-------------|
| [▶ Live v6](https://isao1301111-eng.github.io/samurai-painting-quote/samurai-painting-quote-v6.html) | **v6 (Latest)** | + AI free-text input & Saved Quotes/Clients ledger（本体リポで公開）|
| `samurai-painting-quote-v5.html` | v5 | + Hallucination Guard Protocol v1.0 |
| `samurai-painting-quote-v4.html` | v4 | Baseline — material/condition/NSW rate engine |

> v4 / v5 is kept intentionally to show the diff and progression.

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

## 📂 v6 — AI自由記述入力 & 見積もり台帳 / AI Free-Text Input & Quote Ledger

> ▶ **Live demo:** [samurai-painting-quote-v6.html](https://isao1301111-eng.github.io/samurai-painting-quote/samurai-painting-quote-v6.html)（本体リポで公開 / hosted in the application repo）

v6 は v5 の上に **2つ** を追加した最新版です。

**🤖 AI自由記述入力（LLM × Guard）**  
「築20年の木造2階建て、外壁80㎡、ひび割れあり、油性から水性に塗り替え」のように自由文で書くと、AIがフォームに構造化 → その後 **13項目のハルシネーション防止がAI自身の出力を検証**（塗料量・塗料金額・矛盾・NSW相場）してから見積もりへ進みます。これは本ポートフォリオの主張を1つの流れで体現します：*LLMは速いが幻覚する／ルールエンジンは正確だが融通が利かない → 組み合わせて互いの弱点を消す。* 既定は鍵不要の**オフラインのデモ解析**で誰でも動作。自分の Claude API キーを入れると本物の `claude-opus-4-8` 抽出に切替（キーはブラウザ内のみに保存）。

Describe the job in plain English/Japanese and the tool structures it into the form — then a **13-point Hallucination Guard verifies the AI's own output** (paint volume & cost, contradictions, NSW rates) before quoting. Runs on an offline demo parser by default; add your own Claude API key for real `claude-opus-4-8` extraction.

**📂 永続化層（見積もり台帳）/ Persistence layer**  
- 💾 **保存 / Save** — お客様情報・全入力・検証結果ごと見積もりを保存
- 📂 **履歴・顧客管理タブ / History & Clients** — 顧客名／住所／見積番号で検索
- ↩ **復元 / Restore** ・ ⧉ **複製 / Duplicate** — 過去見積もりの再編集・別プラン作成
- 📤📥 **JSON エクスポート／インポート** — 全データのバックアップ・端末間移行
- データはブラウザ内（`localStorage`）に保存 — **サーバー不要・API不要・単一HTML**

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

## 開発の歩み（課題 → 解決）/ Development Story

一度で完成したのではなく、**「AIをどう信用させるか」という一貫した問いに沿って v4 → v5 → v6 と進化**させました。
Not built in one shot — evolved v4 → v5 → v6 around one question: *how do you make an AI estimate trustworthy?*

| バージョン | ぶつかった課題 / Problem | 解決 / Solution |
|---|---|---|
| **v4** | 材質・塗膜状態・NSW相場を手計算していた | 材質別単価×状態補正×市場レンジ照合の計算エンジン化 |
| **v5** | 生成された見積もりを人間が目視で検証するしかなかった | 生成前に走る**9項目の自動検証エンジン**（論理矛盾・入力漏れ・市場乖離を検知しブロック）＝「AIの出力を検証するAI」 |
| **v6** | LLM自由入力は速いが幻覚する／ルールエンジンは正確だが融通が利かない | 両者を組み合わせ、**AI自身の出力を13項目で検証**してから見積もりへ。加えて保存・顧客台帳で実務運用に耐える形へ |

一貫思想は **Hallucination Guard**：*件数を出すなら、全部言える状態で出せ*（検証#8で実装）。詳しい時系列は [CHANGELOG.md](CHANGELOG.md)、設計判断の物語は [CASE_STUDY.md](CASE_STUDY.md) を参照。

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
AI Automation Developer (27 yrs in painting × AI)  
📧 isao1301111@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/isao-matsumoto-1b271411b)

---

## ロードマップ / Roadmap

- [x] Screenshots (STRICT MODE ON/OFF comparison)
- [x] Claude API連携 — 自由記述テキスト → 自動見積もり生成（v6 で実装 / shipped in v6）
- [ ] 音声入力 → 自動見積もり生成 / Voice input
- [ ] Stripe Billing統合 — 見積もり承認後に自動請求
- [ ] Multi-language (English / Japanese / Thai)
