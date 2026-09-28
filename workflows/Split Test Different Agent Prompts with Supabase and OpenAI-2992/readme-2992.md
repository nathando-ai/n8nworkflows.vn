---
title: "🚀 Tự động hóa A/B Test Prompt với Supabase và OpenAI - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động hóa A/B test prompt cho LLM với n8n, Supabase và OpenAI. Tiết kiệm thời gian và tối ưu hóa hiệu suất LLM một cách khoa học."
slug: "tu-dong-hoa-ab-test-prompt-voi-supabase-openai"
tags: [n8n, automation, no-code, AI, OpenAI]
keywords: [n8n workflow, tự động hóa, A/B test, prompt engineering, OpenAI]
---

# 🚀 Tự động hóa A/B Test Prompt với Supabase và OpenAI - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi cần thử nghiệm nhiều phiên bản prompt khác nhau cho LLM (Large Language Model) để tìm ra phiên bản hiệu quả nhất. Quá trình này thường phải thực hiện thủ công, tốn thời gian và không khoa học. Workflow này sẽ giúp các sếp tự động hóa quá trình A/B test prompt một cách hiệu quả, tiết kiệm thời gian và tối ưu hóa hiệu suất LLM một cách khoa học.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa quá trình A/B test prompt cho LLM
- Tiết kiệm thời gian và chi phí thử nghiệm thủ công
- Tối ưu hóa hiệu suất LLM một cách khoa học
- Theo dõi và phân tích kết quả thử nghiệm một cách dễ dàng
- Tăng cường tính cá nhân hóa cho trải nghiệm người dùng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Supabase với bảng `split_test_sessions` có các cột: `session_id` (text) và `show_alternative` (bool)
- API Key của OpenAI
- Kết nối PostgreSQL
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor. Để import từ file JSON, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/2992](https://n8n.io/workflows/2992)
2. Nhấp vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, nhấp vào nút "Import" và chọn file JSON đã tải về

Hoặc các sếp có thể copy/paste JSON vào n8n Editor bằng cách:

1. Truy cập vào trang [n8n.io/workflows/2992](https://n8n.io/workflows/2992)
2. Copy toàn bộ nội dung JSON của workflow
3. Trong n8n Editor, nhấp vào nút "Import" và paste nội dung JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý đến các node quan trọng sau trong workflow:

- **When chat message received**: Node này nhận tin nhắn từ người dùng và bắt đầu quá trình xử lý.
- **Check If Session Exists**: Node này kiểm tra xem phiên chat đã tồn tại trong bảng `split_test_sessions` của Supabase hay chưa.
- **If Session Does Exist**: Node này kiểm tra xem phiên chat đã tồn tại hay chưa và thực hiện các hành động tương ứng.
- **Assign Path To Session**: Node này gán giá trị `show_alternative` cho phiên chat trong bảng `split_test_sessions` của Supabase.
- **Define Path Values**: Node này định nghĩa các giá trị cho `baseline_prompt` và `alternative_prompt`.
- **OpenAI Chat Model**: Node này sử dụng mô hình OpenAI để tạo phản hồi cho người dùng.
- **Postgres Chat Memory**: Node này lưu trữ lịch sử trò chuyện trong cơ sở dữ liệu PostgreSQL.
- **Get Correct Prompt**: Node này lấy prompt phù hợp để sử dụng trong quá trình tạo phản hồi.

Các sếp cần cấu hình các node này theo hướng dẫn sau:

1. **When chat message received**: Không cần cấu hình gì thêm.
2. **Check If Session Exists**:
   - Chọn credentials của Supabase
   - Điền các tham số cần thiết cho truy vấn
3. **If Session Does Exist**: Không cần cấu hình gì thêm.
4. **Assign Path To Session**:
   - Chọn credentials của Supabase
   - Điền các tham số cần thiết cho truy vấn
5. **Define Path Values**:
   - Định nghĩa các giá trị cho `baseline_prompt` và `alternative_prompt`
6. **OpenAI Chat Model**:
   - Chọn credentials của OpenAI
   - Chọn mô hình OpenAI (ví dụ: `gpt-4o-mini`)
7. **Postgres Chat Memory**:
   - Chọn credentials của PostgreSQL
   - Điền các tham số cần thiết cho truy vấn
8. **Get Correct Prompt**: Không cần cấu hình gì thêm.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong các node, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu xử lý tin nhắn từ người dùng.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận tin nhắn từ người dùng và tạo phản hồi tự động.
- Các sếp có thể lưu log các phiên chat để theo dõi và phân tích kết quả thử nghiệm.
- Các sếp có thể gửi báo cáo định kỳ về kết quả thử nghiệm để đánh giá hiệu suất của các phiên bản prompt.

### 📌 Kết luận
Workflow "Split Test Different Agent Prompts with Supabase and OpenAI" giúp các sếp tự động hóa quá trình A/B test prompt cho LLM một cách hiệu quả, tiết kiệm thời gian và tối ưu hóa hiệu suất LLM một cách khoa học. Các sếp nên áp dụng ngay workflow này để nâng cao trải nghiệm người dùng và tăng cường tính cá nhân hóa cho sản phẩm của mình.