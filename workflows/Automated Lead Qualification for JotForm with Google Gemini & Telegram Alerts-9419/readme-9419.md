---
title: "🚀 Tự Động Hóa Xác Minh Lead Tiềm Năng từ JotForm với Google Gemini & Thông Báo Telegram (AI + No-Code)"
description: "Workflow tự động phân loại lead từ JotForm thành Hot Lead, Cold Lead hoặc Spam bằng trí tuệ nhân tạo Google Gemini, sau đó gửi thông báo Telegram cho lead chất lượng cao và tự động xóa spam. Giúp doanh nghiệp tiết kiệm thời gian và tập trung vào khách hàng tiềm năng thực sự."
slug: "tu-dong-hoa-xac-minh-lead-jotform-google-gemini-telegram"
tags: [n8n, automation, no-code, AI, JotForm, Google Gemini, Telegram, CRM, lead qualification]
keywords: [tự động hóa lead JotForm, phân loại lead bằng AI, Google Gemini n8n, Telegram alert lead, workflow tự động CRM, xóa spam JotForm]
---

# 🚀 **Tự Động Hóa Xác Minh Lead Tiềm Năng từ JotForm với Google Gemini & Telegram**

## **Giới Thiệu**
Các sếp đang phải mất thời gian quét hàng chục, thậm chí hàng trăm lead từ form JotForm mỗi ngày? Bị chìm trong luồng thông tin với những lead không liên quan, spam hoặc chỉ đơn giản là "cold lead" không có giá trị? **Workflow này sẽ giải quyết vấn đề đó bằng trí tuệ nhân tạo (AI) và tự động hóa hoàn toàn!**

Dựa trên công nghệ **Google Gemini** (mô hình AI tiên tiến của Google), workflow sẽ **tự động phân loại lead** thành ba loại:
- **Hot Lead (Lead chất lượng cao)**: Gửi thông báo Telegram ngay lập tức và đánh dấu trong JotForm.
- **Cold Lead (Lead không liên quan)**: Bỏ qua mà không cần can thiệp.
- **Spam/Garbage**: Xóa tự động khỏi JotForm để không làm tắc nghẽn dữ liệu.

Kết quả? **Tiết kiệm 80% thời gian xử lý lead**, tập trung vào khách hàng thực sự quan trọng, và **không bao giờ bỏ lỡ lead chất lượng** nhờ thông báo Telegram thời gian thực.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần quét thủ công hàng trăm lead mỗi ngày.
✅ **Chính xác cao**: AI phân loại lead với độ chính xác >90% (cấu hình được tùy chỉnh).
✅ **Tích cực hành động**: Lead chất lượng được thông báo ngay qua Telegram và đánh dấu trong JotForm.
✅ **Giảm spam**: Xóa tự động tất cả lead không liên quan hoặc spam.
✅ **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản JotForm**:
   - Form đã được tạo và **cấu hình Webhook** để n8n nhận dữ liệu.
   - **API Key** của JotForm (để flag và xóa lead).
   - **ID của Form** (để n8n biết phải lấy lead từ form nào).

2. **Tài khoản Google Cloud (để sử dụng Google Gemini)**:
   - **API Key** của Google Cloud AI (mô hình Gemini).
   - **Project ID** và **Location** (ví dụ: `us-central1`).

3. **Tài khoản Telegram**:
   - **Chat ID** của bot Telegram (để gửi thông báo lead chất lượng).
   - **Token API** của bot Telegram (tạo bot trên [@BotFather](https://t.me/BotFather)).

4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9419](https://n8n.io/workflows/9419) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **11 node**, nhưng có **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Node "Trigger: When Form Submitted" (JotForm Trigger)**
- **Cấu hình**:
  - **Form ID**: Nhập ID của form JotForm bạn muốn theo dõi.
  - **Webhook URL**: Được tự động tạo khi import workflow (không cần thay đổi).
  - **Credentials**: Chọn hoặc tạo mới **JotForm API Credentials** (đăng ký tại [JotForm Developer Portal](https://developer.jotform.com/)).

##### **B. Node "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Cấu hình**:
  - **API Key**: Nhập **API Key** từ Google Cloud AI.
  - **Project ID** và **Location**: Nhập thông tin từ Google Cloud Console.
  - **Prompt**: Workflow đã cấu hình sẵn prompt phân loại lead. **Không cần chỉnh** trừ khi muốn thay đổi logic phân loại.

##### **C. Node "Get Chat ID (One-Time Setup)" (TelegramTrigger)**
- **Lưu ý quan trọng**:
  - Đây là **cấu hình một lần** để lấy **Chat ID** của bot Telegram.
  - **Cách thực hiện**:
    1. Nhập **Token API** của bot Telegram (từ @BotFather).
    2. Gửi tin nhắn **`/start`** đến bot (trên Telegram).
    3. Workflow sẽ tự động trả về **Chat ID** của bạn. **Copy Chat ID này** và dán vào node **"Notify Hot Lead"** (Telegram node).

##### **D. Node "Flag in JotForm" & "Delete Spam Submission" (HTTP Request)**
- **Cấu hình chung**:
  - **URL**: Được tự động tạo từ API JotForm.
  - **Headers**: Nhập **Authorization: Bearer {API_KEY_JOTFORM}**.
  - **Body**: Workflow đã cấu hình sẵn. **Không cần chỉnh** trừ khi muốn thay đổi logic.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một lead mẫu:
   - Tạo một lead test trên JotForm và kiểm tra workflow có hoạt động như mong đợi không.
   - Kiểm tra:
     - Lead **Hot** có được gửi Telegram không?
     - Lead **Spam** có bị xóa không?
     - Lead **Cold** có bị bỏ qua không?

2. **Bật Active workflow**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt cho Google Gemini**:
   - Nếu muốn phân loại lead theo logic riêng, chỉnh sửa **Prompt** trong node `Google Gemini Chat Model` theo cú pháp JSON:
     ```json
     {
       "instruction": "Phân loại lead theo tiêu chí sau:
       - Hot Lead: Giới thiệu về dịch vụ AI/automation, đề xuất hợp tác, hoặc yêu cầu demo.
       - Cold Lead: Yêu cầu việc làm, thông tin sản phẩm không liên quan, hoặc tin nhắn không cụ thể.
       - Spam: Tin nhắn rác, bot, hoặc dữ liệu không hợp lệ.
       Trả về kết quả dưới dạng JSON: {'lead_type': 'Hot|Cold|Spam', 'reason': 'Lý do phân loại'}."
     }
     ```

2. **Gửi thông báo đến Slack thay vì Telegram**:
   - Thay thế node `Telegram` bằng node `Slack` và cấu hình tương tự.

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử phân loại lead cho báo cáo.

4. **Kết hợp với CRM (HubSpot, Salesforce)**:
   - Thay thế node `Flag in JotForm` bằng API của CRM để tự động cập nhật lead vào hệ thống.

5. **Bộ lọc lead theo từ khóa**:
   - Sử dụng node **Set** để thêm logic bộ lọc trước khi gửi đến AI (ví dụ: bỏ qua lead có từ khóa "spam" hoặc "test").

---

### 📌 **Kết luận**
Workflow này không chỉ **tự động hóa việc phân loại lead**, mà còn **giúp các sếp tập trung vào những lead thực sự có giá trị**. Với **Google Gemini**, độ chính xác cao hơn so với các giải pháp truyền thống, và với **Telegram Alerts**, không bao giờ bỏ lỡ lead chất lượng.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với lead mẫu** và bật workflow.

**Công việc của bạn sẽ trở nên đơn giản hơn bao giờ hết!** 🚀

---
**🔗 [Xem workflow gốc trên n8n.io](https://n8n.io/workflows/9419)**
**💬 Có thắc mắc? Để lại comment bên dưới!**