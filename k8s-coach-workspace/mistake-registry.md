# 踩坑登記簿 (間隔複習用)
<!-- 每次踩到坑就加一筆,定期回來抽考自己 -->

## 格式說明

每筆記錄用下方 block 格式。`下次抽考日` 建議設在 3 天後,複習後再往後推 7 天、14 天。

---

## 範例 (Example — 可刪除)

**日期:** 2026-06-16
**主題:** Pod 排程

**踩的坑:** `kubectl run nginx --image nginx` 後 Pod 一直是 `Pending`

**根因:** 叢集只有 control-plane 節點,但 control-plane 預設有 taint `node-role.kubernetes.io/control-plane:NoSchedule`,所以沒有可用的 worker 可以排程

**正確做法:** 建叢集時要帶至少一個 worker 節點 (例如 `lab-cluster.sh up p0` 帶 2 個 worker),或是手動 `kubectl taint` 移除 control-plane 的 taint

**下次抽考日:** 2026-06-19

---

<!-- 從這裡開始加你自己的踩坑記錄 -->
