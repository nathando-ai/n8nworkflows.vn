---
title: "🚀 Tự động lấy giá hàng hóa trực tiếp với Octagon, OpenAI và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động cào và cập nhật giá hàng hóa (vàng, dầu, nông sản...) thời gian thực vào Google Sheets bằng Octagon Agent và OpenAI."
slug: "tu-dong-lay-gia-hang-hoa-octagon-openai-google-sheets"
tags: [n8n, automation, no-code, openai, google-sheets, trading]
keywords: [n8n workflow, tự động hóa giá hàng hóa, octagon agent, openai n8n, google sheets automation]
---

# 🚀 Tự động lấy giá hàng hóa trực tiếp với Octagon, OpenAI và Google Sheets

Các nhà đầu tư và trader thường mất rất nhiều thời gian để theo dõi giá các mặt hàng (vàng, bạc, dầu thô, khí tự nhiên...) từ nhiều nguồn khác nhau rồi cập nhật thủ công vào Google Sheets để phân tích. Việc này vừa nhàm chán, dễ sai sót lại vừa chậm trễ trong thị trường biến động từng giây.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh giúp tự động hóa 100% quy trình: lấy danh sách mã hàng hóa, gọi **Octagon Agent** kết hợp **OpenAI** để phân tích, cào dữ liệu giá trực tiếp và đồng bộ ngược lại vào Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần copy-paste thủ công giá vàng (GCUSD), bạc (SIUSD), dầu (CLUSD) hay khí đốt (NGUSD).
- **Dữ liệu thời gian thực:** Cập nhật liên tục giá thị trường mới nhất nhờ sức mạnh của Octagon Agents.
- **AI-Powered:** Sử dụng OpenAI để tối ưu hóa câu lệnh (prompt) và xử lý dữ liệu trả về một cách chính xác.
- **Đồng bộ hóa mượt mà:** Tự động ghi đè hoặc cập nhật đúng dòng, đúng cột trên Google Sheets kèm theo cơ chế giãn cách (throttling) chống tràn API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets Credentials** (OAuth2 API) kèm sẵn file Google Sheets có các cột chứa mã giao dịch (`Symbol` / `Ticker`) và các trường dữ liệu cần cập nhật.
- **OpenAI API Key** để tạo prompt và xử lý ngôn ngữ tự nhiên.
- **Octagon API Key** để kết nối với các agent chuyên dụng của Octagon.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file từ nguồn gốc, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File / Clipboard** để dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau đây:

- **Read Commodity Symbols in Sheets (Google Sheets):** 
  - Chọn Credentials Google Sheets của các sếp.
  - Điền đúng `Document ID` và chọn đúng `Sheet Name` chứa danh sách mã hàng hóa cần theo dõi (ví dụ: `GCUSD`, `SIUSD`, `CLUSD`, `NGUSD`...).
- **Create Commodities Quote Prompt (OpenAI):** 
  - Chọn Credentials OpenAI.
  - Kiểm tra Model (nên dùng `gpt-4o-mini` hoặc `gpt-4o` tùy nhu cầu) và cấu hình prompt xây dựng tác vụ cho từng mã hàng hóa.
- **Execute Octagon Agent (Octagon):** 
  - Thêm Octagon API Credentials. Node này sẽ chịu trách nhiệm giao tiếp với Agent để trích xuất dữ liệu giá thị trường chính xác dựa trên Skill được fetch từ GitHub.
- **Update Commodities in Sheets (Google Sheets):** 
  - Thiết lập lại ánh xạ (mapping) giữa các trường dữ liệu sau khi qua bước **Parse Commodities Quote Response (Code)** với các cột tương ứng trong bảng Google Sheets của các sếp.
- **Wait 1 Second (Wait):** 
  - Giúp giới hạn tốc độ (rate limit) giữa các lần lặp qua từng mã hàng hóa, tránh việc Google Sheets hoặc API bên thứ ba báo lỗi quá tải.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node **Manual Workflow Trigger** để test chạy thử với dữ liệu mẫu xem giá có đẩy về Google Sheets chuẩn xác không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi sang Cron Trigger:** Thay thế node `Manual Workflow Trigger` bằng node `Schedule Trigger` (Cron) để n8n tự động cập nhật giá mỗi sáng hoặc định kỳ hàng giờ/hàng ngày.
- **Thêm cảnh báo (Alerts):** Tích hợp thêm node Telegram hoặc Slack ở cuối luồng để gửi thông báo về máy mỗi khi cập nhật giá thành công hoặc khi có biến động giá mạnh.
- **Mở rộng danh mục:** Dễ dàng bổ sung thêm các mã nông sản (như `ZCUSD`, `ZSUSD`, `ZWUSD`) vào Google Sheets mà không cần sửa đổi cấu trúc code bên trong workflow.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc kết hợp giữa AI Agents (Octagon + OpenAI) và các công cụ văn phòng quen thuộc (Google Sheets). Hãy thiết lập ngay hôm nay để giải phóng bản thân khỏi các tác vụ cập nhật dữ liệu thủ công các sếp nhé!