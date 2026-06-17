# k8s-coach skill 迭代 todo

## 背景

用 skill-creator 對 k8s-coach 跑行為評測(coaching 品質,非只測觸發)。
4 題 × 2 組(with-skill vs baseline)。baseline = 帶 user 全域費曼設定但無 k8s-coach skill,隔離 skill 真實邊際價值。

## iteration-1 結果(2026-06-17)

| | with-skill | baseline | Δ |
|---|---|---|---|
| Pass rate | 95% (19/20) | 60% (12/20) | +0.35 |
| Tokens/turn | 46.9k | 31.0k | +51% |

價值分布不均,集中在兩題:

| Eval | Δ | 結論 |
|------|---|------|
| 4 resume | +0.6 | 最乾淨勝點。progress.md 狀態機讓精準續傳 + 到期術語卡抽考,baseline 無狀態做不到 |
| 2 crashloop | +0.6 | skill 強制 Socratic(反問第一個指令),baseline 直接倒清單 |
| 3 ClusterIP | +0.2 | skill 做前置檢查(真本事)但只生 1 張術語卡(規格 3-5);baseline 把主題教得更完整 |
| 1 new-student | 0.0 | 兩邊皆 100%,assertion 無區辨力 |

## 已拍板決定

1. **路由摩擦 → 加一條快速切入支線**:progress.md 空白時,新學員帶具體問題(急性故障 / 指定主題)進場,應先直接處理當下需求(帶 Socratic 教法),再順勢用這個真實問題當 warm-up 診斷,而非一律先丟 8-phase 地圖 + 診斷。

## 待辦(deferred,使用者說先不改,回來再做)

- [ ] 實作 routing 快速切入支線(改 SKILL.md Routing / New Student Warm-Up 段)
- [ ] 重寫 eval-1 assertion,收緊到只測 skill 獨有行為(portfolio per-phase、A-G、chaos drill、生產情境 vs 概念診斷)
- [ ] eval-3 術語卡 assertion 改條件式(僅進 C 段正式教學才要求 3-5 張)
- [ ] iteration-2:重跑 4 題 + 產 review viewer 比對

## 產出位置

- 測試集 + fixtures(in repo):`evals/evals.json`、`evals/files/progress-new.md`、`evals/files/progress-resume.md`
- 評測 workspace(repo 外):`/home/ec2-user/jason/k8s-coach-evals/iteration-1/`
  - `benchmark.json` / `benchmark.md`(量化 + 6 條分析師觀察)
  - `review.html`(自帶資料的 standalone viewer)
  - `eval-*/<config>/outputs/response.md`(8 份完整輸出)+ `grading.json`(逐題評分依據)

## Review

- skill 核心價值已被量化證實:狀態機續傳(eval-4)+ Socratic 強制(eval-2)是 baseline 結構上做不到的。
- 最大隱憂是 routing 對「帶著急事進場」的學員造成摩擦,已決定加快速切入支線解決。
- 評測機制本身可複用:fixtures + assertions + aggregate + viewer 都到位,iteration-2 直接沿用。
