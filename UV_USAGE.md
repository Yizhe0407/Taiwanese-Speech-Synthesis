# UV 使用說明

這個專案使用 [uv](https://github.com/astral-sh/uv) 作為 Python 套件管理工具。

## 快速開始

### 安裝依賴

```bash
uv sync
```

這會：

- 讀取 `pyproject.toml` 中的依賴
- 建立虛擬環境在 `.venv/`
- 安裝所有依賴
- 生成/更新 `uv.lock` 鎖定檔

### 執行 Python 腳本

```bash
# 使用 uv run 會自動使用虛擬環境
uv run python gen_tts.py sentences.txt --tts_weights ./pretrained_models/tacotron2.pyt --voc_weights ./pretrained_models/wavernn.pyt --save_dir ./results

# 或者先啟動虛擬環境
source .venv/bin/activate
python gen_tts.py sentences.txt --tts_weights ./pretrained_models/tacotron2.pyt --voc_weights ./pretrained_models/wavernn.pyt --save_dir ./results
```

### 新增依賴

```bash
# 新增一般依賴
uv add package-name

# 新增開發依賴
uv add --dev package-name

# 指定版本
uv add "package-name>=1.0.0"
```

### 移除依賴

```bash
uv remove package-name
```

### 更新依賴

```bash
# 更新所有依賴
uv lock --upgrade

# 更新特定套件
uv lock --upgrade-package package-name
```

## 常用指令

| 指令              | 說明                  |
| ----------------- | --------------------- |
| `uv sync`         | 同步依賴（安裝/更新） |
| `uv add <pkg>`    | 新增套件              |
| `uv remove <pkg>` | 移除套件              |
| `uv run <cmd>`    | 在虛擬環境中執行指令  |
| `uv lock`         | 更新鎖定檔            |
| `uv pip list`     | 列出已安裝套件        |

## 為什麼使用 uv？

- ⚡ **超快速**：比 pip 快 10-100 倍
- 🔒 **可重現性**：`uv.lock` 確保每次安裝都一致
- 🎯 **簡單**：一個指令搞定所有事
- 🔄 **相容性**：完全相容 `pyproject.toml` 標準

## 遷移說明

專案已從 `requirements.txt` 遷移到 `uv`：

- ✅ 依賴已定義在 `pyproject.toml`
- ✅ `uv.lock` 已生成
- ⚠️ `requirements.txt` 保留作為參考（可選擇刪除）
