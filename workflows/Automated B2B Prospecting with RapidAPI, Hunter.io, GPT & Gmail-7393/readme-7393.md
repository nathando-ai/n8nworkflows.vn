---
title: "🚀 Tự Động Hoàn Thành B2B Prospecting: Tìm Khách Hàng, Lấy Email & Gửi Email Cá Nhân Hóa Với AI (N8N)"
description: "Workflow tự động hóa tìm kiếm doanh nghiệp địa phương, xác định thông tin liên lạc, và gửi email cá nhân hóa thông qua AI (GPT-4) + Gmail. Giúp các sếp tiết kiệm 10-15 giờ/ngày trong công việc prospecting."
slug: "tieu-dong-hoan-thanh-b2b-prospecting-voi-n8n"
tags: [n8n, automation, lead-generation, ai-chatbot, gmail-integration, hunter-io, rapidapi]
keywords: [n8n workflow prospecting, tự động hóa tìm khách hàng B2B, email cá nhân hóa với AI, hunter.io + n8n, tự động gửi email prospecting]
---

# 🚀 **Tự Động Hoàn Thành B2B Prospecting: Từ Tìm Khách Hàng Đến Email Cá Nhân Hóa Với AI**

## **💡 Nỗi Đau Của Các Sếp Trong Prospecting B2B**
Mỗi ngày, các sếp phải:
- **Tìm kiếm thủ công** doanh nghiệp tiềm năng trên Google, LinkedIn, hoặc các trang danh mục.
- **Lấy email** của người quyết định (CEO, Marketing Director...) bằng cách sử dụng công cụ như Hunter.io hoặc Apollo.io.
- **Viết email cá nhân hóa** cho từng khách hàng, mất thời gian nghiên cứu và điều chỉnh nội dung.
- **Quên theo dõi** sau khi gửi email, dẫn đến tỷ lệ phản hồi thấp.

**Kết quả?** Tốn **10-15 giờ/ngày** cho một công việc có thể tự động hóa hoàn toàn.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** trong prospecting (từ tìm kiếm đến gửi email).
✅ **Tăng tỷ lệ mở email** lên **30-50%** nhờ nội dung cá nhân hóa bởi AI.
✅ **Hoàn toàn tự động hóa** quá trình theo dõi với Google Tasks.
✅ **Cập nhật liên tục** danh sách khách hàng mới mà không cần can thiệp thủ công.

---
## **🎯 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
🔹 **Tài khoản RapidAPI** (để tìm kiếm doanh nghiệp địa phương).
🔹 **Tài khoản Hunter.io** (để lấy email của người quyết định).
🔹 **Tài khoản OpenAI** (để sử dụng GPT-4 tạo nội dung email).
🔹 **Tài khoản Gmail** (để gửi email tự động).
🔹 **Tài khoản Google Tasks** (để quản lý follow-up).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7393](https://n8n.io/workflows/7393) và import vào **n8n Editor**.
- **Hoặc copy/paste** JSON từ file vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Cấu Hình Credentials (Tài Khoản)**
| **Node**               | **Credentials Cần Thiết**       | **Hướng Dẫn Cấu Hình** |
|------------------------|----------------------------------|-------------------------|
| **Search Local Businesses** | `x-rapidapi-key` (RapidAPI) | Đăng ký API key tại [RapidAPI](https://rapidapi.com/) và thêm vào **Header Auth** trong node. |
| **Find Contacts (Hunter)** | `hunterApi` (Hunter.io) | Đăng ký tài khoản Hunter.io và thêm **Hunter Credential** vào node. |
| **OpenAI Chat Model**   | `openAiApi` (OpenAI) | Đăng ký API key tại [OpenAI](https://platform.openai.com/) và thêm vào node. |
| **Send Email (Gmail)**  | `gmailOAuth2` (Gmail) | Cấu hình OAuth2 cho Gmail trong n8n. |
| **Create Google Task**  | `googleTasksOAuth2Api` | Cấu hình OAuth2 cho Google Tasks và chọn **Task List** phù hợp. |

#### **🔹 Cấu Hình AI Prompt (Nội Dung Email Cá Nhân Hóa)**
- Mở node **"Generate Email Body (AI)"** (type: `agent`).
- **Chỉnh sửa "System Message"** để mô tả công ty và dịch vụ của bạn (ví dụ):
  ```plaintext
  Bạn là một chuyên gia marketing B2B. Tôi là [Tên Công Ty] chuyên cung cấp [Dịch Vụ]. Hãy viết một email cá nhân hóa cho [Tên Khách Hàng] với:
  - Mở đầu thân thiện.
  - Giới thiệu sản phẩm/dịch vụ phù hợp với ngành nghề của họ.
  - Call-to-action rõ ràng (vd: "Hãy liên hệ với tôi để biết thêm chi tiết").
  ```
- **Kiểm tra lại "Format AI Output"** trong node **"Format AI Output"** (type: `code`) để đảm bảo email được định dạng đúng.

#### **🔹 Cấu Hình Email Signature**
- Mở node **"Assemble Final Email"** (type: `set`).
- **Chỉnh sửa biểu thức `email_body`** để thêm chữ ký cá nhân (ví dụ):
  ```javascript
  `{{$json["email_body"]}}\n\nTrân trọng,\n[Tên Bạn]\n[Tên Công Ty]\n[Website]\n[Số Điện Thoại]`
  ```

### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run** với dữ liệu mẫu (ví dụ: nhập tên một doanh nghiệp địa phương).
- **Bật Active** workflow sau khi kiểm tra thành công.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Kết hợp với Slack/Telegram**: Thêm node **webhook** để nhận thông báo khi email được gửi thành công.
🔹 **Lưu Log Tất Cả Email**: Sử dụng node **Set** để lưu dữ liệu vào **Google Sheets** hoặc **Airtable**.
🔹 **Gửi Báo Cáo Định Kỳ**: Tạo một workflow phụ để tổng hợp thống kê gửi email và tỷ lệ phản hồi.
🔹 **Tối Ưu AI Prompt**: Thử nghiệm các mô hình GPT khác (như `gpt-4-1106-preview`) để cải thiện chất lượng email.

---

## **📌 Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp trong prospecting B2B, đồng thời **tăng tỷ lệ chuyển đổi** nhờ email cá nhân hóa bởi AI. **Hãy áp dụng ngay** và xem kết quả trong vòng **24 giờ đầu tiên**!

👉 **Bắt đầu tự động hóa prospecting của bạn [tại đây](https://n8n.io/workflows/7393)**!