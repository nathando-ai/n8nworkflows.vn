---
title: "📚 **Tự Động Hóa Tóm Tắt Sách + Liên Kết Affiliate Amazon Với GPT-4o & Google APIs - Khai Thác AI Cho Marketing Sách**"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động tóm tắt sách, phân tích đánh giá, và gửi email cá nhân hóa với liên kết Affiliate Amazon - tiết kiệm thời gian lên đến 80% cho công việc nghiên cứu sách."
slug: "tieu-dong-hoa-tom-tat-sach-gpt-4o-google-apis"
tags: [n8n, automation, ai-chatbot, marketing-digital, affiliate-marketing, google-apis]
keywords: [n8n workflow tự động hóa sách, GPT-4o tóm tắt sách, affiliate marketing sách, tự động hóa nghiên cứu sách, AI cho marketing, Google Books API]
---

# 🚀 **Tự Động Hóa Tóm Tắt Sách + Affiliate Amazon: AI Book Advisor Cho Các Sếp Marketing**

## **Nỗi Đau Của Các Sếp Khi Nghiên Cứu Sách**
Các sếp marketing, blogger, hoặc người bán sách thường phải mất **giờ đồng hồ** để:
- Tìm kiếm thông tin chi tiết về sách (tóm tắt, đánh giá, tác giả).
- Phân tích nội dung từ nhiều nguồn khác nhau.
- Tạo email cá nhân hóa giới thiệu sách cho khách hàng.
- Theo dõi lịch sử nghiên cứu để tối ưu hóa chiến dịch.

**Workflow này giải quyết tất cả bằng AI + tự động hóa 100% không cần code!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** – Không cần tìm kiếm thủ công trên Google Books, Amazon, hoặc các trang review.
✅ **Tóm tắt sách chuyên nghiệp** – GPT-4o phân tích nội dung và đánh giá để tạo ra **tóm tắt ngắn gọn, chính xác**.
✅ **Liên kết Affiliate tự động** – Email gửi đi luôn có **liên kết Amazon Affiliate**, giúp tăng doanh thu từ giới thiệu sách.
✅ **Lưu lịch sử nghiên cứu** – Dữ liệu được ghi vào **Google Sheets**, giúp theo dõi và phân tích hiệu quả marketing.
✅ **Cá nhân hóa email** – Mỗi email đều có **nội dung độc quyền** dựa trên yêu cầu của khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - **OpenAI API Key** (để sử dụng GPT-4o).
   - **Google Custom Search API Key** (để tìm kiếm đánh giá sách).
   - **Gmail OAuth 2.0** (để gửi email tự động).
   - **Google Sheets OAuth 2.0** (để lưu log).
   - **Amazon Affiliate Tag** (ví dụ: `assoc_amazon_vn_00`).
2. **Google Sheets**:
   - Tạo một bảng với các cột: `date`, `book_title`, `author`, `ai_comment`, `user_email`.
3. **Form Trigger** (nếu muốn người dùng nhập yêu cầu qua form).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11347](https://n8n.io/workflows/11347) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **14 node** quan trọng, các sếp cần chú ý:

##### **🔹 Node "Workflow Configuration" (Set)**
- Điền **Amazon Affiliate Tag** vào biến `$amazonAffiliateTag`.
- Ví dụ: `assoc_amazon_vn_00` (mã tag của bạn trên Amazon Associates).

##### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- Chọn **model = gpt-4o** (đã cấu hình sẵn).
- Đảm bảo **OpenAI API Key** đã được thêm vào **credentials** (`openAiApi`).

##### **🔹 Node "Google Sheets" (googleSheets)**
- Chọn **Google Sheets OAuth 2.0** trong **credentials**.
- Điền **Sheet Name** và **Range** (ví dụ: `Sheet1!A1:E100`).

##### **🔹 Node "Build HTML Email" (Code)**
- Nội dung HTML đã được cấu hình sẵn, **không cần chỉnh sửa** trừ khi muốn thay đổi layout.
- Các biến như `$bookTitle`, `$aiSummary`, `$amazonLink` sẽ tự động được thay thế.

##### **🔹 Node "Search Book on Google Books API" (httpRequest)**
- Đảm bảo **Google Custom Search API Key** đã được thêm vào **credentials**.
- Cấu hình **URL** như sau:
  ```
  https://www.googleapis.com/customsearch/v1?q={$bookTitle}&searchType=book&key={$googleCustomSearchApiKey}
  ```

##### **🔹 Node "Book Curator AI Agent" (agent)**
- **Prompt** đã được tối ưu hóa để phân tích sách, nhưng các sếp có thể **cập nhật** trong **Structured Output Parser** nếu muốn thay đổi logic.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chọn **Run Workflow** và nhập một **tên sách** vào form để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả ngay khi có yêu cầu mới.
2. **Lưu Log Chi Tiết**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu toàn bộ lịch sử giao dịch.
3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để gửi **báo cáo tổng hợp** về sách đã nghiên cứu hàng tuần.
4. **Cải Thiện Prompt AI**:
   - Nếu muốn **tóm tắt sách chi tiết hơn**, cập nhật **Structured Output Parser** để yêu cầu GPT-4o trả về **các điểm nổi bật** cụ thể.

---

### 📌 **Kết Luận: AI Book Advisor - Giải Pháp Marketing Sách Hiệu Quả**
Workflow này không chỉ **tự động hóa tìm kiếm và tóm tắt sách**, mà còn **tăng doanh thu** thông qua liên kết Affiliate và **cải thiện trải nghiệm khách hàng** với email cá nhân hóa.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 cuốn sách** để đảm bảo hoạt động.
3. **Bật Active** và bắt đầu **tự động hóa nghiên cứu sách** của mình!

👉 **Xem workflow gốc**: [n8n.io/workflows/11347](https://n8n.io/workflows/11347)
👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** để tự host và tránh giới hạn phiên bản cloud!

---
**#TựĐộngHóaMarketing #AIChoSách #AffiliateAutomation #n8nVietnam**