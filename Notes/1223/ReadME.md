# 題目：Ultra Lightweight Dehaze Methods for Robot Vision Using High-Level Synthesis
# 講者：Chi-Chia Sun
# 日期：2025/12/23
# 筆記內容：
## 1. 研究背景與目標 (Main Objective)

* **開發高效能除霧演算法**：針對霧氣 (defog)、雨滴 (derain)、低照度 (low light) 及水下 (under water) 等環境，開發優於或等同現有技術的超除霧演算法。
* **優化計算需求**：消除現有方法的缺點並極小化運算資源消耗，以利於嵌入式硬體實作。
* **硬體 IP 實作**：使用高階合成 (HLS) 技術將演算法實作為 FPGA IP，並整合至 HDMI 影像流水線 (Pipelining) 中。
* **機器人視覺應用**：解決自然界霧氣導致影像退化，進而影響 YOLO 或 ViT 等機器學習模型在物體偵測、分類、追蹤與分割上的表現。

---

## 2. 異質運算與 FPGA 技術趨勢 (FPGA Trends & Heterogeneous Computing)

* **先進製程與雲端加速**：目前技術已達 7nm FinFET+ (Xilinx Versal 平台)，AWS 等雲端服務自 2018 年起已大規模採用 FPGA 實例。
* **異質運算架構**：
    * **MPSoC**：結合多核心處理器 (ARM) 與 FPGA，用於 AI、機器學習、ADAS 與 SDR 等高級數據處理。
    * **RFSoC**：進一步整合高帶寬 ADC/DAC，用於無線通訊與雷達系統。
* **開發工具與框架**：
    * **PYNQ**：由 Xilinx 與德州大學奧斯汀分校開發，利用 Python 的生產力來簡化 Zynq 或 UltraScale+ 的開發流程。
    * **High-Level Synthesis (HLS)**：支持將 C/C++ 編譯為 RTL (Verilog/VHDL)，降低硬體設計門檻並加速設計探索。



---

## 3. 除霧演算法實作細節 (Dehaze Method & Implementation)

### 3.1 演算法流程
演算法核心包含以下關鍵步驟：
1.  **暗通道提取 (Dark Channel Extraction)**
2.  **亮通道提取 (Bright Channel Extraction)**
3.  **自適應霧氣因子 (Adaptive Fog Factor)**
4.  **傳輸圖估計 (Transmission Map Estimation)**
5.  **場景修復 (Scene Recovery)**
6.  **對比度拉伸 (Contrast Stretching)** 等後處理。

### 3.2 FPGA 硬體優化
* **影像流水線 (Video Pipelining)**：採用 **Ping-pong buffer** 實作，在 1080p 30FPS 解析度下僅有 **2 幀 (2 frames)** 的延遲。
* **動態調整**：支援在線 (On-the-fly) 即時調整參數。
* **計算優化**：透過 HLS 展開迭代 (Unfolding iterations) 以極小化計算時間，並針對 Framebuffer 格式調整 I/O 接口。

---

## 4. 實驗數據與結果評估 (Results & Evaluation)

### 4.1 影像品質對比 (RESIDE Dataset)
在 MATLAB R2024b 環境下測試，提議的方法在吞吐量 (Throughput) 上具有絕對優勢：

| 指標 (Metrics) | DCP [4] | Dehaze-Net [17] | Dehaze-Former [21] | **Proposed (本研究)** |
| :--- | :---: | :---: | :---: | :---: |
| **FPS $\uparrow$** | 0.23 | 2.73 | 0.42 | **384.17** |
| **PSNR $\uparrow$** | 17.475 | 22.917 | 37.218 | **22.101** |
| **SSIM $\uparrow$** | 0.821 | 0.888 | 0.989 | **0.898** |

*備註：與傳統 DCP 相比，本方法能有效消除色偏 (Color Shifting) 並保留影像自然度。*

### 4.2 電腦視覺檢測提升 (COCO Dataset)
使用 **YOLOv7-tiny** 預訓練模型進行物體偵測測試：
* **mAP 提升**：在極濃霧 ($\beta=3.0$) 環境下，除霧後 mAP 從 26.3% 提升至 34.2%，改善幅度達 **7.9%**。
* 在各種霧氣濃度 ($\beta=1.0 \sim 3.0$) 下，檢測結果均優於其他現有除霧方法。

### 4.3 硬體資源消耗 (ZCU104 平台)
根據 Vitis 與 Vivado 工具鏈報告，本電路具有極小的硬體佔用：

| 資源項目 (Resource) | 使用量 (Utilization) | 佔用比例 (%) |
| :--- | :---: | :---: |
| **LUT** | 6950 | 19% |
| **FF** | 7912 | 13% |
| **BRAM** | 78 | 18% |
| **DSP** | 25 | 2% |
| **理論最大 FPS** | **115.3** | - |

---

## 5. 未來擴展：低照度增強 (Low Light Enhancement)

* **目標**：開發針對低照度環境的超快速增強演算法。
* **數據合成**：利用 **CycleGAN** 技術從原始 COCO 數據集生成合成的黑暗影像 (Synthetic Dark)，用以訓練與評估模型。
* **技術對標**：目前正與 EnlightenGAN、Zero-DCE、AnlightenDiff 等前沿模型進行效果比對。
