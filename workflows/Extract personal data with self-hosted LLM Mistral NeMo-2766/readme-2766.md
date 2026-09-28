---
title: "🚀 Trích xuất dữ liệu cá nhân tự động chuẩn xác với Self-hosted LLM Mistral NeMo trên n8n"
description: "Hướng dẫn xây dựng hệ thống tự động trích xuất thông tin cá nhân từ văn bản phi cấu trúc sử dụng AI mô hình Mistral NeMo chạy local qua Ollama và n8n."
slug: "trich-xuat-du-lieu-ca-nhan-voi-mistral-nemo-n8n"
tags: [n8n, automation, ai, ollama, mistral-nemo, structured-output]
keywords: [n8n workflow, trích xuất dữ liệu ai, mistral nemo ollama, structured output parser, tự động hóa n8n]
---

# 🚀 Trích xuất dữ liệu cá nhân tự động chuẩn xác với Self-hosted LLM Mistral NeMo

Các sếp có bao giờ gặp khó khăn khi phải bóc tách thông tin cá nhân (họ tên, email, số điện thoại, địa chỉ, v.v.) từ các đoạn văn bản dài lộn xộn, CV ứng viên hay email khách hàng chưa? Làm thủ công vừa mất thời gian, dễ bỏ sót lại cực kỳ nhàm chán. 

Giải pháp cho các sếp đây: Workflow n8n tích hợp **Self-hosted LLM Mistral NeMo** thông qua **Ollama**. Hệ thống này sẽ giúp các sếp trích xuất dữ liệu tự động 100%, trả về định dạng JSON chuẩn chỉnh mà không cần tốn chi phí thuê API bên thứ ba, đồng thời bảo mật tuyệt đối dữ liệu nội bộ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Biến văn bản thô thành dữ liệu cấu trúc (JSON) chỉ trong vài giây.
- **Bảo mật tối đa**: Chạy mô hình AI hoàn toàn trên hạ tầng riêng (local) với Ollama, không lộ dữ liệu khách hàng ra ngoài.
- **Độ chính xác cao với Auto-Fixer**: Tự động phát hiện lỗi cấu trúc phản hồi từ LLM và yêu cầu sửa lỗi thông minh trước khi xuất dữ liệu.
- **Tiết kiệm chi phí**: Không tốn phí gọi API OpenAI hay Anthropic, tận dụng tối đa phần cứng sẵn có.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Self-hosted hoặc Cloud).
- Đã cài đặt **Ollama** trên máy chủ local hoặc VPS riêng và tải sẵn model `mistral-nemo:latest`.
- Credentials kết nối Ollama trong n8n (`ollamaApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Ollama Chat Model**: 
  - Chọn đúng credentials kết nối tới server Ollama của các sếp.
  - Đảm bảo thông số `Model` được đặt chính xác là `mistral-nemo:latest`.
- **Structured Output Parser & Define JSON Schema**: 
  - Cấu hình cấu trúc JSON (JSON Schema) mà các sếp muốn LLM trả về (ví dụ: `name`, `email`, `phone`, `address`).
- **Basic LLM Chain**:
  - Khi thay đổi nguồn dữ liệu đầu vào (data source), nhớ cập nhật lại `Prompt Source (User Message)` trong node này để AI hiểu đúng ngữ cảnh cần bóc tách.
- **Auto-fixing Output Parser**:
  - Node này cực kỳ quan trọng: Nếu phản hồi từ LLM không khớp với JSON Schema đã định nghĩa, Auto-Fixer sẽ tự động gọi lại mô hình với một prompt bổ sung để chỉnh sửa định dạng mà không làm gián đoạn workflow.
- **Extract JSON Output (Set node)**:
  - Dùng để chuẩn hóa và lọc ra kết quả JSON cuối cùng, sẵn sàng cho các bước xử lý tiếp theo (như lưu vào Google Sheets, Database hoặc gửi về Webhook).

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với một đoạn văn bản mẫu chứa thông tin cá nhân qua node **When chat message received** hoặc chat trigger.
- Kiểm tra kết quả đầu ra ở node **Extract JSON Output**.
- Nếu mọi thứ mượt mà, bật **Active** workflow để hệ thống chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình này cho doanh nghiệp, các sếp có thể mở rộng thêm:
1. **Kết nối Google Sheets / Airtable**: Tự động lưu thông tin cá nhân đã trích xuất vào bảng tính để quản lý CRM hoặc data khách hàng.
2. **Tích hợp Telegram / Slack Bot**: Cho phép nhân viên gửi đoạn chat/CV trực tiếp vào bot, bot sẽ tự động bóc tách và trả kết quả về group chat ngay lập tức.
3. **Xử lý hàng loạt (Batch processing)**: Thay vì nhận từng message qua chat, các sếp có thể kết nối nguồn dữ liệu từ email đến (IMAP) hoặc file Excel tải lên.

### 📌 Kết luận
Ứng dụng AI self-hosted với Mistral NeMo và n8n là chìa khóa giúp doanh nghiệp tối ưu hóa quy trình xử lý dữ liệu phi cấu trúc mà vẫn đảm bảo an toàn tuyệt đối về mặt thông tin. Chúc các sếp "lên đồ" thành công và hẹn gặp lại ở các bài hướng dẫn tiếp theo!