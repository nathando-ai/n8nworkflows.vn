---
title: "🌟 **Tự Động Hóa Email Tóm Tắt Tin Tức AI Hàng Ngày - Google News + GPT-4o-mini + Gmail + Sheets**"
description: "Giải pháp tự động hóa hoàn toàn không cần code để nhận email tổng hợp tin tức cá nhân hóa hàng ngày từ Google News, được tóm tắt bởi GPT-4o-mini và gửi tự động qua Gmail. Tiết kiệm 2+ giờ mỗi ngày cho các sếp và chuyên gia cần cập nhật thông tin nhanh chóng."
slug: "tieu-dong-hoa-email-tom-tat-tin-tuc-ai-hang-ngay"
tags: [n8n, automation, no-code, ai-summarization, google-news, gmail-automation, google-sheets]
keywords: [tự động hóa email tin tức hàng ngày, gpt-4o-mini tổng hợp tin tức, n8n workflow google news, tự động hóa tin tức bằng AI, email tổng hợp tin tức cá nhân hóa]
---

# 🚀 **Tự Động Hóa Email Tóm Tắt Tin Tức AI Hàng Ngày - Không Cần Code!**

### **🔥 Bạn đã bao giờ mệt mỏi vì phải thủ công:**
- **Lọc tin tức** từ Google News theo nhiều chủ đề khác nhau?
- **Tóm tắt hàng chục bài báo** mỗi ngày để đọc nhanh?
- **Gửi email tổng hợp** cho đồng nghiệp hoặc bản thân mỗi sáng?

**Workflow này giải quyết tất cả!** Hàng ngày lúc 7h sáng, hệ thống sẽ tự động:
✅ **Lấy tin tức mới nhất** từ Google News theo các chủ đề bạn quan tâm (được quản lý trên Google Sheets).
✅ **Tóm tắt bằng AI** (GPT-4o-mini) mỗi bài báo thành **3 câu ngắn gọn**, không cần đọc toàn văn.
✅ **Gửi email tổng hợp** với định dạng HTML đẹp mắt, phân chủ đề rõ ràng.
✅ **Ghi log hoạt động** trên Google Sheets để theo dõi hiệu suất.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2+ giờ mỗi ngày** so với cách thủ công.
- **Tin tức được tóm tắt chính xác** bởi AI, không bỏ sót chi tiết quan trọng.
- **Cá nhân hóa hoàn toàn** theo sở thích (chủ đề, số lượng bài báo, thời gian gửi).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dữ liệu theo dõi** trên Google Sheets để đánh giá hiệu suất.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để quản lý chủ đề và log hoạt động).
2. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini tóm tắt tin tức).
3. **Tài khoản Gmail** (để gửi email tổng hợp).
4. **API Key OpenAI** (trong n8n, tìm tại [OpenAI API Keys](https://platform.openai.com/account/api-keys)).
5. **Google Sheets ID** (tham khảo cách lấy [ở đây](https://support.google.com/docs/answer/10701260)).
6. **Email nhận email tổng hợp** (điền vào node Gmail).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15753](https://n8n.io/workflows/15753) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15753) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **📌 Node 2: Google Sheets — Read Topics**
- **Thao tác:**
  - Click vào **Credentials** → **Add New Credential** → Chọn **Google Sheets OAuth2**.
  - Điền **Google Sheets ID** vào trường `sheetId` (thay thế `YOUR_GOOGLE_SHEET_ID`).
  - Chọn **Tab "Topics"** (đã tạo sẵn trong Google Sheets).
- **Cấu trúc Google Sheets:**
  | Topic       | Search Keywords       | Max Articles | Active |
  |-------------|-----------------------|--------------|--------|
  | Tin tức Tech| "AI + blockchain"     | 5            | TRUE   |
  | Kinh tế Việt| "chính sách kinh tế" | 3            | TRUE   |

##### **📌 Node 9: OpenAI — GPT-4o-mini Model**
- **Thao tác:**
  - Click vào **Credentials** → **Add New Credential** → Chọn **OpenAI**.
  - Điền **API Key** từ OpenAI vào trường `apiKey`.
  - Chọn **Model: gpt-4o-mini** (đã được cài đặt sẵn trong workflow).

##### **📌 Node 11: Gmail — Send Digest Email**
- **Thao tác:**
  - Click vào **Credentials** → **Add New Credential** → Chọn **Gmail OAuth2**.
  - Điền **Email nhận** vào trường `to` (thay thế `YOUR_EMAIL_ADDRESS`).
  - **Lưu ý:** Email này phải là tài khoản Gmail đã kết nối với n8n.

##### **📌 Node 12: Google Sheets — Log Digest**
- **Thao tác:**
  - Click vào **Credentials** → **Add New Credential** → Chọn **Google Sheets OAuth2** (giống Node 2).
  - Điền **Google Sheets ID** vào trường `sheetId` (thay thế `YOUR_LOG_SHEET_ID`).
  - Chọn **Tab "Digest Log"** (đã tạo sẵn trong Google Sheets).
- **Cấu trúc Google Sheets (Tab "Digest Log"):**
  | Date       | Topics Count | Articles Found | Email Sent | Sent At          |
  |------------|--------------|----------------|------------|------------------|
  | 2024-05-20 | 3            | 12             | TRUE       | 07:05:22 AM      |

##### **📌 Node 1: Schedule — Every Day 7AM**
- **Lưu ý:** Nếu muốn thay đổi thời gian, chỉnh **cron expression** từ `0 7 * * *` thành:
  - `0 8 * * *` (8h sáng).
  - `0 6 * * *` (6h sáng).

---

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chọn **Run Workflow** để kiểm tra với dữ liệu mẫu.
- **Active:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng ngày.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack/Telegram Notifications:**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi email tổng hợp được gửi thành công.
   - **Cách làm:** Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau node **Gmail — Send Digest Email**.

2. **Lưu Log Chi tiết hơn:**
   - Thêm cột **Error Log** vào tab **Digest Log** để ghi lại lỗi nếu có (ví dụ: không lấy được tin tức cho chủ đề nào).

3. **Tự động dừng chủ đề không hoạt động:**
   - Sử dụng node **Code** để kiểm tra nếu một chủ đề liên tục không có bài báo trong 3 ngày, tự động **đặt Active = FALSE**.

4. **Kết hợp với Notion/Google Docs:**
   - Thay vì gửi email, lưu tin tức tổng hợp vào **Notion** hoặc **Google Docs** để dễ dàng chia sẻ với team.

5. **Tùy chỉnh định dạng email:**
   - Sử dụng **node Code** để thay đổi màu sắc, logo, hoặc thêm footer vào email HTML.
:::

---
### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp, nhà đầu tư, hoặc chuyên gia cần cập nhật tin tức nhanh chóng mà không tốn thời gian. Với **AI tóm tắt tin tức**, **tự động hóa hoàn toàn**, và **dữ liệu theo dõi chi tiết**, bạn sẽ **tiết kiệm thời gian, tăng hiệu suất làm việc**, và **không bỏ lỡ bất kỳ tin tức quan trọng nào**.

**👉 Hãy áp dụng ngay và bắt đầu mỗi ngày với tin tức được tổng hợp sẵn!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::