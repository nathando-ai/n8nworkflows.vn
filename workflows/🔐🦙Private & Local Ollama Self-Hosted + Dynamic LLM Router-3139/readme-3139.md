---
title: "🔐🦙 Tự động hóa Ollama Local + Dynamic LLM Router - Giải pháp AI tự chủ 100% không cần cloud"
description: "Hướng dẫn tự động hóa Ollama local với Dynamic LLM Router - Giải pháp AI tự chủ 100% không cần cloud, tối ưu hóa hiệu suất LLM dựa trên yêu cầu người dùng"
slug: "ollama-dynamic-llm-router-tu-dong-hoa"
tags: [n8n, automation, no-code, AI, LLM, Ollama]
keywords: [n8n workflow, tự động hóa, LLM, Ollama, AI tự chủ]
---

# 🔐🦙 Tự động hóa Ollama Local + Dynamic LLM Router - Giải pháp AI tự chủ 100% không cần cloud

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình chọn LLM phù hợp dựa trên yêu cầu người dùng
- Tiết kiệm thời gian và tài nguyên bằng cách không cần gửi dữ liệu ra bên ngoài
- Tăng tính chính xác của kết quả nhờ hệ thống routing thông minh
- Hoạt động liên tục 24/7 với hiệu suất tối ưu
- Bảo mật dữ liệu tuyệt đối nhờ chạy hoàn toàn local
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Máy chủ local chạy Ollama (cài đặt và cấu hình Ollama trước khi sử dụng workflow)
- Các model Ollama cần thiết đã được pull về local (phi4:latest, các model khác tùy theo nhu cầu)
- Tài khoản n8n đã được cấu hình và chạy ổn định
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When chat message received" (chatTrigger)**:
   - Cấu hình webhook endpoint để nhận tin nhắn từ người dùng
   - Đảm bảo endpoint này được truy cập được từ các ứng dụng chat của bạn

2. **Node "Ollama Dynamic LLM" (lmChatOllama)**:
   - Thêm credentials "ollamaApi" với URL mặc định: http://127.0.0.1:11434
   - Model sẽ được động chọn thông qua output từ node "LLM Router"

3. **Node "LLM Router" (agent)**:
   - Đây là node quan trọng nhất trong workflow, nó quyết định model nào sẽ được sử dụng
   - Có thể tùy chỉnh prompt trong node này để điều chỉnh logic routing
   - Đảm bảo các model cần thiết đã được pull về local trước khi sử dụng

4. **Node "AI Agent with Dynamic LLM" (agent)**:
   - Node này sử dụng model được chọn bởi router để xử lý yêu cầu
   - Có thể tùy chỉnh prompt và hành vi của agent này

5. **Node "Ollama phi4" (lmChatOllama)**:
   - Thêm credentials "ollamaApi" với URL mặc định: http://127.0.0.1:11434
   - Model được sử dụng là phi4:latest

6. **Node "Router Chat Memory" (memoryBufferWindow)** và **Node "Agent Chat Memory" (memoryBufferWindow)**:
   - Cấu hình kích thước bộ nhớ phù hợp với nhu cầu của bạn
   - Có thể điều chỉnh các tham số như k (số lượng tin nhắn lưu trữ) và các tùy chọn khác

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo tất cả các node hoạt động đúng cách
- Kiểm tra kết quả từ các node để đảm bảo routing và xử lý yêu cầu hoạt động như mong đợi
- Bật Active workflow sau khi đã kiểm tra và xác nhận mọi thứ hoạt động tốt

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các model khác vào hệ thống routing để mở rộng khả năng xử lý của workflow
- Tích hợp với các nền tảng chat như Slack, Telegram để tạo giao diện người dùng thân thiện hơn
- Thêm node để lưu log các yêu cầu và phản hồi để phân tích hiệu suất
- Tạo báo cáo định kỳ về hiệu suất sử dụng các model khác nhau
- Tích hợp với các hệ thống quản lý tài liệu để cung cấp ngữ cảnh bổ sung cho các model

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa và tối ưu hóa sử dụng các model LLM local. Bằng cách tự động routing giữa các model khác nhau dựa trên yêu cầu của người dùng, workflow này giúp tăng hiệu suất, bảo mật dữ liệu và giảm chi phí vận hành. Các sếp có thể dễ dàng triển khai và tùy chỉnh workflow này để phù hợp với nhu cầu cụ thể của doanh nghiệp.