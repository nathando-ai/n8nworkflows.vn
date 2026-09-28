---
title: "🎓 Hướng dẫn tự động hóa đánh giá AI với Gemini và Google Sheets - Dành cho người mới bắt đầu"
description: "Tự động hóa quá trình đánh giá kết quả AI so với dữ liệu chuẩn trong Google Sheets bằng công cụ Evaluation của n8n. Hướng dẫn chi tiết cho người mới bắt đầu."
slug: "huong-dan-danh-gia-ai-voi-gemini-va-google-sheets"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, đánh giá AI, Google Sheets, Gemini]
---

# 🎓 Hướng dẫn tự động hóa đánh giá AI với Gemini và Google Sheets - Dành cho người mới bắt đầu

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải kiểm tra thủ công kết quả của các mô hình AI không? Với workflow này, các sếp có thể tự động hóa quá trình đánh giá tính chính xác của kết quả AI so với dữ liệu chuẩn trong Google Sheets một cách dễ dàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa quá trình đánh giá kết quả AI so với dữ liệu chuẩn trong Google Sheets
- Tiết kiệm thời gian và công sức cho các sếp
- Đảm bảo tính chính xác và nhất quán trong quá trình đánh giá
- Tích hợp dễ dàng với các công cụ AI khác trong hệ sinh thái n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key từ Google Cloud Platform để sử dụng Google Gemini
- Google Sheets đã được sao chép từ [template này](https://docs.google.com/spreadsheets/d/1y6Gyjws8se12QX0uG4eS9il5-v29IpsgdFx3VqIYzWQ/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/8227](https://n8n.io/workflows/8227)
2. Nhấp vào nút "Download" để tải về file JSON của workflow
3. Trong giao diện n8n, nhấp vào nút "Import from File" và chọn file JSON vừa tải về

Hoặc các sếp có thể copy/paste JSON của workflow vào n8n Editor bằng cách:

1. Truy cập vào trang [n8n.io/workflows/8227](https://n8n.io/workflows/8227)
2. Copy toàn bộ nội dung JSON của workflow
3. Trong giao diện n8n, nhấp vào nút "Import from Clipboard" và dán nội dung JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node quan trọng sau:

- **When fetching a dataset row**: Node này sẽ kích hoạt workflow khi có dữ liệu mới trong Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets OAuth2 API.
- **AI Agent**: Node này sẽ xử lý dữ liệu đầu vào và trả về kết quả đánh giá. Các sếp cần cấu hình credentials cho Google Palm API.
- **Google Gemini Chat Model**: Node này sẽ sử dụng mô hình Gemini để đánh giá kết quả AI. Các sếp cần cấu hình credentials cho Google Palm API.
- **Set output Evaluation**: Node này sẽ lưu kết quả đánh giá vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets OAuth2 API.
- **Set correctness**: Node này sẽ cập nhật độ chính xác của kết quả đánh giá vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets OAuth2 API.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp có thể kích hoạt workflow bằng cách:

1. Nhấp vào nút "Activate" để kích hoạt workflow
2. Nhấp vào nút "Execute" để chạy workflow với dữ liệu mẫu
3. Kiểm tra kết quả đánh giá trong Google Sheets

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với các công cụ khác trong hệ sinh thái n8n để tự động hóa các quy trình đánh giá phức tạp hơn.
- Các sếp có thể sử dụng workflow này để đánh giá kết quả của các mô hình AI khác nhau và so sánh hiệu suất của chúng.
- Các sếp có thể mở rộng workflow này để tự động gửi báo cáo đánh giá qua email hoặc Slack.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hiệu quả để đánh giá kết quả AI so với dữ liệu chuẩn trong Google Sheets. Với workflow này, các sếp có thể tiết kiệm thời gian và công sức trong quá trình đánh giá, đồng thời đảm bảo tính chính xác và nhất quán trong kết quả đánh giá. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của các sếp!