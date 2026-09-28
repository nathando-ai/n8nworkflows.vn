---
title: "🚀 Tự động hóa tổng kết bài viết từ URL bằng AI Gemini - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động tổng kết nội dung bài viết từ URL bằng AI Gemini trong n8n. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-tong-ket-bai-viet-ai-gemini-n8n"
tags: [n8n, automation, no-code, AI, Google Gemini]
keywords: [n8n workflow, tự động hóa, AI tổng kết, Google Gemini, n8n chatbot]
---

# 🚀 Tự động hóa tổng kết bài viết từ URL bằng AI Gemini - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải tốn thời gian đáng kể để đọc và tổng kết nội dung từ các bài viết trên WordPress hoặc các blog. Quá trình này không chỉ mất thời gian mà còn dễ gây mệt mỏi và không hiệu quả. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc đọc và tổng kết nội dung từ các bài viết.
- Đảm bảo tính chính xác và nhất quán trong quá trình tổng kết.
- Tự động hóa toàn bộ quá trình, giảm thiểu lỗi do con người gây ra.
- Nâng cao hiệu quả làm việc và tập trung vào các nhiệm vụ quan trọng hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Gemini API (Google Palm API) để sử dụng AI trong quá trình tổng kết.
- URL của bài viết cần tổng kết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/15799](https://n8n.io/workflows/15799) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON đã tải về.
3. Hoặc, các sếp có thể copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Chat Trigger**: Node này dùng để nhận đầu vào từ người dùng. Các sếp có thể thay đổi cách nhập liệu (ví dụ: từ Telegram, Slack, hoặc Zalo) bằng cách thay đổi node này.
- **Extract URL**: Node này dùng để trích xuất URL từ đầu vào. Các sếp cần đảm bảo rằng đầu vào là một URL hợp lệ.
- **Check Valid URL**: Node này dùng để kiểm tra xem URL có hợp lệ hay không. Nếu URL không hợp lệ, workflow sẽ dừng lại.
- **Fetch Webpage**: Node này dùng để tải nội dung của trang web từ URL đã nhập. Các sếp cần đảm bảo rằng trang web cho phép truy cập từ n8n.
- **Extract HTML Content**: Node này dùng để trích xuất nội dung HTML từ trang web. Các sếp có thể điều chỉnh các CSS selectors để loại bỏ các phần không cần thiết (ví dụ: quảng cáo, thanh điều hướng, chân trang).
- **AI Summarizer**: Node này dùng để tổng kết nội dung đã trích xuất bằng AI Gemini. Các sếp có thể điều chỉnh prompt để thay đổi cách tổng kết (ví dụ: thay đổi độ dài, phong cách, hoặc ngôn ngữ).
- **Google Gemini Chat Model**: Node này dùng để kết nối với API của Google Gemini. Các sếp cần tạo một credential mới trong n8n và nhập API key của Google Palm API.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp có thể kích hoạt workflow bằng cách:

1. Nhấn vào nút "Activate" trong n8n Editor.
2. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng như mong đợi.
3. Bật Active workflow để bắt đầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi cách nhập liệu**: Các sếp có thể thay đổi cách nhập liệu từ Chat Trigger sang các nền tảng khác như Telegram, Slack, hoặc Zalo để tiện lợi hơn.
- **Điều chỉnh prompt AI**: Các sếp có thể điều chỉnh prompt trong node AI Summarizer để thay đổi cách tổng kết (ví dụ: thay đổi độ dài, phong cách, hoặc ngôn ngữ).
- **Lưu log và báo cáo**: Các sếp có thể thêm các node để lưu log và báo cáo kết quả tổng kết để theo dõi hiệu suất của workflow.
- **Tích hợp với các hệ thống khác**: Các sếp có thể tích hợp workflow này với các hệ thống khác như Google Sheets, Notion, hoặc Trello để lưu trữ và quản lý kết quả tổng kết.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình tổng kết nội dung từ các bài viết trên WordPress hoặc các blog. Với việc sử dụng AI Gemini, các sếp có thể đảm bảo tính chính xác và nhất quán trong quá trình tổng kết. Hãy áp dụng ngay workflow này để nâng cao hiệu quả làm việc và tiết kiệm thời gian đáng kể.