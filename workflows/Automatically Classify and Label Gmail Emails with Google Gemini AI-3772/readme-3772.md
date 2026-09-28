---
title: "🤖 **Tự Động Phân Loại & Nhãn Email Gmail Bằng AI Gemini - Giảm 90% Thời Gian Quản Lý Email**"
description: "Workflow tự động phân loại và gán nhãn cho email Gmail bằng Google Gemini AI, tiết kiệm thời gian, giảm sai sót và tự động hóa quản lý email 24/7. Phù hợp cho doanh nghiệp, giáo viên, hoặc bất kỳ ai phải xử lý hàng trăm email hàng ngày."
slug: "tu-dong-phan-loai-nhan-email-gmail-bang-ai-gemini"
tags: [n8n, automation, ai, google-gemini, gmail, no-code, self-hosted]
keywords: [tự động hóa email gmail, phân loại email bằng ai, google gemini n8n, giảm thời gian quản lý email, workflow n8n ai, tự động gán nhãn email]
---

# 🚀 **Tự Động Phân Loại & Nhãn Email Gmail Bằng AI Gemini - Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải mất **từ 1-2 giờ** để:
- Lọc và phân loại email từ hàng trăm tin nhắn trong Gmail.
- Gán nhãn thủ công cho từng loại email (quản lý, khiếu nại, hợp đồng, quảng cáo...).
- Lo lắng bỏ lỡ email quan trọng trong luồng tin nhấn chìm.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi AI có thể làm tất cả đó **một cách chính xác và tự động**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** quản lý email hàng ngày.
- **Chính xác 100%** nhờ AI phân loại dựa trên ngữ cảnh và từ khóa.
- **Tự động gán nhãn** theo danh mục sẵn có (quản lý, khiếu nại, hợp đồng, ưu tiên cao...).
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa** theo nhu cầu của doanh nghiệp (thêm/loại nhãn tùy ý).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để kết nối với API Gmail).
2. **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
3. **Tài khoản Groq API** (tùy chọn, nếu muốn sử dụng mô hình Groq làm backup).
4. **Những nhãn Gmail** đã được tạo sẵn (ví dụ: `+Quản lý`, `+Khiếu nại`, `+Hợp đồng`, `+Ưu tiên cao`).
5. **Cài đặt n8n Self-hosted** (khuyến cáo sử dụng VPS để workflow hoạt động liên tục).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/3772) (hoặc sao chép JSON từ canvas).
- Vào **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này bao gồm **9 node chính**, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu Hình Gmail OAuth2 (Node Gmail Trigger & Gmail Actions)**
- **Bước 1:** Vào **Credentials** → Tạo mới **Gmail OAuth2**.
  - Đăng nhập tài khoản Gmail cần kết nối.
  - Cho phép quyền truy cập vào **Gmail API**.
- **Bước 2:** Đặt tên credentials là `gmailOAuth2` (để khớp với workflow).

##### **B. Cấu Hình Google Gemini AI**
- **Bước 1:** Vào **Credentials** → Tạo mới **Google Palm API** (hoặc **Google Gemini API** nếu mới nhất).
  - Đăng ký API Key tại [Google AI Studio](https://makersuite.google.com/).
  - Chọn mô hình `gemini-1.5-pro` (hoặc mô hình khác phù hợp).
- **Bước 2:** Đặt tên credentials là `googlePalmApi`.

##### **C. Cấu Hình Agent & Text Classifier**
- **Node "AI Agent"** và **"Classification Agent"** sẽ tự động phân loại email.
- **Yêu cầu:** Các sếp cần **cập nhật danh sách nhãn** trong **Sticky Note** (node `StickyNote`).
  - Mở node `StickyNote` → Sửa nội dung như sau:
    ```json
    {
      "categories": [
        {
          "name": "Quản lý",
          "description": "Email liên quan đến quản lý, kế hoạch, báo cáo. Từ khóa: 'báo cáo', 'kế hoạch', 'quản lý', 'meeting'"
        },
        {
          "name": "Khiếu nại",
          "description": "Email khiếu nại khách hàng. Từ khóa: 'khiếu nại', 'phàn nàn', 'hỗ trợ', 'sửa chữa'"
        },
        {
          "name": "Hợp đồng",
          "description": "Email liên quan đến hợp đồng, ký kết. Từ khóa: 'hợp đồng', 'ký kết', 'điều khoản', 'thuê bao'"
        },
        {
          "name": "Ưu tiên cao",
          "description": "Email cần xử lý ngay. Từ khóa: 'ngay lập tức', 'ưu tiên', 'khẩn cấp'"
        }
      ]
    }
    ```
  - **Lưu ý:** Các từ khóa phải **phù hợp với ngữ cảnh email** của doanh nghiệp.

##### **D. Cấu Hình Nhãn Gmail**
- Các sếp cần **tạo nhãn Gmail** trước khi chạy workflow:
  - Mở Gmail → Nhấn **"Nhãn"** (icon nhãn) → **"Tạo nhãn mới"**.
  - Tạo các nhãn với **ký tự "+"** ở đầu (ví dụ: `+Quản lý`, `+Khiếu nại`).
  - **Chọn màu sắc** để dễ phân biệt (khuyến cáo sử dụng màu khác nhau cho từng loại).

##### **E. Cấu Hình Node "Add Label"**
- Mở từng node `Add Label` (ví dụ: `Add Label Promotion`, `Add Label (KS Work Related)`).
- Trong trường **"Label Names or IDs"**, chọn **nhãn Gmail** tương ứng với danh mục trong `StickyNote`.
  - Ví dụ: Nếu danh mục là `Quản lý`, chọn nhãn `+Quản lý`.

##### **F. Cấu Hình Mô Hình Groq (Tùy Chọn)**
- Nếu muốn sử dụng mô hình **Groq** làm backup, các sếp cần:
  - Tạo **Groq API Key** tại [Groq Dashboard](https://console.groq.com/).
  - Cấu hình node `Groq Chat Model` với mô hình `meta-llama/llama-4-scout-17b-16e-instruct`.

---
#### **3. Kích Hoạt Workflow ⚡️**
- **Bước 1:** Nhấn **"Test Run"** với một email mẫu để kiểm tra phân loại.
- **Bước 2:** Nếu kết quả đúng, chuyển workflow sang **Active**.
- **Bước 3:** Kiểm tra email trong Gmail để xác nhận nhãn đã được gán tự động.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram** để thông báo email mới được phân loại.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi tin nhắn cảnh báo.
2. **Lưu log phân loại** vào Google Sheets hoặc Notion để theo dõi.
   - Sử dụng node **Google Sheets** hoặc **Notion** để ghi lại lịch sử phân loại.
3. **Tự động chuyển email ưu tiên cao** vào folder riêng.
   - Sử dụng node **Gmail Filter** để chuyển email nhãn `+Ưu tiên cao` vào folder "Khẩn cấp".
4. **Cập nhật từ khóa định kỳ** để AI phân loại chính xác hơn.
   - Mở node `StickyNote` và cập nhật danh sách từ khóa theo nhu cầu mới.
5. **Sử dụng nhiều mô hình AI** (Gemini + Groq) để tăng độ chính xác.
   - Cấu hình node `Groq Chat Model` làm mô hình phụ trợ.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại trong quản lý email. Với **AI Gemini và tự động hóa n8n**, các sếp có thể:
✅ **Phân loại email chính xác** mà không cần can thiệp.
✅ **Tự động gán nhãn** theo danh mục sẵn có.
✅ **Hoạt động 24/7** mà không cần nghỉ ngơi.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (khuyến cáo sử dụng [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Chạy thử** và xem AI làm việc như thế nào!

**💡 Lưu ý:** Nếu gặp khó khăn, các sếp có thể tham khảo [hướng dẫn chi tiết của tác giả](https://n8n.io/workflows/3772) hoặc liên hệ cộng đồng n8n trên [Discord](https://discord.gg/n8n).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với tự động hóa email!** 🚀