---
title: "🚀 **Tự Động Hóa Hunter Tìm Việc Upwork: Lấy Dữ Liệu Cập Nhật + Gửi Báo Cáo AI Hàng Ngày**"
description: "Workflow tự động hóa hoàn toàn giúp các sếp tìm kiếm, lưu trữ và tổng hợp công việc trên Upwork hàng ngày bằng AI, gửi báo cáo email định kỳ với chi tiết công việc mới nhất. Giúp tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-hunter-tim-viec-upwork"
tags: [n8n, automation, no-code, ai, upwork, google-sheets, openai, email-automation]
keywords: [tự động hóa tìm việc upwork, n8n workflow upwork, ai tổng hợp công việc freelance, tự động hóa email báo cáo công việc, apify upwork scraper]
---

# 🚀 **Tự Động Hóa Hunter Tìm Việc Upwork: Lấy Dữ Liệu + Gửi Báo Cáo AI Hàng Ngày**

## **💡 Giới Thiệu: Tiết Kiệm 80% Thời Gian Tìm Việc Thông Qua Tự Động Hóa**
Làm việc tự động hóa tìm kiếm công việc trên Upwork vẫn là một trong những **nỗi đau lớn nhất** của các freelancer và nhà tuyển dụng. Các sếp phải:
- **Quét hàng chục trang** trên Upwork mỗi ngày để tìm kiếm công việc phù hợp.
- **Lưu trữ thủ công** thông tin công việc vào Google Sheets hoặc Excel.
- **Tổng hợp và gửi báo cáo** cho đồng nghiệp hoặc bản thân hàng tuần.
- **Lo lắng bỏ lỡ** những cơ hội hấp dẫn vì không theo dõi thường xuyên.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Lấy dữ liệu công việc mới nhất** từ Upwork hàng ngày (hoặc theo lịch bạn đặt).
✅ **Lưu trữ tự động** vào Google Sheets với định dạng chuẩn.
✅ **Tổng hợp bằng AI** (OpenAI GPT-4o-mini) thành báo cáo ngắn gọn, dễ đọc.
✅ **Gửi email tự động** với báo cáo hàng ngày (hoặc theo lịch bạn chọn).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/tuần** so với cách làm thủ công.
- **Không bỏ lỡ công việc** nào vì hệ thống chạy 24/7.
- **Báo cáo AI tự động** giúp bạn nhanh chóng lọc ra những công việc phù hợp.
- **Lưu trữ dữ liệu dài hạn** trên Google Sheets để theo dõi xu hướng thị trường.
- **Cá nhân hóa** với email báo cáo định dạng chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Upwork** (để lấy dữ liệu công việc).
2. **Tài khoản Apify** (để sử dụng scraper Upwork):
   - [Đăng ký Apify miễn phí](https://apify.com/) và tạo một **task** từ [Upwork Scraper](https://apify.com/upwork/upwork-jobs-scraper/overview).
   - Lưu **Task ID** và **API Token** của bạn (sẽ dùng trong node `Fetch Upwork Jobs`).
3. **Google Sheets** với cấu trúc bảng như sau:
   | Title       | URL               | Description          | Budget | DatePosted |
   |-------------|-------------------|----------------------|--------|------------|
   | (Dữ liệu tự động điền) | (Dữ liệu tự động điền) | (Dữ liệu tự động điền) | (Dữ liệu tự động điền) | (Dữ liệu tự động điền) |
4. **Tài khoản Gmail** (để gửi email báo cáo).
5. **API Key OpenAI** (để sử dụng AI tổng hợp):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
6. **Credentials trong n8n**:
   - **Google Sheets OAuth2** (cấu hình trong n8n).
   - **Gmail OAuth2** (cấu hình trong n8n).
   - **OpenAI API** (cấu hình trong n8n).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
:::note[HƯỚNG DẪN CHI TIẾT]
- **Bước 1:** Tải workflow từ [n8n.io/workflows/4733](https://n8n.io/workflows/4733) hoặc [tải file JSON](https://github.com/n8n-io/workflows/raw/main/workflows/4733.json).
- **Bước 2:** Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON.
- **Bước 3:** Chọn **Self-hosted** (nếu bạn tự host n8n) hoặc **n8n Cloud** (nếu dùng dịch vụ cloud).
:::

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow được chia thành **3 nhóm chính**, mỗi nhóm có nhiệm vụ riêng. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **🟢 Nhóm 1: 📥 Lấy Dữ Liệu & Chuẩn Bị Công Việc Upwork**
**Mục tiêu:** Lấy dữ liệu công việc mới nhất từ Upwork và chuẩn bị cho bước sau.

| Node | Loại | Cấu Hình Cần Thiết |
|------|------|---------------------|
| **🕒 Daily Upwork Job Trigger** | Schedule Trigger | - Chọn **Cron** (ví dụ: `0 0 */6 * * *` để chạy mỗi 6 giờ). |
| **🌐 Fetch Upwork Jobs (Apify)** | HTTP Request | - **URL:** `https://api.apify.com/v2/actor-tasks/<TASK_ID>/run-sync-get-dataset-items?token=<API_TOKEN>` <br> *(Thay `<TASK_ID>` và `<API_TOKEN>` bằng dữ liệu từ Apify của bạn.)* <br> - **Method:** POST <br> - **Headers:** `Content-Type: application/json` <br> - **Body:** `{"datasetId": "<DATASET_ID>"}` *(Lấy từ Apify Task của bạn.)* |
| **🛠️ Format Job Fields** | Set | - Chọn **Fields** và chỉ giữ lại các trường cần thiết: `title`, `url`, `description`, `budget`, `datePosted`. |

#### **🟡 Nhóm 2: 🧾 Lưu Trữ & Tổng Hợp Công Việc Bằng AI**
**Mục tiêu:** Lưu dữ liệu vào Google Sheets và tạo báo cáo tổng hợp bằng AI.

| Node | Loại | Cấu Hình Cần Thiết |
|------|------|---------------------|
| **📈 Log Jobs to Google Sheet** | Google Sheets | - **Credentials:** Chọn `googleSheetsOAuth2Api`. <br> - **Operation:** Append (thêm dữ liệu mới vào cuối bảng). <br> - **Sheet Name:** Đặt tên bảng (ví dụ: `Upwork Jobs`). <br> - **Range:** `Sheet1!A1` (nếu bảng có tên `Sheet1`). |
| **🤖 Summarize Job Listings** (AI Agent) | Agent | - **Sub-Node 1: OpenAI Job Summarizer** <br> - **Prompt:** <br> ``` <br> You are an assistant summarizing freelance job postings. For each job, provide a concise summary in 1-2 lines including: <br> - Job title <br> - Budget range <br> - Key requirements <br> - A brief description of the work <br> Format the output as a bullet point list. <br> ``` <br> - **Model:** `gpt-4o-mini` (đã cấu hình sẵn). <br> - **Credentials:** Chọn `openAiApi`. <br> - **Sub-Node 2: Parse Summary Output** <br> - **Output Format:** Chọn `JSON` để n8n hiểu được kết quả từ AI. |
| **📄 Parse Summary Output** | Output Parser Structured | - **Schema:** Đặt tên `JobSummary` và cấu trúc như sau: <br> ```json <br> { <br> "title": "string", <br> "budget": "string", <br> "requirements": "string", <br> "description": "string" <br> } <br> ``` |

#### **🔴 Nhóm 3: ✉️ Gửi Báo Cáo Email**
**Mục tiêu:** Gửi email báo cáo tổng hợp công việc hàng ngày.

| Node | Loại | Cấu Hình Cần Thiết |
|------|------|---------------------|
| **📧 Send Job Summary Email** | Gmail | - **Credentials:** Chọn `gmailOAuth2`. <br> - **To:** Địa chỉ email của bạn (hoặc team). <br> - **Subject:** `"🚀 New Upwork Jobs Found!"` <br> - **Body:** <br> ``` <br> Hello, <br> <br> Here’s a summary of the latest Upwork jobs matching your criteria: <br> <br> {{#each $item}} <br> - **{{$item.title}}** (Budget: {{$item.budget}}) <br>   Requirements: {{$item.requirements}} <br>   Description: {{$item.description}} <br>   <br> {{/each}} <br> <br> ➕ View full job list here: [Google Sheet Link] <br> <br> Best, <br> Your Automation Bot 🤖 <br> ``` <br> - **Lưu ý:** Sử dụng **IF node** (nếu cần) để kiểm tra xem có dữ liệu mới không trước khi gửi email. |

---
### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy thử với dữ liệu mẫu để kiểm tra workflow.
2. **Bật Active:** Sau khi kiểm tra xong, bật **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Lọc Công Việc Theo Từ Khóa:**
   - Thêm **Filter Node** sau `Fetch Upwork Jobs` để chỉ lấy công việc có từ khóa như "React", "Python", "Marketing"...
   - Ví dụ: `{{$json.title.includes("React")}}`.

2. **Tránh Lặp Dữ Liệu:**
   - Thêm **Set Node** để lưu **ID của công việc** đã lấy trước đó vào một bảng Google Sheets khác.
   - Sau đó, sử dụng **IF node** để kiểm tra xem công việc đã tồn tại chưa trước khi lưu.

3. **Gửi Báo Cáo Slack/Telegram:**
   - Thêm **Slack Node** hoặc **Telegram Bot Node** để gửi báo cáo ngay khi có công việc mới.

4. **Tạo Báo Cáo Hàng Tháng:**
   - Sử dụng **Schedule Trigger** khác để chạy workflow vào cuối tháng và gửi báo cáo tổng hợp.

5. **Tự Động Xóa Công Việc Cũ:**
   - Thêm **Google Sheets Query Node** để xóa công việc cũ hơn 30 ngày.
:::

---
## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này là **giải pháp hoàn hảo** cho các freelancer, nhà tuyển dụng hoặc team marketing muốn tự động hóa quá trình tìm kiếm và theo dõi công việc trên Upwork. Bằng cách kết hợp **scraping dữ liệu, AI tổng hợp và email tự động**, bạn sẽ:
✔ **Không bỏ lỡ công việc** nào.
✔ **Tiết kiệm thời gian** lên tới 80%.
✔ **Có báo cáo chuyên nghiệp** hàng ngày.

**Hành động ngay:**
1. **Chuẩn bị tài khoản** (Apify, Google Sheets, Gmail, OpenAI).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa cuộc sống làm việc của mình!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ thêm?** Liên hệ với tác giả Yaron Been qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)