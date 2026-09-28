---
title: "🚀 Tự Động Hóa Báo Cáo An Toàn Hàng Ngày Cho Lãnh Đạo - Với AI & Wazuh Alerts"
description: "Workflow này tự động tạo báo cáo an toàn hàng ngày bằng AI, giúp các lãnh đạo không chuyên kỹ thuật hiểu nhanh tình hình an ninh mạng thông qua email. Giảm thời gian phân tích từ 2 giờ xuống 5 phút/ngày!"
slug: "tieu-dong-hoa-bao-cao-an-toan-hang-ngay-voi-ai-wazuh"
tags: [n8n, automation, security, ai-summarization, no-code, wazuh, nixguard, secop]
keywords: [tự động hóa báo cáo an toàn, n8n workflow an ninh mạng, báo cáo hàng ngày cho lãnh đạo, ai tóm tắt cảnh báo an toàn, wazuh integration, nixguard api]
---

# 🚀 **Tự Động Hóa Báo Cáo An Toàn Hàng Ngày Cho Lãnh Đạo - Với AI & Wazuh Alerts**

### **Giải pháp cho vấn đề:**
Các sếp không chuyên kỹ thuật thường phải mất **2-3 giờ/ngày** để đọc và tổng hợp cảnh báo an ninh mạng từ hệ thống Wazuh, chỉ để hiểu được tình hình tổng quan. Workflow này **tự động hóa toàn bộ quy trình** bằng AI, giúp bạn nhận được **báo cáo tóm tắt 5 phút** qua email mỗi sáng, với nội dung:
✅ **Tóm tắt các sự kiện quan trọng** (không cần đọc từng cảnh báo chi tiết).
✅ **Đánh giá rủi ro** theo ngôn ngữ dễ hiểu (không cần kiến thức kỹ thuật).
✅ **Gợi ý hành động** (nếu có).
✅ **Hoạt động 24/7** (không phụ thuộc vào thời gian làm việc của bạn).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 15-20 giờ/tuần** (không cần phân tích thủ công).
- **Chính xác 100%** (AI tóm tắt dựa trên dữ liệu thực từ Wazuh).
- **Cá nhân hóa** (báo cáo được gửi trực tiếp đến email cá nhân).
- **Hoạt động liên tục** (không phụ thuộc vào thời gian làm việc).
- **Ngôn ngữ dễ hiểu** (phù hợp cho lãnh đạo không chuyên kỹ thuật).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **API Key của NixGuard**:
   - Đăng ký tại [NixGuard](https://nixguard.thenex.world) để lấy API Key.
   - **Lưu ý**: API Key này sẽ được sử dụng để kết nối với hệ thống AI tóm tắt cảnh báo.
2. **Workflow con "Get Real-Time Security Insights"**:
   - Workflow này **phải được import và kích hoạt** trước (link gốc: [n8n.io/workflows/5895](https://n8n.io/workflows/5895)).
   - **ID của workflow con**: `I0nUORqYTwDFZa51` (nếu khác, cần cập nhật trong node `Execute Workflow`).
3. **Thông tin email**:
   - Tài khoản email để gửi báo cáo (cần cấu hình trong node `Send Email`).
   - Danh sách email của các lãnh đạo cần nhận báo cáo.
4. **Hệ thống Wazuh**:
   - Đảm bảo Wazuh đã được cấu hình và phát sinh cảnh báo an ninh mạng.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5895](https://n8n.io/workflows/5895) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5895) và paste vào **Import Workflow** trong n8n.
- **Lưu ý**: Sau khi import, **không kích hoạt workflow** ngay mà phải cấu hình các node quan trọng trước.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **2 giai đoạn chính** (tương ứng với 2 workflow con được gọi):
- **Giai đoạn 1**: Lấy dữ liệu cảnh báo từ Wazuh (qua NixGuard).
- **Giai đoạn 2**: AI tóm tắt cảnh báo thành báo cáo cho lãnh đạo.

##### **A. Cấu hình API Key & Workflow Con**
1. **Node "Set API Key & Initial Prompt"**:
   - Mở node này và thay thế giá trị `{{ $json["apiKey"] }}` bằng **API Key của NixGuard** (đã lấy từ bước chuẩn bị).
   - Ví dụ:
     ```json
     {
       "apiKey": "sk_your_nixguard_api_key_here"
     }
     ```

2. **Node "Execute: Get Daily Events as JSON"**:
   - Đảm bảo **Workflow con** có ID chính xác (`I0nUORqYTwDFZa51`).
   - Nếu ID khác, cập nhật trong node này và node tương ứng sau (`Execute: Generate Executive Summary`).

3. **Node "Execute: Generate Executive Summary"**:
   - Cấu hình tương tự như node trên, chỉ cần đảm bảo ID workflow con không thay đổi.

##### **B. Cấu hình Email**
1. **Node "Send Email"**:
   - Mở node và cấu hình:
     - **From**: Email của bạn (đã được xác thực).
     - **To**: Địa chỉ email của lãnh đạo (ví dụ: `to@example.com`).
     - **Subject**: Thay thế bằng tiêu đề mong muốn (ví dụ: `"Báo cáo An Toàn Hàng Ngày - [Ngày Tháng]"`).
     - **HTML Content**: Sử dụng node **"Convert Markdown to HTML"** để chuyển đổi nội dung báo cáo từ Markdown sang HTML (nếu cần).

2. **Node "Convert Markdown to HTML" (nếu có)**:
   - Đây là node **Code** tự động chuyển đổi nội dung báo cáo từ định dạng Markdown sang HTML (để email hiển thị đẹp).
   - **Không cần chỉnh sửa** trừ khi bạn muốn thay đổi cách hiển thị.

##### **C. Thiết lập Lịch Triggers**
- **Node "Run Daily at 8 AM"**:
  - Đảm bảo **schedule** được cấu hình đúng giờ (ví dụ: `0 8 * * *` để chạy lúc 8h sáng hàng ngày).
  - Nếu muốn chạy ở giờ khác, chỉnh sửa biểu thức cron.

##### **D. Node "If" (Kiểm tra có cảnh báo không)**
- Node này **kiểm tra** xem có dữ liệu cảnh báo từ Wazuh không.
- Nếu **có cảnh báo**, workflow sẽ tiến hành tóm tắt và gửi email.
- Nếu **không có cảnh báo**, workflow sẽ **bỏ qua** phần gửi email (tránh spam).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual trigger** (nút play) để kiểm tra workflow.
   - Kiểm tra email đã nhận được báo cáo chưa.
   - Nếu có lỗi, kiểm tra log trong node `Sticky Note` (nếu có) hoặc node `Set`.

2. **Kích hoạt Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo cùng lúc với email.
   - Cấu hình trong node `Execute Workflow` bằng cách thêm một **workflow con mới** gửi thông báo trên Slack/Telegram.

2. **Lưu Log Cảnh Báo**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu tất cả cảnh báo vào một bảng dữ liệu.
   - Có thể sử dụng node `Set` để truyền dữ liệu cảnh báo vào Google Sheets.

3. **Báo cáo Định Kỳ (Tuần/Tháng)**:
   - Sử dụng node **Schedule Trigger** với biểu thức cron khác (ví dụ: `0 0 * * 0` để chạy Chủ Nhật hàng tuần).
   - Tạo một **workflow con mới** để tổng hợp báo cáo tuần/month.

4. **Cập Nhật Prompt AI**:
   - Nếu muốn AI tóm tắt khác (ví dụ: thêm/loại bỏ thông tin), chỉnh sửa node **"Set Prompt for Summary"**.
   - Ví dụ:
     ```json
     {
       "prompt": "Tóm tắt cảnh báo an ninh mạng trong 3 câu ngắn gọn. Nêu rõ mức độ nghiêm trọng và hành động khuyến nghị. Không bao gồm chi tiết kỹ thuật."
     }
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc phân tích cảnh báo an ninh mạng thủ công, đồng thời cung cấp **báo cáo chuyên nghiệp** qua email mỗi sáng. Với **AI tóm tắt** và **tích hợp Wazuh**, bạn có thể **quản lý an ninh mạng hiệu quả hơn** mà không cần kiến thức kỹ thuật sâu.

**Hành động ngay!**
1. Import workflow và cấu hình theo hướng dẫn.
2. Kích hoạt và nhận báo cáo hàng ngày.
3. **Nâng cao** bằng cách kết hợp với Slack, lưu log, hoặc báo cáo định kỳ.

👉 [Tải workflow ngay](https://n8n.io/workflows/5895) và bắt đầu tự động hóa an ninh mạng của bạn!