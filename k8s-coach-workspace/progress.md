# 學習進度卡 (斷點續傳)
<!-- 每次 session 開始前更新這裡,讓 Claude 快速掌握你的狀況,避免重複解釋背景 -->

## 基本資訊

| 欄位 | 內容 |
|------|------|
| 目前 phase | P0 心智模型 |
| 目前主題 | P0 D 段 lab ✅ 親眼看五棒+reconcile;F 段口頭 ✅;**剩 G 段 artifact 未 commit** |
| 上次 session 日期 | 2026-06-18 |
| session 累計次數 (session_count) | 2 |
| 上次 Weekly Review (last_weekly_review) | 0 |

## 診斷結果 (New Student Warm-Up)

程度: 中 (有地圖形狀,缺演員名字)。pacing = P0 剛好,不加速。

- 強: 已有 reconcile 直覺 (原話「比對現有環境進行更新」);知道 rolling update 替換 Pod。
- 洞 1: 用「下指令」框架 = 還停在 imperative 思維 (k8s 是 declarative)。
- 洞 2: 各步驟「誰做的」全省略 (API Server / etcd / controller / scheduler / kubelet 都沒提到)。
- 洞 3: 漏掉 Pod 怎麼被排到某台 node (scheduler 指派 + kubelet 啟動)。

## 未完成 lab

- [x] D 段 kind lab:apply hello-nginx → 用 `kubectl get events --sort-by` 看五棒 → delete pod 看 reconcile 自動補(新尾碼/新 IP)→ scale=0 證明改 DESIRED 才停。全做完。
- [ ] **G 段 artifact 未完成**:k8s-portfolio repo 已 `git init` 在 `~/jason/k8s-portfolio`,manifests/hello-nginx.yaml 已 copy。**待學員把 apply→Running 流程圖畫進 `~/jason/k8s-portfolio/p0-apply-to-running.md` 並 commit**。學員記憶法=對照參考圖重畫,所以 Claude 下次**重新生一份參考圖**(五棒接力 + reconcile loop DESIRED/CURRENT + symptom→棒排查表)讓他對照;別假設舊對話還在(可能已換機器)。portfolio repo 目前只在原機器本地、無 remote、gh 未裝。

## 下一步

> 下次繼續(一句話):接 G 段 —— 確認學員有沒有把 `p0-apply-to-running.md` 畫好+commit(`cd ~/jason/k8s-portfolio && git add -A && git commit -m "..."`)。commit 完 **P0 正式畢業**,直接進 P1(核心物件+容器底層)。
> 環境:kind 叢集 `k8s-coach-p0` 仍在(deployment scaled 0)。學員偏好自己敲指令/自己手打 YAML,Claude 只給規格+審稿,別代跑/代寫(見 memory)。
> commit 規則:user 全域禁止任何 trailer/Co-Authored-By,commit message 一行。
> 待補精準度:術語要用「DESIRED vs CURRENT」「reconcile loop 收斂」而非「監控數量」。etcd Raft 深入 park 到 P5/foundations。

## 補充筆記

- 學員背景: DevOps 工程師,hands-on 有 (kubectl apply / 看 logs),底層理論弱;coding 初學。
- 教法備忘: 多用生活 analogy、用學員原話回扣、一次一個 chunk、語言要白。
- chunk map (P0): [1] declarative+reconcile → [2] API Server+etcd → [3] controller 怎麼 reconcile → [4] scheduler 指派 node → [5] kubelet 啟動容器。全部 ✅。
- session 1 scorecard (P0-P1): 底層原理 ✅ / 內部機制 ✅ / 自己的話 ✅。改進=用詞精準度。
- symptom→棒次地圖已教: Pending=scheduler / ContainerCreating=kubelet 網路volume / ImagePullBackOff=runtime拉image / CrashLoopBackOff=容器或probe。
- session 2 (2026-06-18) D段親手做完: kind 拆解(node=container)、kubeconfig/context 安全(他原本怕打到公司 prod EKS,已教 current-context 肌肉記憶)、Deployment→ReplicaSet→Pod 三層(從 pod 名 hash 看族譜)、reconcile 自癒、scale=0。
- session 2 scorecard (P0-P1): 底層原理 ✅(自己用恆溫器比喻 declarative)/ 內部機制 ✅ / 自己的話 ✅。改進=用詞精準度(同上)。
- 新術語卡已加: kubeconfig / context / kind(抽考日 2026-06-21)。
