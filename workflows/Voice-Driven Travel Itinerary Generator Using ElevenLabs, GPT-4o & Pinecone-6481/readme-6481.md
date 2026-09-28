---
title: "🚀 Tạo Lịch Trình Du Lịch Bằng Giọng Nói Sử Dụng ElevenLabs, GPT-4o & Pinecone"
description: "Hướng dẫn tự động hóa tạo lịch trình du lịch bằng giọng nói với n8n, ElevenLabs, GPT-4o và Pinecone. Giải pháp hoàn toàn không cần code cho các doanh nghiệp du lịch."
slug: "tao-lich-trinh-du-lich-bang-giong-noi"
tags: [n8n, automation, no-code, du-lich, ai, elevenlabs, gpt-4o, pinecone]
keywords: [n8n workflow, tự động hóa du lịch, ai du lịch, elevenlabs, gpt-4o, pinecone]
---

# 🚀 Tạo Lịch Trình Du Lịch Bằng Giọng Nói Sử Dụng ElevenLabs, GPT-4o & Pinecone

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình tạo lịch trình du lịch
- Tiết kiệm thời gian lên tới 80% so với làm thủ công
- Cung cấp trải nghiệm khách hàng cá nhân hóa
- Tích hợp giọng nói thông qua ElevenLabs
- Hệ thống nhớ nhớ nhung lên tới 5 lần tương tác
- Dữ liệu được lưu trữ và truy xuất nhanh chóng từ Pinecone
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (cho GPT-4o và embeddings)
- Tài khoản Pinecone API (cho lưu trữ vector)
- Tài khoản ElevenLabs (cho giọng nói)
- Dữ liệu về các gói du lịch đã được vector hóa và lưu trong Pinecone
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/6481)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải
4. Hoặc copy nội dung JSON và dán vào nút "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Voice Agent Webhook** (node đầu tiên):
   - Đặt path là "travel"
   - Phương thức HTTP là POST
   - Cấu hình webhook này trong ElevenLabs với URL của bạn

2. **Tour Recommendation AI Agent**:
   - Cấu hình system prompt phù hợp với nhu cầu của bạn
   - Đảm bảo tham chiếu đúng tới các công cụ (tools) có sẵn

3. **OpenAI Chat Model2**:
   - Chọn model "gpt-4o"
   - Cấu hình các tham số khác như nhiệt độ, top_p theo nhu cầu

4. **Tour List Data store**:
   - Cấu hình credentials Pinecone API
   - Đảm bảo đã tạo và cấu hình vector database trong Pinecone trước đó

5. **Tour Builder Q&A**:
   - Cấu hình role và instructions để trích xuất thông tin từ Pinecone
   - Đảm bảo các trường dữ liệu phù hợp với cấu trúc của bạn

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra toàn bộ chuỗi hoạt động
2. Kiểm tra từng node để đảm bảo dữ liệu được truyền đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để thông báo khi có yêu cầu mới
2. Thêm node lưu log các tương tác để phân tích sau này
3. Tạo báo cáo định kỳ về các yêu cầu phổ biến
4. Kết nối với hệ thống thanh toán để tự động hóa quy trình đặt chỗ

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa tạo lịch trình du lịch bằng giọng nói. Với sự kết hợp của ElevenLabs, GPT-4o và Pinecone, các sếp có thể cung cấp trải nghiệm khách hàng tuyệt vời trong khi tiết kiệm đáng kể thời gian và nguồn lực. Hãy thử ngay để thấy sự khác biệt!