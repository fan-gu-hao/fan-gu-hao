# 嵌入式 Linux 核心與驅動整合 × 異質多核心 × MCU AI／邊緣人工智慧

**Embedded Linux Kernel / BSP / Driver Integration · Heterogeneous Multicore · MCU AI / TinyML · Edge AI**

你好，我是 **fan-gu-hao**。我專注於嵌入式 Linux 核心與板級支援套件（Board Support Package，BSP）、驅動程式原始碼分析與修改、異質多核心通訊，以及微控制器（MCU）與邊緣人工智慧（Edge AI）的實機整合。實作內容涵蓋 Linux 裝置樹與 pinctrl 驅動探測流程除錯、感測器介面移植、FreeRTOS、多程序／多執行緒協作、DDR／MSMC 記憶體資源配置、跨核心訊息傳輸，以及 Hailo-8L 與 TI C71／MMA 等 AI 加速平台的量化與部署。

Hello, I'm **fan-gu-hao**. I build and validate embedded systems spanning Linux kernel/BSP integration, driver source analysis and targeted modifications, inter-processor communication, microcontroller firmware, concurrent real-time systems, and MCU/edge AI inference. My work also covers DDR/MSMC memory reservation, cross-core messaging, and AI deployment on Hailo-8L and TI C71/MMA platforms. My focus is on making hardware, operating systems, and AI workloads work together reliably on real boards.

## 核心工程能力｜Technical Focus

| 技術領域（Area） | 實作重點（Hands-on Work） |
| --- | --- |
| **嵌入式 Linux／BSP／驅動整合**<br>Embedded Linux / BSP / Driver Integration | Linux 核心與模組編譯、pinctrl 驅動探測路徑修改與追蹤、裝置樹與 I²C／接腳資源配置、開機服務。<br>Kernel/module builds, pinctrl driver probe-path instrumentation, device-tree and I²C/pin resource configuration, and boot-time services. |
| **異質多核心與即時系統**<br>Heterogeneous Multicore / RTOS | STM32MP1 Cortex-A7 Linux ↔ Cortex-M4 韌體、BeagleBone AI-64 的 A72 Linux ↔ C71／MMA ↔ R5F 協作，以及 STM32N6 的 FreeRTOS 多工作；包含 OpenAMP／RPMsg 與 remoteproc。<br>STM32MP1 Cortex-A7 Linux/Cortex-M4 firmware, BeagleBone AI-64 A72 Linux/C71-MMA/R5F integration, and STM32N6 FreeRTOS tasks; OpenAMP/RPMsg and remoteproc. |
| **MCU AI／TinyML 相關部署／NPU**<br>MCU AI / TinyML-related Deployment / NPU | STM32N6 上的關鍵字辨識與視覺模型部署、INT8 量化、Neural-ART 編譯、板端驗證、效能與記憶體分析。<br>STM32N6 keyword spotting and vision deployment, INT8 quantization, Neural-ART compilation, and on-board performance/memory analysis. |
| **平行處理與系統可靠性**<br>Concurrency / Reliability | 多程序、多執行緒、佇列與互斥鎖、DMA／快取一致性、影格時序與有效性管理、控制狀態機及故障保護。<br>Multiprocessing, multithreading, queues/locks, DMA/cache coherency, frame validity/timing, state machines, and fault handling. |
| **跨核心記憶體與資料傳輸**<br>Cross-Core Memory / Transport | BeagleBone AI-64 的 DDR／MSMC 裝置樹保留區、連結器區段、遠端核心資源表、RPMsg 分塊傳圖與 CRC32 驗證。<br>DDR/MSMC reservation in the device tree, linker sections, remote-core resource tables, and chunked RPMsg image transport with CRC32 verification on BeagleBone AI-64. |
| **MCU 與硬體介面**<br>MCU / Hardware Interfaces | C 語言韌體、GPIO、PWM、UART、I²C、計時器、中斷與感測器整合。<br>C firmware, GPIO, PWM, UART, I²C, timers, interrupts, and sensor integration. |

## 代表作品｜Featured Engineering Projects

### 1. STM32N6：即時實例分割與 NPU 部署
**STM32N6: Real-Time Instance Segmentation and NPU Deployment**

以 STM32N6570-DK 實作 YOLOv8n-seg：模型轉換、ST 逐通道 INT8 量化、Neural-ART 編譯、後處理適配、攝影機／顯示整合與板端驗證。固定輸入推論平均約 **48.61 毫秒**；完成 **50 張影像回歸驗證**，並保留記憶體配置實驗與測試證據。

Deployed YOLOv8n-seg on STM32N6570-DK with per-channel INT8 quantization, Neural-ART compilation, postprocessing integration, camera/display pipelines, and on-board validation. Fixed-input inference averaged approximately **48.61 ms**, with a **50-image regression test** and documented memory-layout experiments.

**[查看專案與技術證據｜Repository and evidence](https://github.com/fan-gu-hao/stm32n6-instance-segmentation)**

### 2. STM32N6：語音與視覺雙模型協作
**STM32N6: Voice-Guided Dual-Model Vision System**

整合自行訓練的關鍵字辨識（Keyword Spotting，KWS）與 YOLOv8 視覺模型，以 FreeRTOS 三個工作協作處理收音、推論與顯示。涵蓋 MDF／DMA 音訊擷取、MFCC、INT8 部署、CPU／NPU 快取一致性及共享 NPU 的排程。KWS 五折開發驗證 **98.68%（224／227）**，16 段保留音訊的離線 INT8 評估為 **93.75%（15／16）**；兩者不代表通用場景準確率。

Integrated a custom-trained keyword-spotting (KWS) model and YOLOv8 vision inference through three cooperating FreeRTOS tasks. The system covers MDF/DMA audio capture, MFCC features, INT8 deployment, CPU/NPU cache coherency, and sequential use of a shared NPU. KWS achieved **98.68% (224/227)** in five-fold development validation and **93.75% (15/16)** on a small held-out offline INT8 set; these are dataset-specific results.

**[查看專案與技術證據｜Repository and evidence](https://github.com/fan-gu-hao/stm32n6-voice-object-finder)**

### 3. STM32MP1：Linux／Cortex-M4 韌體異質核心與 BSP 整合
**STM32MP1: Linux/Cortex-M4 Firmware Heterogeneous Multicore and BSP Integration**

於 STM32MP157F-DK2 整合 Cortex-A7 Linux 與 Cortex-M4，以 OpenAMP／RPMsg 雙向傳送 VL53L0X 測距資料及控制命令。實作 Linux 核心與裝置樹建置、pinctrl 驅動探測紀錄修改、I²C5 與接腳資源配置、M4 感測器介面移植、圖形介面及 systemd 開機部署。

Integrated Cortex-A7 Linux and Cortex-M4 on STM32MP157F-DK2 through bidirectional OpenAMP/RPMsg communication. Implemented kernel/device-tree build workflows, targeted pinctrl driver probe logging changes, I²C5 pin/resource ownership, M4-side sensor API porting, a Linux graphical interface, and systemd-based startup integration.

**[查看專案與技術證據｜Repository and evidence](https://github.com/fan-gu-hao/stm32mp1-a7-m4-system-integration)**

### 4. Jetson Orin Nano × STM32：智慧巡邏避障車
**Jetson Orin Nano × STM32: Edge-AI Patrol and Obstacle-Avoidance Vehicle**

獨立完成車體選配、電源分路、硬體配線、Jetson Linux 環境、STM32F412 韌體與整車系統整合。以 YOLO 影像推論、雷達與四向測距支援感知；以多程序／多執行緒分離影像、網路及感測工作；由 STM32 負責 PWM、UART 與獨立安全保護，並整合 5G 遠端操作。

Independently developed the vehicle from hardware selection and power distribution to Jetson software, STM32F412 firmware, and full-system testing. Combined YOLO vision, LiDAR, and four-direction ranging with multiprocessing/multithreading, 5G remote operation, and an MCU-side safety control layer.

**[查看完整專案｜Repository](https://github.com/fan-gu-hao/smart-car)** · **[觀看實機展示｜Demo video](https://youtu.be/pAVebk_odPo)**

### 5. BeagleBone AI-64：異質多核心、雙 AI 加速單元與感測融合
**BeagleBone AI-64: Heterogeneous Multicore, Dual AI Acceleration and Sensor Fusion**

整合 **A72 Linux、Hailo-8L、TI C71 DSP／MMA 與 R5F**，完成 YOLOv8n 物件偵測、MobileNetV2 人體姿態估計、HX711 荷重感測及 MLX90614 紅外線表面測溫。由人物偵測框引導姿態模型裁切，再結合手腕線索、荷重事件與溫度資訊。底層實作涵蓋 **DDR／MSMC 保留記憶體、連結器區段、遠端處理器資源表、RPMsg 分塊影像傳輸與 CRC32、C71／MMA 模型服務及 R5F 感測韌體**，並使用獨立服務、多程序與多執行緒整合。已保存的整合展示結果約為 **9.7～10.1 幀／秒**；這是整個展示流程的速度，不是單一加速器的獨立吞吐量。

Integrated **A72 Linux, Hailo-8L, TI C71 DSP/MMA, and R5F** for YOLOv8n object detection, MobileNetV2 human pose estimation, HX711 load sensing, and MLX90614 infrared surface temperature acquisition. Person detection guides pose cropping, while wrist proximity, load transitions, and temperature contribute to event descriptions. Low-level work includes **DDR/MSMC reserved memory, linker sections, remote-processor resource tables, chunked RPMsg image transfer with CRC32, a C71/MMA inference service, and R5F sensor firmware**, coordinated through separate services, processes, and threads. The recorded end-to-end demonstration ran at approximately **9.7–10.1 frames/s**; this is not standalone accelerator throughput.

*「雙 NPU」是專案中對 Hailo-8L 與 TI MMA 兩個加速單元的簡稱；C71 本身是 DSP，不是另一顆獨立 NPU。*
*“Dual NPU” is project shorthand for the Hailo-8L and TI MMA acceleration units; C71 itself is a DSP, not an additional standalone NPU.*

**[查看系統架構、原始碼與驗證紀錄｜Repository, architecture and validation](https://github.com/fan-gu-hao/beaglebone-ai64-hailo8l-heterogeneous-multicore-dual-npu-dual-model-collaborative-inference)**

## 開發方式｜Engineering Approach

我重視**可重建、可量測、可追溯**的工程成果。各專案儲存庫盡可能保留核心原始碼、系統架構、部署步驟、測試紀錄，以及自行實作與第三方元件的界線；效能數據也會標明量測條件及適用範圍。

I prioritize **reproducibility, measurement, and traceability**. My repositories document architecture, source code, deployment steps, validation evidence, and the boundary between my own implementation and third-party components. Performance figures are reported with their measurement scope and limitations.

---

**目前關注方向｜Areas of Interest:** 嵌入式 Linux／BSP、Linux 裝置驅動開發、底層韌體、異質多核心、MCU AI／TinyML，以及 NPU／GPU／DSP 軟硬體整合。  
**Current Focus:** Embedded Linux/BSP, Linux device driver development, low-level firmware, heterogeneous multicore systems, MCU AI/TinyML, and NPU/GPU/DSP software–hardware integration.
