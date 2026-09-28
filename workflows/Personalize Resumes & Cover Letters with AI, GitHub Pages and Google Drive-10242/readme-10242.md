---
title: "🚀 Tự Động Hóa CV & Bài Thư Tính Cá Nhân Hoá AI + GitHub Pages + Google Drive (N8N)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tạo CV và bài thư ứng tuyển cá nhân hoá dựa trên mô tả công việc, kinh nghiệm cá nhân, và tích hợp lưu trữ trên GitHub Pages + Google Drive. Giúp tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-cv-va-bai-thu-tinh-ca-nhan-hoa-ai-github-google-drive"
tags: [n8n, automation, no-code, ai-rag, google-drive, github-pages, openai, telegram-notification]
keywords: [n8n workflow tự động hóa cv, ai cá nhân hóa bài thư, gitHub Pages tự động, Google Drive lưu CV, OpenAI GPT-5 cho ứng tuyển việc làm]
---

# 🚀 **Tự Động Hóa CV & Bài Thư Tính Cá Nhân Hoá AI: Từ Mô Tả Công Việc → CV + Bài Thư Chỉ Với Một Clic**

Hiện nay, việc ứng tuyển việc làm thường bắt đầu từ việc **tìm kiếm công việc phù hợp**, **tạo CV và bài thư ứng tuyển cá nhân hoá**, rồi cuối cùng là **nộp hồ sơ**. Tuy nhiên, quá trình này thường tốn thời gian và dễ gây **chán nản** khi phải viết lại CV và bài thư cho từng công việc khác nhau. Thậm chí, nhiều sếp còn phải **quay lại chỉnh sửa lại sau khi nhận phản hồi từ nhà tuyển dụng**.

**Workflow này giải quyết vấn đề này bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ mô tả công việc → CV cá nhân hoá + bài thư ứng tuyển.
✅ **Sử dụng AI (GPT-5) để phân tích mô tả công việc** và so sánh với kinh nghiệm cá nhân của sếp.
✅ **Tích hợp GitHub Pages** để lưu trữ CV dưới dạng trang web cá nhân (miễn phí, chuyên nghiệp).
✅ **Lưu CV và bài thư vào Google Drive** để dễ dàng chia sẻ hoặc in ấn.
✅ **Gửi thông báo tự động qua Telegram** khi hoàn thành.

Không cần viết code, không cần kiến thức kỹ thuật nào – chỉ cần **cài đặt workflow này và kích hoạt**, sếp sẽ có **CV và bài thư ứng tuyển hoàn chỉnh** chỉ trong vài giây!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công (không cần viết lại CV/bài thư từ đầu).
- **CV và bài thư 100% cá nhân hoá** dựa trên mô tả công việc và kinh nghiệm cá nhân.
- **Lưu trữ chuyên nghiệp** trên GitHub Pages (trang web cá nhân miễn phí) và Google Drive.
- **Thông báo tự động** khi hoàn thành qua Telegram (không cần theo dõi thủ công).
- **Dễ dàng chia sẻ** với nhà tuyển dụng hoặc in ấn.
- **Cập nhật liên tục** khi có kinh nghiệm mới (thêm vào cơ sở dữ liệu).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **OpenAI API Key** (để sử dụng GPT-5 và GPT-5-mini).
   - **Google Sheets API** (để lưu trữ dữ liệu kinh nghiệm và kết quả).
   - **Google Drive API** (để upload CV và bài thư).
   - **GitHub Account** (để lưu trữ trang web cá nhân).
   - **Telegram Bot Token** (để nhận thông báo).

2. **Dữ liệu ban đầu**:
   - **Kinh nghiệm làm việc** (sếp cần nhập vào bảng Google Sheets trước khi chạy workflow).
   - **Mô tả công việc** (sẽ được nhập qua Telegram hoặc Webhook).

3. **Cấu hình GitHub Pages**:
   - Một **repository GitHub** để lưu trữ CV dưới dạng trang web.
   - File `style.css` (đã có trong workflow, chỉ cần upload lên GitHub một lần).

---
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải workflow từ [n8n.io/workflows/10242](https://n8n.io/workflows/10242) hoặc copy JSON từ đây.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON vào.
- **Bước 3**: Chọn **Active** để kích hoạt workflow.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **3 phần chính**:
- **Experience Input Agent** (lưu trữ kinh nghiệm).
- **Job Analyst Agent** (tạo CV và bài thư).
- **GitHub Pages + Google Drive** (lưu trữ kết quả).

##### **A. Cấu Hình API và Credentials**
Các sếp cần **điền thông tin API** vào các node sau:
| **Node**               | **Tham Số Cần Điền**               | **Lưu Ý**                                                                 |
|------------------------|--------------------------------------|----------------------------------------------------------------------------|
| **OpenAI Chat Model**  | `openAiApi` (API Key OpenAI)        | Đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys) và thêm vào n8n. |
| **Google Sheets**      | `googleSheetsOAuth2Api`             | Cấu hình OAuth 2.0 trong n8n và chọn sheet chứa kinh nghiệm.              |
| **Google Drive**       | `googleDriveOAuth2Api`              | Cấu hình OAuth 2.0 và chọn folder lưu CV/bài thư.                        |
| **GitHub**            | `githubApi` (Token GitHub)          | Tạo token tại [GitHub Settings](https://github.com/settings/tokens) và thêm vào n8n. |
| **Telegram**          | `telegramApi` (Bot Token)           | Tạo bot tại [@BotFather](https://t.me/BotFather) và thêm vào n8n.          |

##### **B. Cấu Hình Bảng Google Sheets (Experience Table)**
- **Bước 1**: Tạo một **bảng Google Sheets** mới và chia sẻ với n8n.
- **Bước 2**: Đặt tên sheet là **"Experience"** và cấu trúc cột như sau:
  | Cột 1 (ID) | Cột 2 (Tên Công Ty) | Cột 3 (Vị Trí) | Cột 4 (Thời Gian) | Cột 5 (Mô Tả Kinh Nghiệm) |
  |------------|----------------------|-----------------|--------------------|---------------------------|
  | 1          | Công Ty A            | Dev              | 2020-2023          | "Làm việc với team backend..." |
- **Bước 3**: Trong node **"experience table"**, chọn sheet này và **chế độ "get"** để workflow đọc dữ liệu.

##### **C. Cấu Hình GitHub Pages**
- **Bước 1**: Tạo một **repository mới** trên GitHub (ví dụ: `sếp-tên-cv`).
- **Bước 2**: Upload file `style.css` (từ node **"style.css1"**) vào folder `css` của repo.
- **Bước 3**: Trong node **"index.html setup"**, chọn file `index.html` trong repo và **chọn chế độ "edit"** để workflow tự động cập nhật CV.

##### **D. Cấu Hình Webhook & Telegram**
- **Bước 1**: Trong node **"Webhook"**, giữ nguyên `path` hoặc thay đổi thành URL webhook của sếp.
- **Bước 2**: Trong node **"Telegram Trigger"**, cấu hình bot Telegram để nhận tin nhắn và kích hoạt workflow.
- **Bước 3**: Trong node **"notify-n8n.yml"**, thay thế `<your_webhook_url>` bằng URL webhook thực tế của sếp.

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: **Test Run** với dữ liệu mẫu (ví dụ: mô tả công việc từ một job posting).
- **Bước 2**: Kích hoạt workflow và **chọn "Active"**.
- **Bước 3**: Gửi mô tả công việc qua **Telegram** hoặc gọi Webhook để workflow tự động xử lý.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
1. **Cập Nhật Kinh Nghiệm Liên Tục**:
   - Sếp có thể **thêm kinh nghiệm mới** vào Google Sheets bất kỳ lúc nào, và workflow sẽ tự động sử dụng dữ liệu mới khi tạo CV/bài thư.

2. **Tích Hợp Slack/Email**:
   - Thay vì Telegram, sếp có thể **thêm node Slack/Email** để nhận thông báo khi workflow hoàn thành.

3. **Lưu Log Hoạt Động**:
   - Sếp có thể **thêm node "Set"** để lưu trữ log hoạt động vào Google Sheets hoặc Google Drive để theo dõi lịch sử.

4. **Tối Ưu Hóa AI**:
   - Nếu sếp muốn **giảm chi phí token**, có thể thay **GPT-5** bằng **GPT-4** hoặc **GPT-3.5** trong node `OpenAI Chat Model`.

5. **Tự Động Chia Sẻ CV**:
   - Sau khi hoàn thành, workflow có thể **gửi link Google Drive** hoặc **GitHub Pages** tự động qua Telegram/Email.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa CV và bài thư ứng tuyển** một cách **chuyên nghiệp, cá nhân hoá và tiết kiệm thời gian**. Không cần viết code, không cần kiến thức kỹ thuật – chỉ cần **cài đặt và kích hoạt**, sếp sẽ có **CV và bài thư ứng tuyển hoàn chỉnh** chỉ trong vài giây!

**Hãy thử ngay và ứng tuyển việc làm một cách hiệu quả hơn!** 🚀

---
:::note[CHÚ Ý]
- Để workflow **chạy 24/7**, các sếp nên **self-host n8n** trên VPS (để tránh giới hạn của n8n.cloud).
- Nếu sếp có **nhiều kinh nghiệm**, có thể **upgrade từ Google Sheets sang Vector Database** để giảm token consumption của AI.
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::