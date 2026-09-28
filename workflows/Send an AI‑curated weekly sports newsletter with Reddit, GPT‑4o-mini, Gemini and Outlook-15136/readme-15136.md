---
title: "📧 Tự Động Hoàn Thành Báo Cáo Thể Thao Tuần Kể AI: Từ Reddit Đến Email - Không Cần Code!"
description: "Workflow này tự động thu thập tin tức thể thao từ Reddit, RSS, và các nguồn khác, xử lý bằng AI (GPT-4o-mini + Gemini) để tạo ra một bản tin thể thao cá nhân hóa hàng tuần, gửi trực tiếp qua Outlook. Giúp các sếp tiết kiệm 10+ giờ/tháng và luôn cập nhật tin tức mới nhất."
slug: "tieu-dong-hoan-thanh-bao-cao-the-thao-tuan-ke-ai"
tags: [n8n, automation, no-code, ai-curated, outlook, reddit, gemini, gpt-4o-mini, email-marketing]
keywords: [tự động hóa báo cáo thể thao, workflow n8n thể thao, gửi tin tức thể thao tự động, ai curate newsletter, gemini + gpt-4o-mini, n8n với outlook]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Thể Thao Tuần Kể AI: Từ Reddit Đến Email**

### **Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất **giờ đồng hồ** mỗi tuần để:
- **Thu thập tin tức thể thao** từ nhiều nguồn khác nhau (Reddit, RSS, Twitter, blog thể thao...).
- **Lọc và tổng hợp** thông tin chất lượng, tránh tin giả hoặc nội dung không liên quan.
- **Tạo bản tin cá nhân hóa** với phong cách riêng, không bị lặp lại.
- **Gửi email tự động** cho đội ngũ hoặc khách hàng hàng tuần.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** tin tức từ Reddit, RSS và các nguồn khác.
✅ **Xử lý bằng AI** (GPT-4o-mini + Gemini) để tổng hợp, lọc và viết bản tin chất lượng cao.
✅ **Gửi email tự động** qua Outlook hàng tuần, không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc thu thập và viết bản tin.
- **Tin tức chính xác và mới nhất** từ nhiều nguồn, được AI lọc và tổng hợp.
- **Bản tin cá nhân hóa** với phong cách riêng, không bị lặp lại.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Gửi email tự động** qua Outlook, tiết kiệm thời gian gửi thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Reddit** (để thu thập tin tức từ subreddits thể thao).
2. **API Key của OpenAI** (để sử dụng GPT-4o-mini).
3. **API Key của Google Gemini** (để sử dụng AI Gemini).
4. **Tài khoản Microsoft Outlook** (để gửi email tự động).
5. **Tài khoản RSS Feed** (nếu muốn thêm nguồn RSS khác).
6. **N8n Self-hosted** (để chạy workflow 24/7 ổn định).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/15136](https://n8n.io/workflows/15136) hoặc sao chép JSON.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Create Workflow"** để lưu vào n8n của bạn.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm các node chính sau. Các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node `n8n-nodes-base.scheduleTrigger` (Động cơ lịch)**
- **Cấu hình:**
  - **Schedule:** Chọn **"Weekly"** (hàng tuần) và thời gian phù hợp (ví dụ: thứ 7 sáng 7h).
  - **Time Zone:** Đặt theo múi giờ của bạn (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Active:** Bật để workflow chạy tự động.

##### **🔹 Node `n8n-nodes-base.reddit` (Thu thập tin tức từ Reddit)**
- **Cấu hình:**
  - **Subreddits:** Nhập các subreddits thể thao như `r/nba`, `r/nfl`, `r/soccer`, `r/baseball`.
  - **Limit:** Đặt số lượng post thu thập (ví dụ: `20`).
  - **Credentials:** Đăng ký **Reddit App** để lấy `Client ID` và `Client Secret` (mã hóa).
    - **Hướng dẫn đăng ký Reddit App:**
      1. Truy cập [Reddit App](https://www.reddit.com/prefs/apps).
      2. Tạo một **New App** với loại `script`.
      3. Nhận `Client ID` và `Client Secret`, sau đó thêm vào **Credentials** trong n8n.

##### **🔹 Node `n8n-nodes-base.rssFeedRead` (Thu thập từ RSS)**
- **Cấu hình:**
  - **URL RSS:** Nhập các nguồn RSS thể thao (ví dụ: [BBC Sport RSS](https://www.bbc.com/sport/rss.xml)).
  - **Limit:** Đặt số lượng bài viết thu thập (ví dụ: `10`).

##### **🔹 Node `@n8n/n8n-nodes-langchain.agent` (Xử lý bằng AI)**
- **Cấu hình:**
  - **Model:** Chọn **GPT-4o-mini** (OpenAI) hoặc **Gemini** (Google).
  - **Prompt:** Sửa đổi để phù hợp với phong cách bản tin của bạn. Ví dụ:
    ```
    "Tôi là một AI tổng hợp tin tức thể thao. Hãy lấy các bài viết từ Reddit và RSS, lọc ra những tin tức mới nhất và quan trọng nhất về thể thao. Sau đó, viết một bản tin ngắn gọn, cá nhân hóa, và có phong cách chuyên nghiệp. Đảm bảo không có tin giả và tránh lặp lại."
    ```
  - **API Key:** Điền `API Key` của OpenAI/Gemini vào **Credentials**.

##### **🔹 Node `n8n-nodes-base.merge` (Gộp dữ liệu)**
- **Cấu hình:**
  - **Merge Strategy:** Chọn **"All"** để gộp tất cả tin tức từ Reddit và RSS.
  - **Output:** Dữ liệu sẽ được truyền đến node AI để xử lý.

##### **🔹 Node `@n8n/n8n-nodes-langchain.lmChatOpenAi` (Chat với GPT-4o-mini)**
- **Cấu hình:**
  - **Model:** Chọn **GPT-4o-mini**.
  - **Prompt:** Sửa đổi để phù hợp với yêu cầu (ví dụ: viết bản tin ngắn gọn, thêm hình ảnh, cá nhân hóa).
  - **API Key:** Điền `API Key` của OpenAI.

##### **🔹 Node `@n8n/n8n-nodes-langchain.googleGemini` (Chat với Gemini)**
- **Cấu hình:**
  - **Model:** Chọn **Gemini Pro**.
  - **Prompt:** Sử dụng cùng prompt như GPT-4o-mini.
  - **API Key:** Điền `API Key` của Google.

##### **🔹 Node `n8n-nodes-base.microsoftOutlook` (Gửi email)**
- **Cấu hình:**
  - **Credentials:** Đăng ký **Microsoft Outlook API** để lấy `Client ID` và `Client Secret`.
    - **Hướng dẫn đăng ký Outlook API:**
      1. Truy cập [Azure Portal](https://portal.azure.com/).
      2. Tạo một **Azure AD App Registration**.
      3. Cấu hình **API Permissions** cho `Mail.Send`.
      4. Nhận `Client ID` và `Client Secret`, sau đó thêm vào **Credentials** trong n8n.
  - **Email To:** Nhập địa chỉ email của người nhận (ví dụ: `team@doanhnghiep.com`).
  - **Subject:** Đặt tiêu đề email (ví dụ: `"Bản tin thể thao tuần này 🏀🏈🏉"`).
  - **Body:** Sử dụng dữ liệu từ AI (bản tin đã viết).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy **Manual Trigger** để kiểm tra workflow với dữ liệu mẫu.
- **Bật Active:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm nguồn tin tức khác:**
   - Kết nối với **Twitter API** hoặc **Google News RSS** để đa dạng hóa nguồn tin.
2. **Lưu log hoạt động:**
   - Sử dụng **Google Sheets** hoặc **Slack** để lưu lịch sử gửi email và phản hồi.
3. **Tùy chỉnh phong cách bản tin:**
   - Sửa đổi **prompt** để AI viết theo phong cách riêng (ví dụ: hài hước, chuyên nghiệp, ngắn gọn).
4. **Gửi báo cáo định kỳ:**
   - Kết hợp với **Google Analytics** hoặc **Power BI** để theo dõi mở email và tương tác.
5. **Thêm hình ảnh tự động:**
   - Sử dụng **node `n8n-nodes-base.image`** để chèn hình ảnh từ URL vào email.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc thu thập và viết bản tin thể thao thủ công. Với sự hỗ trợ của **AI (GPT-4o-mini + Gemini)**, bản tin sẽ **luôn mới nhất, chất lượng cao và cá nhân hóa**. **Gửi email tự động qua Outlook** giúp tiết kiệm thời gian và đảm bảo tin tức được chia sẻ kịp thời.

**🚀 Hãy áp dụng ngay và tự động hóa bản tin thể thao của bạn!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::