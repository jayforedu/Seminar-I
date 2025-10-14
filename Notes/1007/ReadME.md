# 題目：半導體電漿電源的演進應用與設計關鍵
# 講者：洪再和
# 日期：2025/10/07
# 筆記內容：

## 電漿電源:半導體設備中最複雜及高技術的零組件

```mermaid
flowchart TB
    %% 上電極路徑
    A["RF Generator (Upper Electrode)
    Freq: 400kHz / 13.56 / 27 / 60 MHz"] --> 
    B["RF Matchbox (Upper)"] --> 
    C["Powered Electrode (Source)
    ICP Coil / Shower Head"]

    %% 下電極路徑
    C --> D["Electrostatic Chuck (ESC, Lower Electrode)"]
    D --> E["RF Matchbox (Lower)"]
    E --> F["RF Generator (Lower Electrode)
    Freq: 400kHz / 13.56 MHz"]

    %% 控制系統
    R["RPS (Remote Plasma Source)
        Control Power Input"]
    M["MFC (Mass Flow Controller)
        Control Gas Flow"]
    P["Pump (Vacuum Pump)
        Control Chamber Pressure"]

    %% 連線（虛線表示旁路控制）
    R -.-> B
    M -.-> C
    P -.-> D

```
## 電將電源的世代演進與啟示

| 時期           | 維修方式   | 世代   | 全球數量 | 製程節點          | 類型與控制方式             | 重量  | 元件       | 效率 (@full load) | 備註                    |
|----------------|------------|--------|-----------|-------------------|----------------------------|-------|-------------|------------------|-------------------------|
| 1980～原廠停修 | 整機替換   | 第一代 | ~10K EA   | (6吋/8吋) >90nm   | Class AB 類放大器 類比控制 | 65kg  | Si MOSFET   | <50%             |                         |
| 1990～原廠停修 | 升級維修   | 第二代 | ~120 EA   | 8吋/12吋 >16nm    | Class E 類放大器 類比控制  | 14kg  | Si MOSFET   | 65%              |                         |
| 2000～         | 維修保養   | 第三代 | ~200K EA  | 16–90nm           | Class E 類放大器 數位+類比控制 | 21kg  | Si MOSFET   | 65%              |                     |
| 2010～         | 維修保養   | 第四代 | ~200K EA  | <16nm             | Class E 類放大器 數位+同步+雙頻 | 16kg  | Si MOSFET   | 70%              |                   |
| 2022～         | 保固中     | 第五代 | ~50K EA   | <3nm              | Class E 類放大器 數位+同步+雙頻 | 16kg  | Si MOSFET   | —                | 無須 Matchbox / DirectDriver |

## 半導體蝕刻電漿系統:
### 控制方式xRF頻率混合x附載特性 <br>
CEX Control:同頻率，不同相位角度精準控穩電漿 <br>
Pulsing Control:高頻弦波下的方波開關導通控制<br>
Mix RF Frequency Source: 2+27+60 (Bias:13+60)<br>

## 現行高頻電漿電源三大瓶僅:<font color="red"> 電力品質、效率、散熱</font>
* 電力品質:諧波失真率最低卡在 **30%**
* 矽元件的電漿電源轉換率:仍有 **30%** 的提升潛力
* 5kW真空管的電漿電源效率低於 **30%** ，啟動就需耗電12kW廠務供電(17000W)=損失(12000W)+輸出(5000W)<br>
  效率 = 輸出/輸入 = 5000W/17000W = **29.4%**<br>
  損失 = 輸入-輸出 = 17000W-5000W = 12000W(熱損失)

## 轉換效率問題: 30% 的改善空間
線段由上至下為:歐制、美制四代、美制二代、美制三代、陸制、美制一代
```mermaid
xychart-beta
    title "各負載狀況下整機效率折線圖"
    x-axis "設定LOAD" [10, 20, 30 ,40, 50, 60, 70, 80, 90, 100]
    y-axis "效率 " 10 -->100
    line "US Gen 1" [15, 25, 30, 35, 40, 45, 48, 50, 52, 54]
    line "美製二代" [35, 48, 52, 55, 57, 59, 60, 62, 63, 64]
    line "美製三代" [30, 35, 40, 45, 50, 53, 55, 57, 58, 59]
    line "美製四代" [45, 55, 60, 65, 67, 68, 69, 70, 71, 72]
    line "歐製" [50, 65, 70, 72, 73, 74, 74, 75, 75, 75]
    line "陸製" [22, 30, 35, 40, 45, 48, 50, 52, 53, 54]
```
## 電壓壓降問題: SEMI F47 Voltage Sag 規範遠遠不足應付現實
```mermaid
xychart-beta
    title "Required Semiconductor Equipment Voltage Sag Ride-Through Capability Curve"
    x-axis "Duration of Voltage Sag In Second" [0.05,0.1,0.2,0.2,0.5,0.5,1.0]
    y-axis "Percent of Equipment Nominal Voltage " 0 -->100
    line "" [50,50,50,70,70,80,80]
```

## 電源散熱:熱累積導致故障及重大公安隱憂
* 第一代:70-90-150<sup>。</sup>C
* 第二第:90-110度<sup>。</sup>C

## 老舊的功率量測技術:良率的隱藏殺手
- P<sub>forword</sub>  =(V<sub>F</sub> )<sup>2</sup>/ 50 $\Omega$
- P<sub>reflected</sub>=(V<sub>R</sub>)<sup>2</sup> / 50 $\Omega$ <br>
 **VSWR>4就失真**

## RF Pulsing: 提升先進製程良率的關鍵優勢
- Improved CD control:Ensures dimensions of etched features are within tight tolerances
- Enhanced profile uniformity:Helps create consistent etch profiles across the entire wafer
- Icerased selectivity:Enables the etching of specific materials while minimizing the etching of others

## 設計契機: 13000 案例驗證+高效模組新方案
SiC/GaN+超高開關頻率 150kHz $\rightarrow$ 500kHz $\rightarrow$ 輕量化,更高效能,高功率密度<br>
第一代:50VDC/5kW $\eta$~97%模組
- 降溫 60<sup>。</sup>C
- 減重 18 公斤
- 效率提升 20%
- 諧波改善>90%
<br>

第二代:0-210VDC/5kW $\eta$~96%模組
- 降溫 60<sup>。</sup>C
- 減重 3 公斤
- 效率提升 20%-50%
- 諧波改善>90%
