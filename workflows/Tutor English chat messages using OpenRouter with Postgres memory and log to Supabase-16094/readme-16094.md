---
title: "🎓 Tạo Trợ Lý Tiếng Anh Thông Minh với OpenRouter và Bộ Nhớ Postgres"
description: "Hướng dẫn tự động hóa tạo trợ lý tiếng Anh nhớ lịch sử trò chuyện của học viên với n8n, OpenRouter và Supabase"
slug: "tao-tro-ly-tieng-anh-thong-minh-voi-openrouter-postgres"
tags: [n8n, automation, no-code, AI, chatbot]
keywords: [n8n workflow, tự động hóa, trợ lý tiếng Anh, OpenRouter, Postgres, Supabase]
---

# 🎓 Tạo Trợ Lý Tiếng Anh Thông Minh với OpenRouter và Bộ Nhớ Postgres

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các trung tâm tiếng Anh khi phải trả lời hàng trăm câu hỏi tương tự hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian trả lời câu hỏi lặp lại
- Nhớ lịch sử trò chuyện của từng học viên
- Tự động ghi log tất cả cuộc trò chuyện
- Tích hợp dễ dàng với các nền tảng khác
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenRouter (miễn phí có giới hạn)
- Cơ sở dữ liệu PostgreSQL (cho bộ nhớ trò chuyện)
- Dự án Supabase với bảng `conversations` (các cột: user_id, role, message)
- Tài khoản n8n đã cài đặt và chạy
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/16094](https://n8n.io/workflows/16094)
2. Nhấn nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON workflow và chọn "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node**:
   - Đảm bảo đường dẫn webhook là duy nhất (đã được tạo sẵn: `e5626949-1022-4883-a045-3d118685694d`)
   - Kiểm tra phương thức HTTP là POST

2. **OpenRouter Chat Model Node**:
   - Thêm credentials OpenRouter API
   - Có thể thay đổi model (mặc định: `poolside/laguna-m.1:free`)
   - Đăng ký tài khoản OpenRouter tại [https://openrouter.ai/](https://openrouter.ai/)

3. **Postgres Chat Memory Node**:
   - Thêm credentials PostgreSQL
   - Đảm bảo database có bảng `conversations` với cấu trúc:
     ```sql
     CREATE TABLE conversations (
       user_id TEXT,
       role TEXT,
       message TEXT
     );
     ```

4. **Supabase Node**:
   - Thêm credentials Supabase API
   - Đảm bảo bảng `conversations` đã được tạo

5. **Edit Fields Node**:
   - Kiểm tra các biểu thức trích xuất dữ liệu từ webhook
   - Nếu thay đổi tên trường đầu vào, hãy cập nhật các biểu thức tương ứng

6. **AI Agent Node**:
   - Tùy chỉnh prompt hệ thống để thay đổi phong cách giảng dạy
   - Ví dụ: "Hãy giải thích lỗi ngữ pháp một cách đơn giản và thân thiện"

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu:
   ```json
   {
     "user_id": "student_123",
     "message": "I goed to the market yesterday."
   }
   ```
2. Kiểm tra phản hồi từ trợ lý tiếng Anh
3. Bật Active workflow để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối với Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận tin nhắn từ học viên
2. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo hàng tuần về tiến độ học tập
3. **Tích hợp với LMS**: Kết nối với hệ thống quản lý học tập để theo dõi kết quả
4. **Tùy chỉnh model**: Thử nghiệm với các model khác như GPT-4o, Claude, hoặc Gemini

### 📌 Kết luận
Workflow này tạo ra một trợ lý tiếng Anh thông minh hoàn toàn tự động, nhớ lịch sử trò chuyện của từng học viên và ghi log tất cả cuộc trò chuyện. Với việc tích hợp dễ dàng và khả năng hoạt động liên tục 24/7, đây là giải pháp hoàn hảo cho các trung tâm tiếng Anh muốn tối ưu hóa thời gian và nâng cao chất lượng giảng dạy. Hãy thử ngay và biến đổi cách dạy học của bạn!