---
title: "💰 [Tự động hóa chi tiêu WhatsApp với AI: Nhận dạng văn bản, hình ảnh & âm thanh]"
description: "Hướng dẫn chi tiết workflow n8n tự động ghi nhận chi tiêu từ WhatsApp bằng AI (nhận dạng văn bản, hình ảnh, âm thanh) và lưu vào PostgreSQL. Tiết kiệm 90% thời gian thủ công."
slug: "tu-dong-hoa-chi-tieu-whatsapp-voi-ai"
tags: [n8n, automation, no-code, whatsapp, ai, postgres]
keywords: [n8n workflow, tự động hóa chi tiêu, nhận dạng văn bản, hình ảnh, âm thanh, postgres]
---

# 💰 Tự động hóa chi tiêu WhatsApp với AI: Nhận dạng văn bản, hình ảnh & âm thanh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi quản lý chi tiêu cá nhân hoặc doanh nghiệp, việc ghi nhận các khoản chi từ tin nhắn WhatsApp thường là công việc thủ công, tốn thời gian và dễ xảy ra lỗi. Các sếp thường phải:

- Phân loại thủ công từng tin nhắn (chi tiêu, báo cáo, câu hỏi...)
- Nhập dữ liệu vào bảng tính hoặc cơ sở dữ liệu
- Xử lý các hóa đơn hình ảnh/âm thanh một cách thủ công

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, với kết quả chính xác và không giới hạn số lượng tin nhắn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tự động xử lý hàng nghìn tin nhắn mỗi ngày
- **Chính xác cao**: AI phân loại và trích xuất dữ liệu từ văn bản, hình ảnh, âm thanh
- **Tích hợp hoàn hảo**: Lưu dữ liệu vào PostgreSQL để phân tích báo cáo
- **Hỗ trợ đa dạng**: Xử lý cả tin nhắn văn bản, hình ảnh và âm thanh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API
- PostgreSQL database
- API keys cho:
  - OpenAI (hoặc các LLM khác)
  - Deepgram (cho nhận dạng âm thanh)
  - Google Gemini (cho nhận dạng hình ảnh)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/5201)
2. Click "Copy JSON" và lưu vào file `whatsapp-expense-tracker.json`
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON đã lưu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Incoming WhatsApp Trigger"**:
   - Cấu hình credentials cho WhatsApp Business API
   - Điền số điện thoại nhận tin nhắn

2. **Node "OpenAI Chat Model" (x8)**:
   - Tạo credentials cho OpenAI
   - Chọn model phù hợp (gợi ý: gpt-4o-mini)

3. **Node "Fetch User Profile from Postgres"**:
   - Cấu hình credentials PostgreSQL
   - Điền câu truy vấn lấy thông tin người dùng

4. **Node "Insert Transaction into DB1"**:
   - Cấu hình credentials PostgreSQL
   - Điền câu truy vấn chèn giao dịch

5. **Node "Run OCR on Image (Gemini API)"**:
   - Tạo credentials cho Google Gemini
   - Điền endpoint API

6. **Node "Transcribe Audio by deepgram"**:
   - Tạo credentials cho Deepgram
   - Điền endpoint API

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn mẫu qua WhatsApp
   - Kiểm tra dữ liệu được lưu vào PostgreSQL
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có giao dịch mới
- Thêm node gửi báo cáo định kỳ qua email
- Tích hợp với các công cụ phân tích dữ liệu như Metabase
- Thêm tính năng xác thực hai bước cho các giao dịch lớn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình ghi nhận chi tiêu từ WhatsApp, từ nhận dạng hình ảnh/âm thanh đến lưu trữ dữ liệu. Với kết quả chính xác và tiết kiệm thời gian đáng kể, đây là giải pháp hoàn hảo cho các doanh nghiệp và cá nhân muốn tối ưu hóa quản lý chi tiêu.