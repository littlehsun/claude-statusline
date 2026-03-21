# Claude Code Enhanced Statusline ⚡

專為 **Claude Code** 設計的增強狀態列，顯示模型名稱、資料夾、Git 狀態、Context 使用率，以及 Pro / Max 方案的速率限制。

## ✨ 特色 (Features)

* **🌈 雙行視覺化狀態列**：第一行顯示模型、Git 分支與狀態、Context 使用率；第二行顯示 5h / 7d Rate Limit 的 progress bar 與倒數時間
* **🌿 Git 狀態一覽**：顯示 staged（+）、modified（!）、untracked（?）、ahead（↑）、behind（↓）
* **⏱ 倒數 + 絕對時間**：5H reset 同時顯示倒數（如 `2h15m`）與絕對時間（如 `19:00`）
* **⑂ Worktree 支援**：使用 worktree 時自動顯示名稱
* **🎨 RGB 全彩**：使用 truecolor ANSI 色碼，依使用率動態變色（綠 → 橙 → 黃 → 紅）
* **🐧 雙平台支援**：自動相容 macOS 與 Ubuntu/Linux

## 🖼️ 狀態列預覽

```
Sonnet │ my-project  main !1 ↑2 │ ✍ 45%
5H ●●●●○○○○○○ 38% ⟳ 2h15m (19:00)    7D ●●●●●●●○○○ 72% ⟳ 03/30 08:00
```

## 🚀 安裝 (Quick Start)

**必備工具：** `jq`（腳本會自動安裝）

```bash
chmod +x setup_claude_status.sh
./setup_claude_status.sh
```

安裝時會詢問進度條樣式：

| 選項 | 樣式 | 預覽 |
|------|------|------|
| 1（預設）| 方格 | `▰▰▰▱▱▱▱▱▱▱` |
| 2 | 圓點 | `●●●○○○○○○○` |
| 3 | 半格精度 | `███▌░░░░░░` |

安裝完成後，進入 Claude Code 執行：

```bash
/statusline ~/.claude/statusline-command.sh
```

發送任何訊息後狀態列即會亮起。

> 若使用自訂 `CLAUDE_CONFIG_DIR`，請將路徑替換為對應目錄下的 `statusline-command.sh`。

## 📁 檔案說明 (Files)

| 檔案 | 說明 |
|------|------|
| `statusline-command.sh` | 主腳本：顯示模型、Git 狀態、Context、Rate Limit |
| `setup_claude_status.sh` | 安裝腳本：自動檢查 `jq`、複製腳本至 Claude config 目錄 |

## 🙏 致謝 (Credits)

視覺設計參考了 [kamranahmedse/claude-statusline](https://github.com/kamranahmedse/claude-statusline)，包含 RGB 色彩配置、`●○` progress bar 樣式，以及雙行佈局的設計概念。
