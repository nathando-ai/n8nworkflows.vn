---
title: "🚀 Tự Động Hóa Tạo & Nâng Cao Dữ Liệu Lead với Hunter.io + AI Perplexity (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tìm kiếm, enrich và phân tích lead từ Google Sheets, sau đó gửi kết quả trực tiếp qua Telegram hoặc Airtable. Tiết kiệm 10+ giờ/tháng cho bộ phận Sales & Marketing."
slug: "tieu-dong-hoa-tao-nang-cao-du-lieu-lead-hunter-ai"
tags: [n8n, automation, sales, marketing, ai, hunter-io, google-sheets, airtable, telegram]
keywords: [tự động hóa lead generation, enrich lead với AI, hunter io n8n, workflow sales marketing, tự động hóa không code, tự động hóa dữ liệu khách hàng]
---

# 🚀 **Tự Động Hóa Tạo & Nâng Cao Dữ Liệu Lead với Hunter.io + AI Perplexity**

### **Giải pháp cho các sếp Sales & Marketing:**
Bạn đã bao giờ phải tốn **giờ đồng hồ** để tìm kiếm email, số điện thoại của lead từ danh sách website? Hoặc phải **lặp lại công việc thủ công** để enrich dữ liệu khách hàng mỗi khi có lead mới? **Workflow này sẽ tự động hóa toàn bộ quy trình** cho bạn – từ tìm kiếm thông tin công ty, enrich lead, đến gửi kết quả qua Telegram hoặc Airtable **một cách tự động, không cần code!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận Sales & Marketing bằng việc tự động enrich lead.
- **Dữ liệu lead chính xác cao** với thông tin công ty, email, số điện thoại từ Hunter.io + AI.
- **Cập nhật liên tục** khi có lead mới (không cần làm thủ công).
- **Gửi báo cáo tự động** qua Telegram hoặc lưu vào Airtable cho dễ theo dõi.
- **Kết hợp AI** để phân tích và tìm kiếm thông tin chi tiết từ website công ty.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Hunter.io** (API Key) để enrich lead.
✅ **Tài khoản Google Sheets** (để lưu danh sách lead ban đầu).
✅ **Tài khoản Airtable** (để lưu kết quả enrich lead).
✅ **Tài khoản Telegram Bot** (để nhận thông báo kết quả).
✅ **API Key OpenRouter** (để sử dụng AI Perplexity).
✅ **Tài khoản n8n Self-hosted** (để chạy workflow 24/7).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/3616).
2. Trong n8n Editor, nhấn **"Import"** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **"Import from JSON"** trong n8n.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Google Sheets (Leads List)**
- **Node:** `Leads List`, `Leads List2`, `Leads List3`, `Leads List4`
  - **Tham số cần điền:**
    - **Credentials:** Chọn tài khoản Google Sheets đã kết nối.
    - **Sheet Name:** Tên sheet chứa danh sách lead (ví dụ: `"Leads"`).
    - **Range:** `Sheet1!A:B` (cột chứa tên công ty và website).

#### **🔹 Cấu hình Hunter.io (Enrich Lead)**
- **Node:** `Find real user data with Hunter`
  - **Tham số cần điền:**
    - **Credentials:** Chọn tài khoản Hunter.io đã kết nối.
    - **API Key:** Điền API Key từ Hunter.io.
    - **Domain:** Sử dụng `$json["website"]` (trích từ Google Sheets).

#### **🔹 Cấu hình AI Perplexity (OpenRouter)**
- **Node:** `OpenRouter Chat Model`, `OpenRouter Chat Model1`
  - **Tham số cần điền:**
    - **API Key:** Điền API Key từ OpenRouter.
    - **Model:** Chọn `perplexity/perplexity-large`.
    - **Prompt:** Sử dụng template đã định sẵn trong workflow (ví dụ: *"Tìm thông tin chi tiết về công ty [company_name] từ website [website]"*).

#### **🔹 Cấu hình Telegram Bot (Gửi kết quả)**
- **Node:** `Telegram Trigger`
  - **Tham số cần điền:**
    - **Credentials:** Chọn bot Telegram đã kết nối.
    - **Chat ID:** ID của chat Telegram muốn nhận thông báo.
    - **Message:** Sử dụng `$json["enriched_lead"]` (dữ liệu enrich lead).

#### **🔹 Cấu hình Airtable (Lưu kết quả)**
- **Node:** `Airtable`
  - **Tham số cần điền:**
    - **Credentials:** Chọn tài khoản Airtable đã kết nối.
    - **Base ID:** ID của bảng Airtable.
    - **Table Name:** Tên bảng muốn lưu lead enrich (ví dụ: `"Enriched Leads"`).
    - **Records:** Sử dụng `$json["final_data"]` (dữ liệu cuối cùng).

#### **🔹 Cấu hình Schedule Trigger (Chạy tự động)**
- **Node:** `Schedule Trigger`
  - **Tham số cần điền:**
    - **Schedule:** Chọn thời gian chạy (ví dụ: **mỗi ngày lúc 9h sáng**).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Test"** trên node `Manual Trigger` để kiểm tra workflow.
   - Kiểm tra kết quả trên **Telegram** và **Airtable**.
2. **Bật Active workflow** khi đã kiểm tra xong.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
- **Kết hợp với Slack:** Thay vì Telegram, các sếp có thể gửi kết quả qua Slack bằng node `slack`.
- **Lưu log vào Google Drive:** Sử dụng node `googleDrive` để lưu lịch sử enrich lead.
- **Gửi báo cáo định kỳ:** Sử dụng node `email` để gửi báo cáo hàng tuần cho team.
- **Tối ưu AI:** Thay đổi prompt trong `OpenRouter Chat Model` để lấy thông tin chi tiết hơn.
- **Lọc lead trùng lặp:** Sử dụng node `Keep only non-duplicates code` để tránh dữ liệu trùng.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp Sales & Marketing bằng cách tự động enrich lead từ Google Sheets, sử dụng AI Perplexity và Hunter.io. **Không cần code**, chỉ cần cấu hình vài bước là có thể chạy 24/7 trên **n8n Self-hosted**.

👉 **Hãy áp dụng ngay và bắt đầu tự động hóa lead của mình!**
👉 **Cần hỗ trợ thêm?** Liên hệ với tác giả: [Velebit](https://innovatio.design) hoặc [n8n Community](https://community.n8n.io/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::