---
title: "🚀 Tự Động Hoàn Thành Email Làm Nóng (Cold Email Icebreakers) Từ Tìm Kiếm Doanh Nghiệp Cục Bộ Với GPT-4 & Dumpling AI"
description: "Workflow tự động hóa tìm kiếm doanh nghiệp địa phương, trích xuất email và website, tạo email làm nóng cá nhân hóa bằng GPT-4, và quản lý leads trên Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng trong lead generation."
slug: "tieu-dong-hoan-thanh-email-lam-nong-tu-tim-kiem-doanh-nghiep-cuc-bo"
tags: [n8n, automation, lead-generation, ai-gpt4, dumpling-ai, google-sheets]
keywords: [n8n workflow tự động hóa, cold email icebreaker, tìm kiếm doanh nghiệp địa phương, GPT-4 tự động viết email, lead generation tự động]
---

# 🚀 **Tự Động Hoàn Thành Email Làm Nóng (Cold Email Icebreakers) Từ Tìm Kiếm Doanh Nghiệp Cục Bộ**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp Trong Lead Generation**
Bạn đã bao giờ phải:
- **Tìm kiếm thủ công** hàng trăm doanh nghiệp địa phương để tìm email liên hệ?
- **Viết email làm nóng** một cách lặp đi lặp lại, mất nhiều thời gian mà hiệu quả còn thấp?
- **Quản lý leads** trên nhiều bảng tính khác nhau, khó theo dõi và cập nhật?

Workflow này **tự động hóa toàn bộ quy trình** từ tìm kiếm doanh nghiệp đến viết email cá nhân hóa, giúp bạn **tiết kiệm 10+ giờ/tháng** và tăng hiệu quả lead generation lên **300%**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tìm kiếm và viết email tự động, chỉ cần nhập từ khóa.
- **Email cá nhân hóa**: GPT-4 tự động viết email làm nóng dựa trên thông tin doanh nghiệp.
- **Quản lý leads hiệu quả**: Lưu tất cả dữ liệu vào Google Sheets và tích hợp với Instantly.ai (nếu cần).
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Dumpling AI** (để tìm kiếm doanh nghiệp trên Google Maps).
2. **API Key OpenAI** (để sử dụng GPT-4 viết email).
3. **Google Sheets OAuth 2.0** (để lưu log kết quả).
4. **Tài khoản Instantly.ai** (tùy chọn, để thêm leads vào chiến dịch).
5. **Credentials HTTP Header Auth** (nếu sử dụng API của Dumpling AI hoặc Instantly.ai).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6156](https://n8n.io/workflows/6156) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **9 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Form Trigger (Bắt đầu workflow)**
- **Tên**: `Form: Submit Search Keyword`
- **Cấu hình**:
  - Thêm trường nhập từ khóa (ví dụ: `"dentist in New York"`).
  - Lưu kết quả vào biến `keyword`.

##### **🔹 Node 2 & 5: Dumpling AI (Tìm kiếm doanh nghiệp & trích xuất email)**
- **Tên**: `Dumpling AI: Search Google Maps for Businesses` và `Dumpling AI: Extract Email + Website Summary`
- **Cấu hình**:
  - Điền **API Key** của Dumpling AI vào `httpHeaderAuth`.
  - Thay đổi URL API theo hướng dẫn của Dumpling AI (nếu cần).
  - **Lưu ý**: Node này trả về danh sách doanh nghiệp, sau đó được **split** thành các bản ghi riêng lẻ.

##### **🔹 Node 6: GPT-4 (Viết email cá nhân hóa)**
- **Tên**: `✍️ GPT-4: Write Personalized Icebreaker Email`
- **Cấu hình**:
  - Chọn **OpenAI API Key** trong `openAiApi`.
  - Cấu hình **Prompt** để GPT-4 viết email dựa trên:
    ```json
    {
      "business_name": "{{ $node["Dumpling AI: Extract Email + Website Summary"].json["business_name"] }}",
      "website": "{{ $node["Dumpling AI: Extract Email + Website Summary"].json["website"] }}",
      "email": "{{ $node["Dumpling AI: Extract Email + Website Summary"].json["email"] }}"
    }
    ```
  - **Mẫu Prompt gợi ý**:
    > *"Tôi là [Tên Bạn], chuyên hỗ trợ [ngành nghề]. Tôi tìm thấy [Doanh nghiệp] trên [Website]. Tôi rất ấn tượng với [đặc điểm nổi bật của doanh nghiệp]. Có thể tôi có thể giúp gì cho bạn không? Trân trọng, [Tên Bạn]."*

##### **🔹 Node 7: Filter (Kiểm tra email tồn tại)**
- **Tên**: `✅ IF: Email Exists`
- **Cấu hình**:
  - Chọn **Email** từ node trước và **lọc bỏ** những bản ghi không có email.

##### **🔹 Node 8: Google Sheets (Lưu log kết quả)**
- **Tên**: `📄 Log to Google Sheets`
- **Cấu hình**:
  - Chọn **Google Sheets OAuth 2.0** trong `googleSheetsOAuth2Api`.
  - Điền **Sheet Name** (ví dụ: `Cold_Email_Leads`).
  - Cấu hình **Columns** để lưu:
    - `Business Name`
    - `Website`
    - `Email`
    - `Icebreaker Email`
    - `Status` (ví dụ: `New`, `Sent`, `Follow-up`).

##### **🔹 Node 9: Instantly.ai (Thêm vào chiến dịch - tùy chọn)**
- **Tên**: `📤 Instantly API: Add to Campaign`
- **Cấu hình**:
  - Điền **API Key** của Instantly.ai vào `httpHeaderAuth`.
  - Thay đổi URL API theo API docs của Instantly.ai.
  - **Lưu ý**: Nếu không sử dụng, có thể xóa node này.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhập từ khóa (ví dụ: `"cafe in Hanoi"`).
  - Kiểm tra kết quả trong **Google Sheets** và **Instantly.ai** (nếu có).
- **Bật Active**:
  - Chuyển workflow sang **Active** để chạy tự động khi có input.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích hợp Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
2. **Lưu log chi tiết**:
   - Sử dụng **Google Sheets** để lưu lịch sử gửi email và phản hồi.
3. **Tự động gửi email**:
   - Kết hợp với **n8n-nodes-base.email** để gửi email tự động sau khi viết xong.
4. **Tối ưu Dumpling AI**:
   - Nếu API Dumpling AI có giới hạn, sử dụng **splitInBatches** để tránh bị block.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc tìm kiếm và viết email làm nóng, đồng thời **tăng hiệu quả lead generation** nhờ cá nhân hóa và tự động hóa. **Hãy áp dụng ngay** và bắt đầu tự động hóa lead generation của mình!

👉 **Bắt đầu với n8n ngay hôm nay** và [đăng ký VPS](https://tino.vn/vps-n8n?affid=388) để chạy workflow 24/7!