
# Bilibili Automated Archival System 
### B站自动化视频归档与加密存储系统

## 1. Project Overview / 项目简介
**EN:** An automated Python pipeline for video data preservation, covering dynamic scraping, high-definition archiving, and AES-encrypted storage（to 7z zip）.


**CN:** 基于 Python 的视频数据保存流水线，涵盖动态爬虫、高清归档及 AES 加密存储（7z压缩）。

---

## 2. Core Workflow / 核心流程

1.  **Phase 1: Metadata Scraping (`Get_BID.py`)**
    *   Scrapes video's urls list from creator spaces via **Selenium** and generates `BID.xlsx`.
    *   通过 **Selenium** 爬取 UP 主投稿列表，生成种子文件 `BID.xlsx`。
2.  **Phase 2: Archival Pipeline (`GOOD_JOB2.py`)**
    *   **Acquisition**: Downloads 720P streams via `yt-dlp` & `FFmpeg`.
    *   **Mining**: Fetches real-time stats (views/favs) via RESTful APIs.
    *   **Security**: Generates random passwords and creates **AES-256** encrypted ZIPs.
    *   **归档任务**: 利用 `yt-dlp` & `FFmpeg` 采集高清流；通过 RESTful API 抓取播放量等统计数据；生成随机密码并进行 **AES-256** 加密打包。
<img width="1600" height="1806" alt="Archival_Pipeline_Flowchart (2)" src="https://github.com/user-attachments/assets/e24dbe8e-4af9-4de6-b917-24037abaf70a" />


3.  **Phase 3: Final result (`download_report.xlsx`)**
<img width="439" height="116" alt="669c37602d610b84b56b79cec1d5098d" src="https://github.com/user-attachments/assets/18c1fe8c-218f-4116-8988-b1e344a4e79b" />

**EN:** The system generates a comprehensive Excel report as a digital asset catalog, ensuring every archived video is indexed with its metadata and security credentials.

**CN:** 系统会自动生成一份详尽的 Excel 报表作为数字资产目录，确保每段归档视频都拥有完整的元数据记录与安全凭证。


| Index | 视频名称 (Title) | 发布日期 (Release) | 时长 (Duration) | 大小 (Size) | 播放量 (Views) | 解压密码 (Password) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 示例视频 A / Sample A | 2017-12-12 | 00:18:43 | 32.06 MB | 293,693 | mAUc** |
| 2 | 示例视频 B / Sample B | 2017-12-20 | 00:16:11 | 22.07 MB | 176,637 | ngsP** |
| 4 | 示例视频 C / Sample C | 2019-02-05 | 00:05:59 | 43.93 MB | 932,924 | cSZo** |
| ... | ... | ... | ... | ... | ... | ... |


---

## 3. Data Seed Structure / 数据结构 (BID.xlsx)

| Column/列名 | Description/描述 |
| :--- | :--- |
| **视频标题 (Title)** | Original title for indexing. / 原始标题用于索引。 |
| **完整链接 (URL)** | Bilibili Video URL (BV ID). / 视频 BV 号链接。 |
<img width="491" height="313" alt="07529312bdbccb1f456247f88e549d12" src="https://github.com/user-attachments/assets/9a4f3601-9efb-4dd1-a6a0-bb52f252f808" />

---

## 4. Technical Highlights / 技术亮点

*   **Automation**: Selenium handles dynamic rendering & pagination.
    *   **自动化**: 使用 Selenium 模拟浏览器处理动态加载与翻页。
*   **Data Integrity**: Robust indexing mechanism ensures no ID duplication even if folders are deleted.
    *   **数据一致性**: 稳健的索引机制，确保即使本地文件删除，序列号依然连续不重复。
*   **Security**: AES-encrypted archival prevents data corruption or cloud-sync censorship.
    *   **安全性**: AES 加密归档，防止数据损坏或云端同步时的内容屏蔽。

---

## 5. Motivation & Reflection / 初衷与心得

**EN:** 
Cloud storage is prone to remote "locking" or censorship. So I built this "Local-First" encrypted vault. It transforms manual saving into a programmable pipeline, ensuring that valuable digital content remains accessible and private regardless of platform changes.

**CN:** 
云端存储易受远程封存或审查影响。因此我设计了这套“本地优先”的加密库方案。将手动备份转化为可编程的自动化流水线，确保即便平台变动，优质内容依然能以私密、完整的方式长期留存。

---

## 6. Tech Stack / 技术栈

*   **Scraping**: Selenium, Chrome WebDriver
*   **Media**: yt-dlp, FFmpeg
*   **Data**: openpyxl (Excel), Requests (API)
*   **Storage**: pyzipper (AES-256 Encryption - 7z)
