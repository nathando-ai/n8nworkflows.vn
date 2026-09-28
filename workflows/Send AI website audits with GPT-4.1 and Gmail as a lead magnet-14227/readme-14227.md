---
title: "🚀 Tự Động Hóa Audit Website AI + Email Lead Magnet - Tham Khảo & Cài Đặt Chi Tiết"
description: "Workflow tự động hóa sử dụng GPT-4.1 và Gmail để phân tích website khách hàng, gửi báo cáo cải tiến cá nhân hóa qua email - giải pháp lead magnet hiệu quả cho doanh nghiệp. Thời gian xử lý: ~30-60s/lead."
slug: "tieu-dong-hoa-audit-website-ai-va-email-lead-magnet"
tags: [n8n, automation, lead-generation, ai-summarization, gmail-integration]
keywords: [n8n workflow lead magnet, tự động hóa audit website, gpt-4.1 email cá nhân hóa, lead generation AI, n8n self-hosted]
---

# 🚀 **Tự Động Hóa Audit Website AI + Email Lead Magnet - Hướng Dẫn Cài Đặt & Sử Dụng**

## **📌 Nỗi Đau Của Doanh Nghiệp & Giải Pháp**
Các sếp đang gặp khó khăn khi:
- **Tốn thời gian** để phân tích website khách hàng thủ công (thường mất 1-2 giờ/lead).
- **Không cá nhân hóa** nội dung, dẫn đến tỷ lệ chuyển đổi thấp.
- **Không tự động hóa** quy trình lead generation, bỏ lỡ cơ hội liên lạc với khách hàng tiềm năng.

**Workflow này giải quyết tất cả!** Khi khách hàng nhập email và URL website vào form, hệ thống sẽ:
✅ **Tự động lấy nội dung website** (xóa script, định dạng HTML).
✅ **Phân tích AI sâu** (gpt-4.1) về:
   - Loại hình doanh nghiệp, đối tượng mục tiêu.
   - Các điểm yếu tự động hóa (7-10 điểm với mức độ nguy cơ).
   - Bộ công cụ copywriting (gợi ý mở đầu, tone voice, phản đối).
✅ **Tạo email cá nhân hóa** (ngôn ngữ website) với 10 cải tiến cụ thể.
✅ **Gửi email tự động** qua Gmail với thiết kế branded (logo, gradient header, CTA button).

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với phân tích thủ công.
- **Tỷ lệ chuyển đổi cao** nhờ email cá nhân hóa (ngôn ngữ website).
- **Hoạt động 24/7** mà không cần can thiệp người.
- **Thiết kế chuyên nghiệp** (HTML email branded, logo, CTA button).
- **Dữ liệu phân tích chi tiết** để tối ưu website.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần:
1. **Tài khoản n8n Self-hosted** (khuyến nghị VPS để chạy 24/7).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Tài khoản Gmail** (để gửi email tự động).
4. **Logo & URL liên kết** (Booking, Instagram, LinkedIn).
5. **Domain & Form Embed** (để chia sẻ link form cho khách hàng).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14227](https://n8n.io/workflows/14227).
- **Import vào n8n Editor**:
  - Nhấp `Import` → Chọn file JSON → `Import`.
  - **Hoặc** copy toàn bộ JSON vào `Create Workflow` → `Paste JSON`.

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**
#### **🔹 Node 1: Form Trigger (n8n-nodes-base.formTrigger)**
- **Cấu hình 2 trường**:
  - `Email` (type: `email`).
  - `Website URL` (type: `url`).
- **Embed form** vào landing page hoặc chia sẻ link trực tiếp.

#### **🔹 Node 2: Fetch Website HTML (n8n-nodes-base.httpRequest)**
- **Không cần cấu hình** (sử dụng URL từ form).

#### **🔹 Node 3: Clean HTML (n8n-nodes-base.code)**
- **Mã JavaScript mặc định** đã xử lý:
  - Xóa script, style, tag HTML thừa.
  - Giữ nội dung văn bản (max 28K chars ≈ 7K tokens).
  - Lấy các signal quan trọng (WhatsApp, booking, checkout).

#### **🔹 Node 4-5: Analyst & Writer Agent (AI Processing)**
- **Sử dụng OpenAI API**:
  - **Analyst Model**: `gpt-4.1-mini` (hoặc `gpt-4o` cho độ chính xác cao hơn).
  - **Writer Model**: `gpt-4.1-mini` (tự động viết email cá nhân hóa).
- **Không cần cấu hình** (n8n tự động lấy `openAiApi` từ credentials).

#### **🔹 Node 6: Build Email HTML (n8n-nodes-base.code)**
- **Cần chỉnh sửa mã** tại đầu file:
  ```javascript
  const YOUR_NAME = "Tên Của Bạn";
  const YOUR_EMAIL = "email@domain.com";
  const CAL_URL = "https://calendly.com/your-link";
  const INSTAGRAM_URL = "https://instagram.com/yourpage";
  const LINKEDIN_URL = "https://linkedin.com/in/yourprofile";
  const LOGO_URL = "https://yourdomain.com/logo.png";
  ```
- **Kết quả**: Email HTML branded với:
  - Header gradient + logo.
  - Thẻ cải tiến số hóa.
  - CTA button liên kết đến Booking.

#### **🔹 Node 7: Send Email (n8n-nodes-base.gmail)**
- **Cấu hình Gmail OAuth2**:
  1. Đăng nhập vào n8n → `Credentials` → `Add` → `Gmail OAuth2`.
  2. Chọn `senderName` (hiển thị tên người gửi).
  3. **Không cần chỉnh subject** (AI tự động tạo).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhập email giả (ví dụ: `test@example.com`) và URL website.
   - Kiểm tra email nhận được có đúng format không.
2. **Bật Active**:
   - Nhấp `Active` trên workflow.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾN TRIỂN THÊM]
- **Kết nối Slack/Telegram**: Gửi thông báo khi email được gửi thành công.
- **Lưu log**: Sử dụng `stickyNote` để ghi lại lịch sử phân tích.
- **Báo cáo định kỳ**: Tạo báo cáo hàng tháng về số lead nhận được.
- **Cập nhật logo/color**: Thay đổi trong node `Build Email HTML`.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing thay vì phân tích thủ công. **Tự động hóa 100%**, **cá nhân hóa cao**, và **hoạt động liên tục** - đây là công cụ không thể thiếu cho lead generation hiện đại.

**👉 Bắt đầu ngay!**
1. **Cài n8n Self-hosted** trên VPS (khuyến nghị [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chia sẻ form** cho khách hàng và bắt đầu thu hút lead!

---
**💡 Lưu ý**: Nếu gặp vấn đề, tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ với Synecta (tác giả workflow). Chúc các sếp thành công! 🚀