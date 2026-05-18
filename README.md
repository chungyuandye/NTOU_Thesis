# 國立臺灣海洋大學學位論文 LaTeX 模板

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![LaTeX Engine: XeLaTeX](https://img.shields.io/badge/Engine-XeLaTeX-green.svg)](https://tug.org/xetex/)
[![Version](https://img.shields.io/badge/Version-1.3-orange.svg)](ntou-thesis.sty)

> **National Taiwan Ocean University (NTOU) Thesis LaTeX Template**  
> 依據《國立臺灣海洋大學博、碩士學位論文格式規範》（114-08-06）製作

---

## 目錄

- [功能特色](#功能特色)
- [檔案結構](#檔案結構)
- [環境需求](#環境需求)
- [快速開始](#快速開始)
- [論文元資料設定](#論文元資料設定)
- [書背（bookspine）編譯](#書背bookspine編譯)
- [字型說明](#字型說明)
- [常見問題](#常見問題)
- [授權](#授權)

---

## 功能特色

- ✅ 符合海大官方論文格式規範（封面、書名頁、摘要、目次、圖次、表次）
- ✅ 一鍵設定所有論文元資料（`\NTOUSetup{...}`）
- ✅ 自動產生封面、書名頁、學位考試及格證明書
- ✅ 可獨立編譯的書背（`bookspine.tex` → `bookspine.pdf`）
- ✅ 中英文雙語摘要環境
- ✅ 圖表連續編號（不重置章節）
- ✅ 字型自動偵測（支援 cwTeX、Noto 本機字型、系統字型三層 fallback）
- ✅ 浮水印支援（書名頁）
- ✅ 完整支援 TikZ / pgfplots 流程圖與統計圖

---

## 檔案結構

```
your-thesis/
├── ntou-thesis.sty          # 核心樣式套件（勿任意更動）
├── ntou_thesis_example.tex  # 論文主文件（從這裡開始撰寫）
├── bookspine.tex            # 書背獨立文件（另行編譯）
├── ntou-logo.pdf            # 封面校徽（請自行取得）
├── Watermark_JPG.jpg        # 書名頁浮水印圖（請自行取得）
└── fonts/                   # （選用）自備字型目錄
    ├── NotoSerifTC-Regular.ttf
    ├── NotoSerifTC-Bold.ttf
    ├── NotoSansTC-ExtraLight.ttf
    └── NotoSansTC-Bold.ttf
```

> **注意**：`ntou-logo.pdf` 與 `Watermark_JPG.jpg` 請向校方或系辦取得，不包含於本 repo。

---

## 環境需求

| 項目 | 需求 |
|------|------|
| TeX 發行版 | [TeX Live](https://www.tug.org/texlive/) 2022+ 或 [MiKTeX](https://miktex.org/) |
| 編譯引擎 | **XeLaTeX**（必須，不支援 pdfLaTeX / LuaLaTeX） |
| 作業系統 | Windows / macOS / Linux |
| 中文字型 | 見 [字型說明](#字型說明) |

---

## 快速開始

### 1. 複製本 repo

```bash
git clone https://github.com/your-username/ntou-thesis.git
cd ntou-thesis
```

### 2. 先編譯書背

書背需獨立產生 PDF 後，再由主文件匯入：

```bash
xelatex bookspine.tex
# 產出 bookspine.pdf
```

### 3. 編譯論文主文件

```bash
xelatex ntou_thesis_example.tex
xelatex ntou_thesis_example.tex   # 執行兩次以確保目次正確
```

### 使用 VS Code（推薦）

安裝 [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) 擴充套件，並在設定中將 Recipe 設為 `xelatex`。

### 使用 Overleaf

1. 上傳全部檔案（含 `fonts/` 目錄或確認系統字型可用）
2. 在 Overleaf 設定中將編譯器改為 **XeLaTeX**
3. 先編譯 `bookspine.tex`，下載 `bookspine.pdf` 後再上傳
4. 編譯 `ntou_thesis_example.tex`

---

## 論文元資料設定

在 `ntou_thesis_example.tex` 頂端的 `\NTOUSetup{...}` 填入您的論文資訊：

```latex
\NTOUSetup{
  mainfont      = {Times New Roman},        % 英文主字型
  department    = {航運管理學系},             % 系所中文名稱
  departmenten  = {Department of Shipping and Transportation Management},
  collegeen     = {College of Maritime Science and Management},
  degreezh      = {碩士},                   % 碩士 / 博士
  degreeen      = {Master of Science},      % Master of Science / Doctor of Philosophy
  titlezh       = {論文名稱},
  titleen       = {Thesis English Title},
  studentzh     = {學生姓名},
  studenten     = {Student Name},
  advisorzh     = {指導教授姓名 教授},
  advisoren     = {Prof. Advisor English Name},
  rocdate       = {中華民國 115 年 6 月},   % 封面日期
  endate        = {June 2026},
  spineyear     = {2026},                   % 書背西元年份
  logofile      = {ntou-logo.pdf},          % 封面校徽檔名
}
```

---

## 書背（bookspine）編譯

開啟 `bookspine.tex`，修改設定區（`①` 標示處）：

```latex
%% 系所名稱（每字加 \\ \vfill）
\def\bsDeptChars {航 \\ \vfill 運 \\ \vfill 管 \\ \vfill 理 \\ \vfill 學 \\ \vfill 系}
\def\bsDeptColH{5.5cm}   % 字數 × ~0.9cm

%% 論文題目（每字加 \\）
\def\bsTitleV  {\\您\\的\\論\\文\\題\\目}

%% 研究生姓名
\def\bsAuthorV {王\\小\\明}

%% 畢業年份（西元）
\def\bsYear    {2026}
```

編譯完成後，`bookspine.pdf` 會自動被主文件透過 `\includepdf` 匯入。

---

## 字型說明

本模板採三層字型自動偵測，**依序**嘗試：

| 優先順序 | 字型來源 | 說明 |
|---------|---------|------|
| 1 | `./cwTeX Q Kai Medium.ttf` | 置於專案根目錄的 cwTeX 楷書 |
| 2 | `fonts/NotoSerifTC-Regular.ttf` 等 | 置於 `fonts/` 子目錄的 Noto 字型 |
| 3 | 系統安裝字型 | `Noto Serif CJK TC`（需先安裝） |

**建議做法**：將 Noto 字型放至 `fonts/` 目錄（可從 [Google Fonts](https://fonts.google.com/noto/specimen/Noto+Serif+TC) 下載），確保跨平台一致性。

---

## 常見問題

**Q：編譯時出現 `This package requires XeLaTeX` 錯誤？**  
A：請確認使用 XeLaTeX 編譯，不支援 pdfLaTeX。

**Q：書背 PDF 沒有被匯入？**  
A：請先單獨執行 `xelatex bookspine.tex`，確認 `bookspine.pdf` 存在後再編譯主文件。

**Q：封面校徽或浮水印不顯示？**  
A：確認 `ntou-logo.pdf` 與 `Watermark_JPG.jpg` 已放置於專案根目錄，且 `\NTOUSetup` 中的 `logofile` 欄位正確。

**Q：中文字型顯示異常？**  
A：請依 [字型說明](#字型說明) 確認字型路徑。Overleaf 用戶建議使用 `fonts/` 目錄方式。

---

## 授權

本模板以 [MIT License](LICENSE) 釋出，歡迎自由使用與修改。  
若用於學術論文，感謝在致謝中提及本模板。
