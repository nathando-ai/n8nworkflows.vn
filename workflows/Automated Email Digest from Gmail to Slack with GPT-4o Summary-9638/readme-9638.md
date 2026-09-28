---
title: "📧 Tự Động Hóa Báo Cáo Email Hàng Ngày Từ Gmail Sang Slack Với Tóm Tắt AI (GPT-4o) - Giảm 90% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa lấy tất cả email ngày hôm qua từ Gmail, phân tích bằng GPT-4o-mini, và gửi tóm tắt định dạng chuyên nghiệp sang Slack hàng ngày. Giúp các sếp tiết kiệm 2+ giờ/ngày và giảm thiểu lỗi trong việc theo dõi email."
slug: "tieu-dong-hoa-bao-cao-email-gmail-slack-gpt-4o"
tags: [n8n, automation, gmail, slack, ai, gpt-4o, no-code, email-summary, workflow-daily]
keywords: [tự động hóa email gmail slack, báo cáo email hàng ngày, gpt-4o tóm tắt email, workflow n8n tự động, giảm thời gian làm thủ công email]
---

# 🚀 **Tự Động Hóa Báo Cáo Email Hàng Ngày Từ Gmail Sang Slack Với Tóm Tắt AI (GPT-4o)**

### **Giải pháp cho các sếp bị "chìm" trong email hàng ngày**
Hàng ngày, các sếp phải mất **2-3 giờ** để đọc, phân loại và tóm tắt email từ Gmail. Kết quả? **Thông tin quan trọng bị bỏ qua**, quyết định bị chậm trễ, và năng suất giảm sút. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
- **Lấy tất cả email ngày hôm qua** từ Gmail (từ 00:00 đến 24:00).
- **Phân tích và tóm tắt** bằng **GPT-4o-mini** (mô hình AI hiệu quả, chi phí thấp).
- **Gửi báo cáo định dạng chuyên nghiệp** sang Slack hàng ngày (lúc 8h sáng).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2-3 giờ/ngày** để tập trung vào công việc chiến lược.
- **Tóm tắt email chính xác** bằng AI, giảm thiểu lỗi bỏ qua thông tin quan trọng.
- **Báo cáo định dạng chuyên nghiệp** được gửi tự động sang Slack, dễ theo dõi và chia sẻ.
- **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.
- **Kết hợp với Slack** để đồng bộ thông tin toàn bộ team.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n):
   - Các sếp phải **cho phép n8n đọc email** trong cài đặt Gmail (quyền `Read-only`).
   - [Hướng dẫn cấp quyền Gmail cho n8n](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.gmail.html#authentication).

2. **Tài khoản Slack**:
   - **Bot Slack** được tạo và cấp quyền `post` vào channel mục tiêu (ví dụ: `#general`).
   - [Hướng dẫn tạo bot Slack](https://api.slack.com/apps).

3. **API Key OpenRouter** (để sử dụng GPT-4o-mini):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - **Model khuyến nghị**: `openai/gpt-4o-mini` (tiết kiệm chi phí so với GPT-4).

4. **VPS n8n** (nếu tự host):
   - Đã cài đặt và chạy n8n trên máy chủ 24/7 (không dùng phiên bản cloud miễn phí).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9638) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và dán vào **Create Workflow** → **Import JSON**.

:::note[Lưu ý]
- **Không sử dụng phiên bản n8n cloud** nếu muốn chạy 24/7 (do giới hạn thời gian hoạt động).
- **Không cần chỉnh sửa code** trong node `Format for Slack` (nếu không muốn tự code).
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

| **Node**                          | **Cần chỉnh gì?**                                                                 | **Lưu ý**                                                                 |
|-----------------------------------|----------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Schedule Trigger**              | Thiết lập lịch chạy **lúc 8h sáng** (hoặc thời gian phù hợp).                   | Nếu muốn chạy vào giờ khác, chỉnh `cron` trong node này.                |
| **Gmail - Get Yesterday's Emails** | Chọn **credentials Gmail** đã tạo trước đó.                                      | Đảm bảo quyền `Read-only` đã được cấp.                                  |
| **AI Agent - Analyze Emails**     | Chọn **credentials OpenRouter** và nhập **API Key**.                           | Model mặc định là `gpt-4o-mini` (không cần chỉnh).                       |
| **Structured Output Parser**      | **Không cần chỉnh** (n8n tự động phân tích kết quả từ AI).                    | Nếu muốn thay đổi cấu trúc output, chỉnh trong node `Format for Slack`.  |
| **Format for Slack**              | **Chỉnh channel Slack** và nội dung báo cáo (nếu muốn cá nhân hóa).            | Ví dụ: Thêm logo công ty, thay đổi định dạng thời gian.                  |
| **Slack - Send Summary**          | Chọn **credentials Slack** và channel mục tiêu (ví dụ: `#daily-summary`).       | Đảm bảo bot Slack có quyền `post` vào channel đó.                       |
| **If (node điều kiện)**           | **Không cần chỉnh** (n8n tự động kiểm tra có email không).                   | Nếu muốn thay đổi logic, chỉnh trong node này.                          |

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Chạy node **Gmail - Get Yesterday's Emails** để kiểm tra lấy được email không.
   - Chạy node **AI Agent** để xem AI tóm tắt như thế nào.
   - Chạy node **Slack - Send Summary** để kiểm tra báo cáo trên Slack.

2. **Bật Active workflow**:
   - Sau khi test thành công, **bật switch `Active`** ở góc trên bên phải.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm logo công ty vào báo cáo Slack**:
   - Trong node **Format for Slack**, thêm code để chèn ảnh:
     ```javascript
     const logoUrl = "https://example.com/logo.png";
     return {
       blocks: [
         { type: "section", text: { type: "mrkdwn", text: "*Daily Email Digest*" } },
         { type: "image", image_url: logoUrl, alt_text: "Logo" },
         // ... phần nội dung tóm tắt
       ]
     };
     ```

2. **Lưu log email vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Gmail** để lưu tất cả email vào bảng tính.
   - **Ưu điểm**: Dễ theo dõi lịch sử và phân tích dài hạn.

3. **Gửi báo cáo qua Email (nếu cần)**:
   - Thêm node **Email** (ví dụ: Gmail Send) sau node **Format for Slack** để gửi báo cáo qua email cá nhân.

4. **Tùy chỉnh prompt AI**:
   - Trong node **OpenRouter Chat Model**, chỉnh **prompt** để AI tóm tắt theo phong cách riêng:
     ```json
     {
       "prompt": "Tóm tắt email ngày hôm qua theo định dạng sau:\n1. **Tóm tắt ngắn (1 câu)**\n2. **Điểm quan trọng** (danh sách bullet)\n3. **Hành động cần thực hiện** (nếu có)\n\n**Yêu cầu:** Không bao gồm email spam hoặc không liên quan."
     }
     ```

5. **Chỉnh lịch chạy theo giờ làm việc**:
   - Nếu công ty làm việc từ 9h-17h, chỉnh **Schedule Trigger** để chạy lúc 9h sáng.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc làm thủ công email hàng ngày, đồng thời **tăng cường hiệu quả** bằng AI. **Chỉ cần 10 phút setup**, các sếp sẽ nhận được **báo cáo chuyên nghiệp** mỗi sáng trên Slack.

👉 **Hành động ngay**:
1. **Import workflow** và cấu hình credentials.
2. **Test run** để đảm bảo hoạt động.
3. **Bật Active** và **quên đi việc làm thủ công email**!

**Nếu có vấn đề**, các sếp có thể tham khảo:
- [Hỗ trợ n8n Việt Nam](https://community.n8n.io/)
- [Tài liệu Gmail n8n](https://docs.n8n.io/integrations/built-in/n8n-nodes-base.gmail.html)
- [Tài liệu Slack n8n](https://docs.n8n.io/integrations/built-in/n8n-nodes-base.slack.html)

---
**#TựĐộngHóa #N8N #AI #Slack #Gmail #WorkflowHàngNgày**