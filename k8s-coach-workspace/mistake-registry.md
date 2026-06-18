# 踩坑登記簿 (間隔複習用)
<!-- 每次踩到坑就加一筆,定期回來抽考自己 -->

## 格式說明

每筆記錄用下方 block 格式。`下次抽考日` 建議設在 3 天後,複習後再往後推 7 天、14 天。

---

## 範例 (Example, 可刪除)

**日期:** 2026-06-16
**主題:** Pod 排程

**踩的坑:** `kubectl run nginx --image nginx` 後 Pod 一直是 `Pending`

**根因:** 叢集只有 control-plane 節點,但 control-plane 預設有 taint `node-role.kubernetes.io/control-plane:NoSchedule`,所以沒有可用的 worker 可以排程

**正確做法:** 建叢集時要帶至少一個 worker 節點 (例如 `lab-cluster.sh up p0` 帶 2 個 worker),或是手動 `kubectl taint` 移除 control-plane 的 taint

**下次抽考日:** 2026-06-19

---

<!-- 從這裡開始加你自己的踩坑記錄 -->

**日期:** 2026-06-18
**主題:** YAML 欄位拼錯 / 讀 validation error

**踩的坑:** Deployment apply 失敗 `strict decoding error: unknown field "spec.selector.matchLabels"`(把 `matchLabels` 打成 `metaLabels`)

**根因:** k8s 嚴格解碼,遇到不認識的欄位直接退件(防打錯字卻無聲失敗)。錯誤訊息的 `unknown field "A.B.C"` 是藏寶圖,完整路徑直指出錯的層級與欄位。

**正確做法:** 讀 `unknown field "路徑"` → 去檔案找該路徑那層,看欄位名「不是拼錯就是放錯層」。selector 認親的正確欄位是 `matchLabels`,且必須等於 template.metadata.labels。

**下次抽考日:** 2026-06-21
